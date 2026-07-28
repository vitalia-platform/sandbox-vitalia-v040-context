# Aprendizados

- [PROJETO] A documentação técnica estava excessivamente focada em infraestrutura bruta (Redis, GPUs) e desconectada do valor de negócio (SDD e Medical Gates). A reestruturação por persona e a divisão em módulos (Básico, Intermediário, Avançado) resolveu esse débito técnico.
- [KIT] O uso do comando `/vitalia-brainstorming` (protocolo socrático) foi essencial para apresentar as opções de arquitetura da documentação (Prós e Contras) antes de aplicar qualquer alteração real, evitando retrabalho.
- [KIT] Fricção no workflow SDD é uma _feature_ de segurança, blindando a arquitetura contra "vibe coding" (execuções impulsivas sem contexto).
- [KIT] Centralizar as restrições comportamentais na Constituição (`architect-constitution.md`) garante obediência universal, não importando a IDE ou orquestrador que consuma o Kit.
- [KIT] O desacoplamento prévio do código focado estritamente na especificação via `/vitalia-brainstorming` provou-se altamente eficaz para validar resiliência de rede (WSL2 NAT) e restrições de hardware antes de qualquer geração de código.
- [DASHBOARD] A separação entre Cold Load (carregamento de modelo na GPU) e Warm Inference em benchmarks de LLM é indispensável para diagnosticar gargalos de VRAM em nós híbridos (NVIDIA GTX 1060 vs MX450).
