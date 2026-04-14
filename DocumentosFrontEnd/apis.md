# Catalogo de APIs e Integracoes

Ultima revisao: 13/04/2026

Padrao desta documentacao:
- Metodo HTTP
- Endpoint
- Onde chama
- Finalidade

## 1. Backend Principal (https://apps.uhlelo.com.br)

| Metodo | Endpoint | Onde chama | Finalidade |
|---|---|---|---|
| POST | /usuarios/login | app/components/splashscreen/splashscreen.tsx, app/components/login/page.tsx | Autenticar motorista e retornar token/session data |
| DELETE | /deleteTokenNotification/remover | app/components/buttons/btnLogout.tsx | Remover token de push no logout |
| GET | /Vagas/vagas_disponiveis | hooks/useVagasDisponiveis.ts, hooks/useAlertVagasDisponiveis.ts | Listar vagas elegiveis |
| POST | /Candidatar/ | app/pages/vagas/page.tsx | Registrar candidatura em vaga |
| GET | /Candidaturas/motorista_filter | hooks/useListaCandidaturas.ts | Listar candidaturas do motorista |
| GET | /Candidaturas/status_candidatura | app/pages/candidaturas/page.tsx | Consultar status da candidatura |
| GET | /Candidaturas/detalhes_servico | app/pages/candidaturas/page.tsx | Buscar detalhes da candidatura/servico |
| DELETE | /deleteCandidatura/remover | app/pages/candidaturas/page.tsx | Cancelar/remover candidatura |
| GET | /Servicos/ativos | hooks/useServicosAtivos.ts, utils/salvarLocalizacao.ts | Carregar servicos ativos |
| GET | /Servicos/detalhes | hooks/useDetalhesServico.ts | Buscar detalhes de um servico |
| GET | /Servicos/status_filtrados | app/pages/servico/page.tsx | Buscar status para controles de tela |
| POST | /UpdateStatus/ | utils/atualizarStatusServico.ts, app/pages/servico/page.tsx, app/components/buttons_status/* | Atualizar etapa/status do servico |
| POST | /UpdateStatus/status_arquivos_baixados | hooks/useDownloadArquivos.ts | Atualizar marcador de documentos baixados (total/parcial) |
| POST | /StatusNotificacao/ | utils/aceitarProposta.ts | Alterar status de notificacao de proposta |
| POST | /StatusNotificacao/attStatus | app/pages/servico/page.tsx, app/components/buttons_status/btnTransito.tsx | Atualizar status de notificacao durante execucao |
| POST | /RecusarServico/ | utils/recusarCandidatura.ts | Recusar servico/carga |
| POST | /AttManutencao/ | app/pages/servico/page.tsx | Atualizar etapa de manutencao dentro do fluxo de servico |
| POST | /InsertManutencao/ | app/components/manutencao/manutencao.tsx | Registrar manutencao |
| POST | /InsertLocation/detalhes | utils/salvarLocalizacao.ts, app/pages/servico/page.tsx | Persistir localizacao no backend |
| POST | /InsertLocation/sincronizar | utils/salvarLocalizacao.ts | Sincronizar localizacoes acumuladas offline |
| POST | /InsertLocation/log_sisgen | utils/salvarLocalizacao.ts | Registrar entrada da funcao Sisgen, tentativa, timeout, erro e resultado do envio |
| POST | /InsertLocation_sisgen/ | utils/salvarLocalizacao.ts | Persistir dados de localizacao relacionados ao Sisgen |
| GET | /Informacoes/gerais | hooks/useListaInformacoes.ts | Buscar dados de usuario e veiculos |
| GET | /Informacoes/usuarios | hooks/useServicosAtivos.ts, utils/salvarLocalizacao.ts, telas de alerta/historico | Obter tipo/hierarquia do motorista |
| GET | /Informacoes/statusVeiculo | app/pages/informacoes/page.tsx | Consultar status atual de veiculo |
| GET | /Informacoes/cpfFilter | hooks/useConsultaCpf.ts | Consultar cadastro por CPF |
| GET | /Informacoes/buscarId | app/components/alerts/cadastro_finalizado.tsx | Resolver id do motorista por CPF |
| GET | /Informacoes/motivoRecusado | app/components/alerts/candidatura_reprovada.tsx | Exibir motivo de recusa |
| GET | /Veiculos/placa | hooks/useVerificaPlaca.ts, fluxos cadastro | Validar duplicidade e existencia de placa |
| GET | /Veiculos/getDados | app/cadastro/dados_veiculo.tsx, app/cadastro/leitura_ocr/dados_veiculo.tsx | Carregar dados de veiculo para edicao |
| GET | /Veiculos/especie | fluxos de cadastro de veiculo | Listar especies/tipos de veiculo |
| GET | /Veiculos/filtro_especie | app/pages/vagas/page.tsx, app/pages/candidaturas/page.tsx, app/pages/informacoes/page.tsx, alertas | Filtrar compatibilidade por especie |
| POST | /Cadastro/newUser | app/cadastro/dados_motorista.tsx, app/cadastro/ocr_dadosMotorista.tsx | Criar novo cadastro de motorista |
| POST | /AttCadastro/editDadosMotorista | app/cadastro/dados_motorista.tsx, app/cadastro/leitura_ocr/dados_motorista.tsx | Atualizar dados de motorista |
| POST | /AttCadastro/editDadosMotoristaCpf | app/cadastro/leitura_ocr/dados_motorista.tsx | Atualizacao de motorista por CPF |
| POST | /AttCadastro/dadosEndereco | app/cadastro/dados_endereco.tsx, app/cadastro/ocr_dadosEndereco.tsx | Salvar endereco do cadastro |
| POST | /AttCadastro/dadosEndereco_existente | app/cadastro/dados_endereco.tsx, app/cadastro/leitura_ocr/dados_endereco.tsx | Atualizar endereco de cadastro existente |
| POST | /CadastroVeiculo/ | app/cadastro/dados_veiculo.tsx, app/cadastro/ocr_dadosVeiculo.tsx | Criar veiculo no cadastro |
| POST | /CadastroVeiculo/motorista_existente | app/cadastro/dados_veiculo.tsx | Vincular/atualizar veiculo para motorista existente |
| POST | /AttCadastro/update_dados_veiculo | app/cadastro/dados_veiculo.tsx | Atualizar dados de veiculo existente |
| POST | /AttCadastro/senha | app/cadastro/dados_login.tsx | Definir senha no fluxo de cadastro |
| POST | /AttCadastro/senha_esquecida | app/cadastro/dados_login.tsx | Recuperar senha |
| POST | /AttCadastro/senha_existente | app/cadastro/dados_login.tsx | Alterar senha com validacao da atual |
| GET | /recuperar_senha/verificar_codigo | app/components/password_refresh/verifyToken.tsx | Verificar codigo de recuperacao |
| GET | /recuperar_senha/buscar_parametros | app/components/password_refresh/verifyToken.tsx | Buscar parametros da recuperacao |
| POST | /recuperar_senha/recuperar_senha | app/components/password_refresh/getToken.tsx | Disparar processo de recuperacao |
| POST | /upload_foto | utils/salvarArquivo.ts | Upload de documentos/fotos individuais |
| POST | /uploadProcesso | utils/salvarArquivoProcesso.ts | Upload de arquivo de processo |
| POST | /uploadProcessoLote | utils/salvarArquivosLote.ts | Upload em lote |
| GET | /ArquivosMotorista/{cpf} | utils/buscarArquivos.ts | Listar arquivos do motorista |
| GET | /ArquivosMotorista/{cpf}/{arquivo} | utils/buscarArquivos.ts | Baixar arquivo por nome |
| GET | /PreSelecionado/ | hooks/usePreSelecionado.ts | Buscar alertas de pre-selecao |
| GET | /Selecionado/ | hooks/useSelecionado.ts | Buscar alertas de selecao |
| GET | /CargaLiberada/ | hooks/useCargaLiberada.ts | Buscar eventos de carga liberada |
| POST | /EnviarNotificacao/salvar_token | utils/gerarTokenNotificacao.ts | Registrar expo push token no backend |
| POST | /geminiLerVeiculos/ | utils/geminiLerVeiculo.ts | Extrair dados de veiculo com IA |
| POST | /geminiExtrairAntt/ | utils/geminiExtrairAntt.ts | Extrair dados ANTT com IA |
| POST | /geminiComprovanteEntrega/ | utils/geminiLerComprovante.ts | Ler comprovante de entrega |
| POST | /ocrGoogleVision/ | utils/enviarParaOCR.ts | OCR de imagem/documento |

## 2. Sisgen (https://frotas.sisgen.com.br:34593/API/V3/public)

| Metodo | Endpoint | Onde chama | Finalidade |
|---|---|---|---|
| POST | /auth-integracao.php | hooks/useServicosAtivos.ts, hooks/useDownloadArquivos.ts, app/pages/servico/page.tsx, app/pages/historico/page.tsx, utils/gerarTokenSisgen.ts, utils/salvarArquivosSisgen.ts | Gerar token de integracao Sisgen |
| POST | /consulta_arquivos.php | hooks/useServicosAtivos.ts, app/pages/servico/page.tsx, app/pages/historico/page.tsx | Verificar disponibilidade de arquivos |
| POST | /consulta_contrato_assinado.php | hooks/useServicosAtivos.ts | Verificar contrato assinado |
| POST | /exibe_arquivos.php | app/pages/servico/page.tsx, app/pages/historico/page.tsx, utils/downloadArquivos.ts | Obter URL/arquivo para download |
| POST | /consulta_arquivos_cte.php | app/pages/servico/page.tsx | Verificar arquivos CTe |
| POST | /atualiza_localizacao.php | utils/salvarLocalizacao.ts | Enviar localizacao para Sisgen |
| POST | /inserir_arquivo_processo.php | utils/salvarArquivosSisgen.ts | Enviar arquivos de processo para Sisgen |

## 3. Integracoes Externas de Apoio

| Metodo | Endpoint | Onde chama | Finalidade |
|---|---|---|---|
| GET | https://cep.awesomeapi.com.br/json/{cep} | app/cadastro/dados_endereco.tsx, app/cadastro/ocr_dadosEndereco.tsx, app/cadastro/leitura_ocr/dados_endereco.tsx | Resolver endereco e codigo IBGE via CEP |
| GET | https://clients3.google.com/generate_204 | utils/salvarLocalizacao.ts | Verificacao de internet real para estrategia online/offline |

## 4. Observacoes de Operacao
- A maior parte das rotas usa token salvo no SecureStore e enviado no header Authorization.
- Varios fluxos de alerta usam polling de 1 segundo.
- A trilha de localizacao aplica regras por status de servico (ignora 1, 2 e 6 para envio).
- O inicio do rastreamento em utils/locationTracking.ts revalida permissao foreground, permissao background e GPS antes de registrar as tarefas.
- O envio para Sisgen registra um log inicial com status 0000 antes de buscar token e chamar a API externa.

## 5. Cruzamento com backend-holdMobile
- Repositorio base analisado: https://github.com/devuhlelo/backend-holdMobile
- Documento detalhado de integracao App x Backend: docs/integracao-backend-holdMobile.md
- Observacao de compatibilidade:
	- A rota GET /ArquivosMotorista/{cpf} esta listada neste catalogo como uso do app, porem nao foi localizada no backend atual.
	- A rota confirmada no backend para esse modulo e GET /ArquivosMotorista/{cpf}/{nomeArquivo}.
