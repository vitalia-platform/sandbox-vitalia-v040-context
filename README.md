# Contexto Multi-Máquina (Vitalia Kit)

Bem-vindo ao repositório de memória de contexto do seu projeto. Este repositório é projetado para permitir que múltiplos agentes (em múltiplas máquinas físicas, contêineres ou WSLs) colaborem no mesmo projeto simultaneamente sem corromper o histórico ou sobrescrever o trabalho uns dos outros.

Para visualizar o estado ativo da sessão e o dashboard visual com diagramas Mermaid, acesse [DASHBOARD.md](./DASHBOARD.md).

---

## 🏗️ Arquitetura dos Arquivos

A estrutura do contexto foi modernizada na Spec 3.1 para suportar a arquitetura **3-Tier**:

1. **`DASHBOARD.md`**: Visão visual agregada gerada automaticamente. Mostra quais máquinas estão ativas, o diagrama Mermaid e o estado do semáforo de consolidação.
2. **`SESSION_STATE.md`**: Estado consolidado ativo e o Próximo Passo (P0).
3. **`data/*.jsonl`**: A fonte da verdade imutável (append-only) para Aprendizados (`learnings.jsonl`), Decisões (`decisions.jsonl`) e Histórico (`session_history.jsonl`).
4. **`shards/*.yaml`**: Arquivos isolados por máquina. Cada agente escreve exclusivamente no seu arquivo `shard` para notificar ao cluster o que ele está fazendo.
5. **`LEARNINGS.md`, `DECISIONS.md`, `SESSION_HISTORY.md`**: Visões read-only geradas pelo motor de contexto a partir dos arquivos `.jsonl`.

---

## 🚦 Protocolo do Semáforo (Lock System)

Como múltiplas máquinas podem tentar consolidar os dados simultaneamente (ex: duas máquinas finalizando a sessão ao mesmo tempo), o Vitalia Kit implementa um semáforo distribuído via `DASHBOARD.md`.

1. **Tentativa de Lock**: Antes de rodar a consolidação, o Agente lê o `DASHBOARD.md`.
2. **Verificação de Expiração**: Se o semáforo estiver `LOCKED`, o agente compara o `expires_at`.
   - Se estiver no futuro: o agente aborta silenciosamente ou emite um aviso HITL.
   - Se estiver no passado: o agente adquire o lock forçadamente (staleness recovery).
3. **Write**: O agente atualiza o arquivo `DASHBOARD.md` para `LOCKED`, faz o push, e roda o processamento intensivo.
4. **Release**: O agente altera o `DASHBOARD.md` para `LIVRE` após empurrar todas as visões para a nuvem.

---

## 🔑 Configuração SSH/PAT

Para o sincronismo ocorrer de forma transparente, o agente local BASH *deve* ter permissão de push sem intervenção humana.

- **Recomendado (SSH)**: Garanta que sua chave `~/.ssh/id_rsa` esteja em seu SSH agent e registrada no GitHub. O agente usará a chave automaticamente.
- **Alternativa (PAT)**: Se usar HTTPS, armazene seu Personal Access Token via git credential helper:
  `git config --global credential.helper store`

---

## ❓ FAQ & Erros Conhecidos

- **Erro `Merge conflict in DASHBOARD.md`**:
  Ocorre raramente quando duas máquinas adquirem o lock ao mesmo milissegundo. 
  **Solução**: Rode `/vitalia-session-consolidate` manualmente para forçar um rebase e sobreposição controlada.
- **Perda de Dados em `LEARNINGS.md`**:
  Nunca edite o arquivo `.md` diretamente, pois ele será sobrescrito. Adicione novidades no arquivo `data/learnings.jsonl`.
- **"O agente parou no meio do pull"**:
  Isso acontece se sua chave SSH expirou ou necessita de passphrase e não está no ssh-agent. Desbloqueie sua chave SSH via terminal.

---
_Gerado automaticamente pelo Vitalia Kit (Spec 3.1) - Última Atualização do README: Jul/2026_
