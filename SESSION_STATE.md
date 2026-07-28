# Estado da Sessão

**Atividades recentes:**
- Implementação de `StreamPublisher` e `StreamConsumer` conectados ao Redis Streams.
- Manipulação assíncrona das inferências do LLM e integração com `.cancel()` de Tasks no `asyncio` e ACKs em tempo real (`CANCEL_INTENT` -> `CANCELLED_PROMPT`).
- Testes massivos de stress test, validando a segurança anti-leak do `zombie_timer` e monotonicidade do `UUID v7`.
- Cobertura de testes atingida em **91%** global e documentação atualizada (`README.md`, `.env.example`).
- Criação e validação do pipeline final em uma demonstração real-time (`run_demo.py`).

## Próximo Passo (P0)
- Iniciar os preparativos para o setup Multimáquinas (Nó 1 x Nó 2 físico) usando a engine de lock recém construída, ou partir para a implementação da próxima SPEC (`003`) da arquitetura.
