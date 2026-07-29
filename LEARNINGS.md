# Aprendizados

- [PROJETO] A documentação técnica estava excessivamente focada em infraestrutura bruta (Redis, GPUs) e desconectada do valor de negócio (SDD e Medical Gates). A reestruturação por persona e a divisão em módulos (Básico, Intermediário, Avançado) resolveu esse débito técnico.
- [KIT] O uso do comando `/vitalia-brainstorming` (protocolo socrático) foi essencial para apresentar as opções de arquitetura da documentação (Prós e Contras) antes de aplicar qualquer alteração real, evitando retrabalho.
- [KIT] Fricção no workflow SDD é uma _feature_ de segurança, blindando a arquitetura contra "vibe coding" (execuções impulsivas sem contexto).
- [KIT] Centralizar as restrições comportamentais na Constituição (`architect-constitution.md`) garante obediência universal, não importando a IDE ou orquestrador que consuma o Kit.
- [KIT] O desacoplamento prévio do código focado estritamente na especificação via `/vitalia-brainstorming` provou-se altamente eficaz para validar resiliência de rede (WSL2 NAT) e restrições de hardware antes de qualquer geração de código.
- [DASHBOARD] A separação entre Cold Load (carregamento de modelo na GPU) e Warm Inference em benchmarks de LLM é indispensável para diagnosticar gargalos de VRAM em nós híbridos (NVIDIA GTX 1060 vs MX450).
- [PROJETO] O uso de `zombie_timer` (`asyncio.create_task`) que vigia a desconexão dos workers precisou de cancelamento explícito via código na hora de confirmar a posse do RED lock. Sem isso o loop vazava tarefas assíncronas dormindo nos nós (detectado e mitigado no Stress Test).
- [PROJETO] Manipulação nativa do `fakeredis` e instâncias do `redis` assíncrono em Python exigiu tratamento assertivo de codificação entre `bytes` e `str` no trânsito das chaves e valores.
- [PROJETO] A versão 0.4+ do Microsoft AutoGen fragmentou a arquitetura em `autogen-core` e `autogen-ext`, quebrando a compatibilidade retroativa com a UI legada `autogenstudio`. Foi necessário adotar scripts puros para validar infraestrutura sem fricção e isolar a biblioteca legada para futura refatoração.
- [PROJETO] O motor Ollama retorna HTTP 404 (Not Found) no endpoint `/api/generate` quando o modelo especificado não está presente localmente na máquina servidora, o que exige um tratamento de erro mais claro do que um genérico falha de endpoint.
- [KIT] Para testar hipóteses de infraestrutura, usar scripts minimalistas nativos (ex: httpx, redis) é mais confiável e à prova de "dependency hell" do que carregar todo o contexto da aplicação.
- [KIT] O Uvicorn ignora a diretiva `pythonpath` do `pyproject.toml`, sendo obrigatória a flag `--app-dir src` no `README` ao utilizar "Src Layout" em projetos FastAPI não instalados globalmente.
- [PROJETO] Modificações arquiteturais na estrutura de arquivos exigem correções duplas nos testes, especialmente ao aplicar mocks (`@patch`) em caminhos de importação.
