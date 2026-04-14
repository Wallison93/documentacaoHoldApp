# 02 - Funcionalidades Por Dominio

Este arquivo descreve as funcionalidades principais com profundidade media: metodo, endpoint, arquivo e finalidade.

## 1) Autenticacao e usuario

Base: `/usuarios`

- `GET /usuarios/`
  - Arquivo: `routes/usuarioRoutes.js`
  - Finalidade: listar usuarios (campo usuario) para verificacao basica.

- `POST /usuarios/login`
  - Arquivo: `routes/usuarioRoutes.js`
  - Finalidade: autenticar por CPF/email + senha, validar com bcrypt e retornar `token_API` JWT.

## 2) Servicos (viagens)

Base: `/servicos`

- `GET /servicos/servicos_disponiveis`
  - Arquivo: `routes/servicos/servicos.js`
  - Finalidade: listar servicos com status disponivel.

- `GET /servicos/todos_servicos`
  - Arquivo: `routes/servicos/servicos.js`
  - Finalidade: listar todos os servicos.

- `GET /servicos/buscar_por_id`
  - Arquivo: `routes/servicos/servicos.js`
  - Finalidade: obter dados de um servico por id.

- `GET /servicos/buscar_Motorista_designado`
  - Arquivo: `routes/servicos/servicos.js`
  - Finalidade: localizar servicos em que motorista foi designado.

- `GET /servicos/buscar_destino_do_servico`
  - Arquivo: `routes/servicos/servicos.js`
  - Finalidade: retornar destino/servicos vinculados ao motorista escolhido.

- `GET /servicos/buscar_dados_servico`
  - Arquivo: `routes/servicos/servicos.js`
  - Finalidade: consultar servico por motorista + status da viagem.

- `GET /servicos/buscar_dados_servico_infosviagem`
  - Arquivo: `routes/servicos/servicos.js`
  - Finalidade: consultar historico de viagem a partir de status minimo.

- `GET /servicos/buscar_servico_finalizados`
  - Arquivo: `routes/servicos/servicos.js`
  - Finalidade: listar servicos finalizados por motorista/status.

- `POST /servicos/inserir_fotos_carga`
  - Arquivo: `routes/servicos/servicos.js`
  - Finalidade: registrar foto da carga para a viagem.

- `POST /servicos/update_fotos_carga`
  - Arquivo: `routes/servicos/servicos.js`
  - Finalidade: atualizar comprovacoes/fotos finais da carga.

## 3) Candidaturas

Base: `/candidatura`

- `GET /candidatura/lista`
  - Arquivo: `routes/candidaturas/candidaturas.js`
  - Finalidade: listar candidaturas.

- `GET /candidatura/buscar_por_motorista`
  - Arquivo: `routes/candidaturas/candidaturas.js`
  - Finalidade: filtrar candidaturas por motorista.

- `POST /candidatura/inserir`
  - Arquivo: `routes/candidaturas/candidaturas.js`
  - Finalidade: cadastrar candidatura em servico.

- `POST /candidatura/update`
  - Arquivo: `routes/candidaturas/candidaturas.js`
  - Finalidade: atualizar status/atributos da candidatura.

- `DELETE /candidatura/remover`
  - Arquivo: `routes/candidaturas/candidaturas.js`
  - Finalidade: remover candidatura.

- `POST /candidatura/motorista_indisponivel`
  - Arquivo: `routes/candidaturas/candidaturas.js`
  - Finalidade: marcar indisponibilidade do motorista.

## 4) Localizacao e status em rota

Base: `/localizacao`

- `GET /localizacao/`
  - Arquivo: `routes/Localizacao/Localizacao.js`
  - Finalidade: listar localizacoes armazenadas.

- `GET /localizacao/buscar_statusMotorista`
  - Arquivo: `routes/Localizacao/Localizacao.js`
  - Finalidade: obter status atual do motorista.

- `POST /localizacao/verificando`
  - Arquivo: `routes/Localizacao/Localizacao.js`
  - Finalidade: validar/recuperar ultimo registro do motorista.

- `POST /localizacao/inserir`
  - Arquivo: `routes/Localizacao/Localizacao.js`
  - Finalidade: inserir primeira localizacao do motorista.

- `POST /localizacao/inserir_localizacao`
  - Arquivo: `routes/Localizacao/Localizacao.js`
  - Finalidade: inserir ponto de localizacao com data/hora.

- `POST /localizacao/update`
  - Arquivo: `routes/Localizacao/Localizacao.js`
  - Finalidade: atualizar latitude/longitude/status.

- `POST /localizacao/update_status`
  - Arquivo: `routes/Localizacao/Localizacao.js`
  - Finalidade: atualizar somente status do motorista.

- `POST /localizacao/updatefoto_iniciorota`
- `POST /localizacao/updatefoto_fimrota`
- `POST /localizacao/updatefoto_comprovante`
  - Arquivo: `routes/Localizacao/Localizacao.js`
  - Finalidade: anexar evidencias fotograficas no ciclo da viagem.

## 5) Cadastro de motorista e veiculo

Base: `/cadastro_motorista`

- `POST /cadastro_motorista/inserir`
  - Arquivo: `routes/Cadastro_motorista/cadastro_motorista.js`
  - Finalidade: inserir dados iniciais de cadastro de motorista.

- `POST /cadastro_motorista/inserir_novo_usuario`
  - Arquivo: `routes/Cadastro_motorista/cadastro_motorista.js`
  - Finalidade: criar novo usuario vinculado ao motorista.

- `POST /cadastro_motorista/update_dados_motorista`
  - Arquivo: `routes/Cadastro_motorista/cadastro_motorista.js`
  - Finalidade: atualizar dados cadastrais do motorista.

- `POST /cadastro_motorista/update_endereco_motorista`
  - Arquivo: `routes/Cadastro_motorista/cadastro_motorista.js`
  - Finalidade: atualizar endereco.

- `POST /cadastro_motorista/inserir_veiculo_por_cpf`
  - Arquivo: `routes/Cadastro_motorista/cadastro_motorista.js`
  - Finalidade: inserir veiculo associado ao CPF.

- `POST /cadastro_motorista/update_dados_veiculo`
  - Arquivo: `routes/Cadastro_motorista/cadastro_motorista.js`
  - Finalidade: atualizar dados do veiculo.

## 6) Consultas auxiliares (lookup e buscas)

- `/lookup_status/*` e `/lookup_enderecos/*`
  - Arquivos: `routes/lookup_status/page.js`, `routes/lookup_enderecos/page.js`
  - Finalidade: tabelas de apoio (status de motorista/viagem/candidatura, estados/cidades).

- `/dados_veiculo/*` e `/dados_motorista/*`
  - Arquivos: `routes/dados_veiculos/page.js`, `routes/dados_motorista/page.js`
  - Finalidade: consulta de dados cadastrais de veiculo/motorista.

- `/buscas/*`
  - Arquivos em `routes/buscas/**`
  - Finalidade: filtros operacionais de candidaturas, historico, servicos, informacoes, vagas, veiculos, enderecos, arquivos e estado/cidade.

## 7) Atualizacoes e manutencao

- `/UpdateStatus/*`, `/StatusNotificacao/*`, `/RecusarServico/*`, `/AttCadastro/*`, `/AttManutencao/*`
  - Arquivos em `routes/atualizar/**`
  - Finalidade: atualizar status de servicos/candidaturas, recusar servico, editar cadastro, registrar manutencao.

- `/Status/*`
  - Arquivo: `routes/Status/status.js`
  - Finalidade: atualizacoes de estado de operacao e consultas de status do motorista.

- `/diario_bordo/*`
  - Arquivo: `routes/Diario_bordo/page.js`
  - Finalidade: registrar ocorrencias, data de inicio/fim e eventos de bordo.

## 8) Uploads, OCR e IA

- Upload de arquivos:
  - `POST /upload_foto/`
  - `POST /uploadProcesso/`
  - `POST /uploadProcessoLote/`
  - Arquivos: `routes/uploads/uploadFoto.js`, `routes/uploads/uploadProcesso.js`, `routes/uploads/uploadProcessoLote.js`
  - Finalidade: envio de imagens e lote de comprovantes (inclui compactacao ZIP no lote).

- Leitura OCR/IA:
  - `POST /ocrGoogleVision/`
  - `POST /geminiLerVeiculos/`
  - `POST /geminiComprovanteEntrega/`
  - `POST /geminiLerContratoAssinado/`
  - `POST /geminiExtrairAntt/`
  - Arquivos: `routes/uploads/googlevision.js` e demais rotas em `routes/uploads/`
  - Finalidade: extrair campos de documentos e identificar tipo de documento/imagem.

## 9) Notificacao e comunicacao

- `POST /EnviarNotificacao/salvar_token`
  - Arquivo: `routes/enviarNotificacao/page.js`
  - Finalidade: salvar/atualizar Expo Push Token por motorista.

- Rotinas internas exportadas (usadas por script cron):
  - `enviarNotificacoesMotoristas(dbz)`
  - `enviarNotificacoesPorTipoVeiculo(dbz)`
  - Arquivo: `routes/enviarNotificacao/page.js`
  - Finalidade: disparo de push pendente por motorista e por compatibilidade de veiculo.

- `POST /notificacao_motorista/salvar_token`
  - Arquivo: `routes/notificacao_motoristaescolhido/page.js`
  - Finalidade: cadastro de token para notificacao no contexto de motorista escolhido.

## 10) Integracoes externas

- `POST /ProxySisgen/atualiza_localizacao`
  - Arquivo: `routes/proxySisgen/proxySisgen.js`
  - Finalidade: encaminhar atualizacao de localizacao para API Sisgen com token Bearer recebido no body.

## 11) Recuperacao de senha

Base: `/recuperar_senha`

- `POST /recuperar_senha/recuperar_senha`
  - Arquivo: `routes/recuperar_senha/page.js`
  - Finalidade: validar email de usuario, gerar codigo e enviar por email via SMTP.

- `GET /recuperar_senha/buscar_parametros`
  - Arquivo: `routes/recuperar_senha/page.js`
  - Finalidade: recuperar dados basicos do usuario por email e gerar token JWT.

- `GET /recuperar_senha/verificar_codigo`
  - Arquivo: `routes/recuperar_senha/page.js`
  - Finalidade: validar codigo enviado para recuperacao.
