<!-- DECISIONS.md | Atualizado em: 30-07-2026 16:27:58(GMT-04:00) -->

# Decisões Arquiteturais

- Decidido reorganizar a documentação do projeto como um "Mini-Curso" focado em SDD (Spec-Driven Development), separando claramente o conteúdo por personas e graus de proficiência (Básico, Intermediário, Avançado), o que aproxima a teoria da prática de Katas interativos. `[pre-migration]`
- O pipeline E2E de validação de testes de bancada foi extraído para ser a "Fonte da Verdade" no `docs/TESTING.md` para evitar redundância na documentação de onboard. `[pre-migration]`
- Centralizar a regra "Kill Switch" exclusivamente em `architect-constitution.md` para proibir planejamentos nativos de IAs, evitando divergências documentais em relação ao `AGENTS.md`. `[pre-migration]`
- Utilizar iteração dinâmica (for loop em bash) no `install-project.sh` para criação dos symlinks das pastas estruturais, ao invés de hardcodar chamadas globais, garantindo isolamento da instância. `[pre-migration]`
- Decidido adotar Redis Streams (garantindo at-least-once delivery contra instabilidade no WSL2 NAT), Distribuição Efêmera de Chaves HMAC via Redis Keyspace dedicado com ACL/TTL (HIPAA/LGPD), e obrigatoriedade de conectores HTTP 100% assíncronos (`httpx.AsyncClient`) para cancelamento rápido via `asyncio.Task.cancel`. `[pre-migration]`
- Decidido criar a arquitetura do Vitalia Node Manager (Dashboard) como um sistema Híbrido (FastAPI Backend + Web App Dashboard interativo + CLI TUI runner), com Descoberta Dupla de Nós (Scanner de Sub-rede Local + Heartbeat via Redis para redes remotas), Barramento de Comandos via Redis Streams com autenticação HMAC (Spec 002), e suíte de Benchmark de LLM com descarregamento obrigatório prévio para medir diferença entre Cold Load e Warm Inference. `[pre-migration]`
- Decidido refatorar a arquitetura legada baseada no framework Autogen (especialmente dependências de UI como `autogenstudio`) devido à quebra de compatibilidade massiva introduzida na v0.4+. O sistema buscará usar bibliotecas fundamentais e nativas sempre que possível para garantir estabilidade no barramento distribuído. `[pre-migration]`
