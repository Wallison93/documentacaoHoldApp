# 01 - Visao Geral

## Objetivo do projeto

Backend Node.js/Express para operacao de motoristas, servicos de transporte, candidaturas, localizacao em viagem, manutencao, notificacoes push e processamento de documentos (upload + OCR/IA).

## Stack principal

- Runtime: Node.js (ESM)
- Framework web: Express
- Banco: MySQL (`mysql2`, usando pool de conexoes)
- Autenticacao: JWT (`jsonwebtoken`)
- Hash de senha: `bcrypt`
- Uploads: `multer`
- IA/OCR:
  - Google Vision (`@google-cloud/vision`)
  - Gemini (`@google/generative-ai`)
  - Tesseract (`tesseract.js`)
- Email: `nodemailer`
- HTTP externo: `axios`

## Estrutura de alto nivel

- `index.js`: bootstrap da aplicacao, middlewares globais e montagem dos modulos de rota.
- `routes/`: endpoints HTTP organizados por contexto de negocio.
- `middleware/Middleware.js`: validacao de token JWT por header `authorization`.
- `config/db.js`: pool de conexoes MySQL.
- `scripts/`: rotinas de notificacao via cron.
- `services/`: extratores e detectores de documentos.

## Fluxos funcionais principais

1. Autenticacao e acesso
- Login por CPF/email + senha (bcrypt).
- Geracao de token JWT para cliente.
- Rotas protegidas validam token antes de executar querys sensiveis.

2. Ciclo de servico/viagem
- Listagem de servicos disponiveis.
- Candidatura do motorista.
- Selecao/pre-selecao e atualizacoes de status.
- Atualizacao de localizacao e status durante execucao.
- Registro de evidencias (fotos/processo/comprovantes).

3. Cadastro de motorista/veiculo
- Insercao e atualizacao de dados cadastrais.
- Atualizacao de endereco, senha e status de cadastro.
- Insercao/atualizacao de veiculos vinculados ao motorista.

4. Notificacoes
- Cadastro de Expo Push Token por motorista.
- Envio em lote para notificacoes pendentes.
- Rotina por tipo de veiculo para abertura de vagas compatveis.

5. OCR e leitura de documentos
- Upload de imagens/arquivos.
- Extracao de campos de documentos (CNH, CRLV, comprovantes etc.).
- Processamento via Gemini/Google Vision conforme endpoint.
