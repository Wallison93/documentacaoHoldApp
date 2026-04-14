# 04 - Operacao E Execucao

## Como rodar localmente

1. Instalar dependencias:
- `npm install`

2. Configurar `.env` com variaveis de banco/JWT/chaves externas.

3. Executar:
- desenvolvimento: `npm run dev`
- producao: `npm start`

## Variaveis de ambiente (esperadas)

- `PORTA` (opcional, default 3306 no codigo)
- `DB_HOST`
- `DB_PORT`
- `DB_USER`
- `DB_PASSWORD`
- `DB_NAME`
- `SECRET_KEY`
- `GEMINI_API_KEY`

## Banco de dados

- Conexao em pool configurada em `config/db.js`.
- A aplicacao faz consultas SQL diretas via `db.query(...)` nos modulos de rota.

## Segurança

- Middleware JWT: `middleware/Middleware.js`
- Header esperado: `authorization`
- Rotas protegidas retornam `403` para token ausente/invalido.

## Uploads e arquivos

- Upload simples de foto/processo via `multer`.
- Upload em lote compacta os arquivos em ZIP (`archiver`) por `cod_processo`.

## Integracoes

- Expo Push API para notificacoes.
- SMTP para recuperacao de senha.
- API Sisgen via proxy interno.
- Gemini/Google Vision para leitura de documentos.

## Rotinas cron

Scripts existentes:

- `scripts/enviarNotificacoesCron.js`
  - Executa `enviarNotificacoesMotoristas(dbz)`.

- `scripts/enviarNotificacaoVeiculoCron.js`
  - Executa `enviarNotificacoesPorTipoVeiculo(dbz)`.

Uso tipico (exemplo):

- `node scripts/enviarNotificacoesCron.js`
- `node scripts/enviarNotificacaoVeiculoCron.js`

## Deploy/Process manager

- Projeto preparado para uso com PM2 (`ecosystem.config.cjs` e anotacoes no `index.js`).
- Recomenda-se manter restart monitorado e logs centralizados.
