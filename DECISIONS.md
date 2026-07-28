# Decisões Arquiteturais

- Decidido reorganizar a documentação do projeto como um "Mini-Curso" focado em SDD (Spec-Driven Development), separando claramente o conteúdo por personas e graus de proficiência (Básico, Intermediário, Avançado), o que aproxima a teoria da prática de Katas interativos.
- O pipeline E2E de validação de testes de bancada foi extraído para ser a "Fonte da Verdade" no `docs/TESTING.md` para evitar redundância na documentação de onboard.
- Centralizar a regra "Kill Switch" exclusivamente em `architect-constitution.md` para proibir planejamentos nativos de IAs, evitando divergências documentais em relação ao `AGENTS.md`.
- Utilizar iteração dinâmica (for loop em bash) no `install-project.sh` para criação dos symlinks das pastas estruturais, ao invés de hardcodar chamadas globais, garantindo isolamento da instância.
