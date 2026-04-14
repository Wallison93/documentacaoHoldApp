# Documentacao do Backend Hold Mobile

Esta pasta centraliza a documentacao funcional do projeto.

## Arquivos

- `01-visao-geral.md`: arquitetura, stack, organizacao e fluxo principal.
- `02-funcionalidades.md`: funcionalidades por dominio (metodo, endpoint, arquivo e finalidade).
- `03-mapa-rotas.md`: mapa consolidado dos prefixos de rota e principais endpoints por modulo.
- `04-operacao.md`: execucao local, variaveis de ambiente, deploy e rotinas cron.

## Observacoes

- A API e exposta por modulos montados em `index.js`.
- Existem alguns endpoints duplicados em arquivos historicos/comentados. Nesta doc, a prioridade foi descrever o comportamento funcional esperado do codigo ativo.
- O projeto usa MySQL (`mysql2`) e JWT para autenticacao em rotas protegidas.
