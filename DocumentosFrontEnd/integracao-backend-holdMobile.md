# Integracao com backend-holdMobile

Ultima revisao: 13/04/2026

Repositorio analisado:
- URL: https://github.com/devuhlelo/backend-holdMobile
- Commit de referencia: 33ce9fb

## 1. Como a API autentica
- Middleware: middleware/Middleware.js
- Regra: rotas protegidas exigem header Authorization com JWT.
- Formato usado pelo app: token puro no header Authorization.
- Erros padrao:
  - 403 Token nao fornecido
  - 403 Token invalido

## 2. Rotas chamadas pelo app e confirmadas no backend

## 2.1 Sessao e login
1. POST /usuarios/login
- Arquivo backend: routes/usuarioRoutes.js
- Entrada: body { usuario, senha }
- Regra: usuario pode ser CPF ou email; senha validada com bcrypt.
- Saida de sucesso: { message, token_API, dados }
- Erros comuns: 400 campos obrigatorios, 401 usuario/senha incorretos.

2. DELETE /deleteTokenNotification/remover
- Arquivo backend: routes/deletes/tokenNotification/tokenNotification.js
- Auth: sim
- Entrada: body { id_motorista }
- Saida: confirma remocao de tokens de push do motorista.

## 2.2 Vagas e candidaturas
1. GET /Vagas/vagas_disponiveis
- Arquivo backend: routes/buscas/vagas/vagas.js
- Auth: sim
- Entrada: query id_motorista
- Regra: retorna servicos abertos (status_servico = 1), sem motorista, sem candidatura previa do motorista e com compatibilidade por notificacao/tipo de veiculo.
- Saida: lista de vagas com dados de servico.

2. POST /Candidatar/
- Arquivo backend: routes/inserir/candidatar/candidatar.js
- Auth: sim
- Entrada: body.dados { id_servico, id_motorista, status_candidatura }
- Saida: 201 com message de candidatura criada.

3. GET /Candidaturas/motorista_filter
- Arquivo backend: routes/buscas/candidaturas/candidaturas.js
- Auth: sim
- Entrada: query id_motorista
- Regra: lista candidaturas do motorista com status diferente de 6 e servico com status < 3.

4. GET /Candidaturas/status_candidatura
- Arquivo backend: routes/buscas/candidaturas/candidaturas.js
- Auth: sim
- Entrada: query id (codigo de status)
- Saida: descricao do status na tabela status_candidatura.

5. GET /Candidaturas/detalhes_servico
- Arquivo backend: routes/buscas/candidaturas/candidaturas.js
- Auth: sim
- Entrada: query id (id do servico)
- Saida: dados resumidos do servico.

6. DELETE /deleteCandidatura/remover
- Arquivo backend: routes/deletes/candidaturas/candidaturas.js
- Auth: sim
- Entrada: body { id_servico, id_motorista }
- Saida: message + quantidade removida.

7. GET /Candidaturas/emailExistente
- Arquivo backend: routes/buscas/candidaturas/candidaturas.js
- Auth: nao
- Entrada: query email
- Saida: { existe: true|false, message }

## 2.3 Servicos e historico
1. GET /Servicos/ativos
- Arquivo backend: routes/buscas/servicos/servicos.js
- Auth: sim
- Entrada: query id_motorista
- Regra: busca ultimo servico ativo por motorista (status > 1 e != 6) com dados de notificacao.

2. GET /Servicos/status_filtrados
- Arquivo backend: routes/buscas/servicos/servicos.js
- Auth: sim
- Entrada: query id (status)
- Saida: descricao do status.

3. GET /Servicos/detalhes
- Arquivo backend: routes/buscas/servicos/servicos.js
- Auth: sim
- Entrada: query id (id do servico)
- Saida: campos essenciais de exibicao e documentos_baixados.

4. GET /Historico/motorista_filter
- Arquivo backend: routes/buscas/historico/historico.js
- Auth: sim
- Entrada: query id_motorista
- Regra: retorna servicos com status_servico = 6.

## 2.4 Informacoes do motorista e veiculo
1. GET /Informacoes/gerais
- Arquivo backend: routes/buscas/informacaoes/informacoes.js
- Auth: sim
- Entrada: query id_motorista
- Saida: objeto consolidado { usuario, veiculos }.

2. GET /Informacoes/usuarios
- Arquivo backend: routes/buscas/informacaoes/informacoes.js
- Auth: sim
- Entrada: query id_motorista
- Saida: dados do usuario (inclui hierarquia e status_cadastro).

3. GET /Informacoes/cpfFilter
- Arquivo backend: routes/buscas/informacaoes/informacoes.js
- Auth: nao
- Entrada: query cpf
- Saida: dados de usuario por CPF.

4. GET /Informacoes/buscarId
- Arquivo backend: routes/buscas/informacaoes/informacoes.js
- Auth: nao
- Entrada: query cpf
- Saida: id do usuario.

5. GET /Informacoes/statusVeiculo
- Arquivo backend: routes/buscas/informacaoes/informacoes.js
- Auth: sim
- Entrada: query status
- Saida: descricao_status_veiculo.

6. GET /Informacoes/motivoRecusado
- Arquivo backend: routes/buscas/informacaoes/informacoes.js
- Auth: nao
- Entrada: query id
- Saida: motivo_recusa no cadastro do usuario.

7. GET /Veiculos/filtro_especie
- Arquivo backend: routes/buscas/veiculos/veiculos.js
- Auth: sim
- Entrada: query cod_especie
- Saida: nome da especie de veiculo.

8. GET /Veiculos/especie
- Arquivo backend: routes/buscas/veiculos/veiculos.js
- Auth: nao
- Entrada: sem parametros
- Saida: lista de especies.

9. GET /Veiculos/getDados
- Arquivo backend: routes/buscas/veiculos/veiculos.js
- Auth: sim
- Entrada: query id_veiculo
- Saida: dados detalhados do veiculo.

10. GET /Veiculos/placa
- Arquivo backend: routes/buscas/veiculos/veiculos.js
- Auth: nao
- Entrada: query placa
- Saida: { existe: true|false, message }

## 2.5 Alertas e notificacoes operacionais
1. GET /PreSelecionado/
- Arquivo backend: routes/buscas/preselecionado/preselecionado.js
- Auth: sim
- Entrada: query id_motorista
- Regra: filtra servico_notificacao com id_tipo_notificacao = 2 e status = 1.

2. GET /Selecionado/
- Arquivo backend: routes/buscas/selecionado/selecionado.js
- Auth: sim
- Entrada: query id_motorista
- Regra: filtra servico_notificacao com id_tipo_notificacao = 3 e status = 1.

3. GET /CargaLiberada/
- Arquivo backend: routes/buscas/cargaLiberada/cargaLiberada.js
- Auth: sim
- Entrada: query id
- Regra: filtra servico_notificacao com id_tipo_notificacao = 4 e status = 1.

4. POST /EnviarNotificacao/salvar_token
- Arquivo backend: routes/enviarNotificacao/page.js
- Auth: nao
- Entrada: body { id_motorista, expo_push_token }
- Regra: faz upsert em notificacoes_tokens.

## 2.6 Atualizacoes de status e manutencao
1. POST /UpdateStatus/
- Arquivo backend: routes/atualizar/status_servico/status_servico.js
- Auth: sim
- Entrada: body.dados { id, status, alterarDataInicio? }
- Regra: atualiza status_servico; quando status = 6 atualiza dt_fim; quando status = 3 e alterarDataInicio = 1 atualiza dt_inicio.

2. POST /UpdateStatus/status_arquivos_baixados
- Arquivo backend: routes/atualizar/status_servico/status_servico.js
- Auth: sim
- Entrada: body.dados { cod_processo, documentos_baixados }
- Saida: confirma atualizacao do flag de download.

3. POST /StatusNotificacao/
- Arquivo backend: routes/atualizar/status_candidaturas/status_candidaturas.js
- Auth: sim
- Entrada: body.dados { id, status }
- Regra: atualiza servico_notificacao por id_servico_notificacao.

4. POST /StatusNotificacao/attStatus
- Arquivo backend: routes/atualizar/status_candidaturas/status_candidaturas.js
- Auth: sim
- Entrada: body.dados { id, status }
- Regra: atualiza candidaturas por id_servico.

5. POST /AttManutencao/
- Arquivo backend: routes/atualizar/manutencao/manutencao.js
- Auth: sim
- Entrada: body.dados { cod_processo, id_motorista }
- Regra: fecha manutencao mais recente (data_fim_manutencao = NOW()).

6. POST /InsertManutencao/
- Arquivo backend: routes/inserir/manutencao/manutencao.js
- Auth: sim
- Entrada: body.dados { cod_processo, id_motorista, latitude, longitude, endereco, descricao }
- Regra: cria ocorrencia de manutencao com data_inicio_manutencao em NOW().

7. POST /RecusarServico/
- Arquivo backend: routes/atualizar/recusar_servico/recusar_servico.js
- Auth: sim
- Entrada: body.dados { id_servico, id_motorista }
- Regra: devolve servico para aberto e marca candidatura do motorista como recusada.

## 2.7 Cadastro e atualizacao cadastral
1. POST /Cadastro/newUser
- Arquivo backend: routes/inserir/cadastro/novoUsuario.js
- Auth: nao
- Entrada: body.dados com dados pessoais
- Regra: valida CPF unico antes do INSERT.

2. POST /CadastroVeiculo/
- Arquivo backend: routes/inserir/cadastro/novoVeiculo.js
- Auth: nao
- Entrada: body.dados com cpf e dados do veiculo
- Regra: resolve id_motorista pelo CPF e insere em dados_veiculo.

3. POST /CadastroVeiculo/motorista_existente
- Arquivo backend: routes/inserir/cadastro/novoVeiculo.js
- Auth: nao
- Entrada: body.dados com id do motorista e dados do veiculo
- Saida: 201 com id inserido.

4. POST /AttCadastro/editDadosMotorista
5. POST /AttCadastro/editDadosMotoristaCpf
6. POST /AttCadastro/dadosEndereco
7. POST /AttCadastro/dadosEndereco_existente
8. POST /AttCadastro/update_dados_veiculo
9. POST /AttCadastro/senha
10. POST /AttCadastro/senha_existente
11. POST /AttCadastro/senha_esquecida
- Arquivo backend: routes/atualizar/cadastro/cadasto.js
- Auth: nao (neste arquivo)
- Entrada: body.dados com campos da operacao
- Regras:
  - senhas sao tratadas com bcrypt nas rotas ativas de senha.
  - senha_existente valida senha atual com bcrypt.compare.

## 2.8 Localizacao e logs
1. POST /InsertLocation/detalhes
- Arquivo backend: routes/inserir/localizacao/localizacao.js
- Auth: sim
- Entrada: body.dados { id_servico, usuario, latitude, longitude, status_servico, local, data_criacao, tp_conexao }
- Regra: evita inserir se houver registro recente equivalente em menos de 10 minutos.
- Saida: 201 quando inserido; 200 quando ignorado por intervalo.

2. POST /InsertLocation/sincronizar
- Arquivo backend: routes/inserir/localizacao/localizacao.js
- Auth: sim
- Entrada: mesmo payload de detalhes
- Regra: tambem aplica verificacao de duplicidade por janela de 10 minutos.

3. POST /InsertLocation/log_sisgen
- Arquivo backend: routes/inserir/localizacao/localizacao.js
- Auth: sim
- Entrada: body.dados com console, status_api, processo, lat, lng, local, status, id_motorista, tipo, data_hora, tp_conexao
- Uso atual no app: registra um log logo na entrada de salvarSisgen com mensagem de chamada da funcao e status 0000, alem de logs de token expirado, timeout, erro e resposta final.
- Saida: grava em logs_salvar_sisgen.

4. POST /InsertLocation_sisgen/
- Arquivo backend: routes/inserir/localizacao/localizacao_sisgen.js
- Auth: sim
- Entrada: body.dados semelhante a localizacao + tipo
- Regra: resolve cod_fornecedor a partir de cod_motorista_app; aplica janela de 10 minutos antes de inserir em processo_rota.

## 2.9 Recuperacao de senha
1. POST /recuperar_senha/recuperar_senha
- Arquivo backend: routes/recuperar_senha/page.js
- Auth: nao
- Entrada: body { email }
- Regra: so gera codigo se o email existir em usuarios.
- Saida: mensagem de codigo enviado por email.

2. GET /recuperar_senha/verificar_codigo
- Arquivo backend: routes/recuperar_senha/page.js
- Entrada: query codigo
- Saida: registro do codigo ou 404.

3. GET /recuperar_senha/buscar_parametros
- Arquivo backend: routes/recuperar_senha/page.js
- Entrada: query email
- Saida: { token_API, dados } para continuidade do fluxo.

## 2.10 Uploads e OCR/Gemini
1. POST /upload_foto
- Arquivo backend: routes/uploads/uploadFoto.js
- Entrada multipart: foto + cpf
- Saida: path salvo e identificacao do motorista.

2. POST /uploadProcesso
- Arquivo backend: routes/uploads/uploadProcesso.js
- Entrada multipart: foto + cod_processo
- Saida: path salvo.

3. POST /uploadProcessoLote
- Arquivo backend: routes/uploads/uploadProcessoLote.js
- Entrada multipart: fotos[] + cod_processo
- Saida: gera ZIP caminhao_comprovantes.zip no diretorio do processo.

4. POST /ocrGoogleVision/
- Arquivo backend: routes/uploads/googlevision.js
- Entrada multipart: file
- Saida tipica: { sucesso, campos_detectados, tokens }

5. POST /geminiLerVeiculos/
- Arquivo backend: routes/uploads/geminiLerVeiculos.js
- Entrada multipart: file
- Saida tipica: { sucesso, campos_detectados, tokens }

6. POST /geminiComprovanteEntrega/
- Arquivo backend: routes/uploads/geminiComprovanteEntrega.js
- Entrada multipart: file
- Saida tipica: { sucesso, campos_detectados, tokens }

7. POST /geminiExtrairAntt/
- Arquivo backend: routes/uploads/geminiExtrairAntt.js
- Entrada multipart: file
- Saida tipica: { sucesso, dados, tokens }

## 3. Divergencias identificadas no cruzamento
1. Endpoint documentado no app para listagem GET /ArquivosMotorista/{cpf} nao aparece implementado no backend atual.
- Rota confirmada no backend: GET /ArquivosMotorista/{cpf}/{nomeArquivo}

2. O app tambem usa integracoes Sisgen diretas (/auth-integracao.php, /consulta_arquivos.php, /exibe_arquivos.php etc.), que nao sao rotas desse backend.
- Essas chamadas vao para o host Sisgen configurado em utils/configSisgen.js.

## 4. Recomendacao de manutencao da doc
- Quando atualizar o backend, revisar este arquivo junto com docs/apis.md para manter App e API sincronizados.