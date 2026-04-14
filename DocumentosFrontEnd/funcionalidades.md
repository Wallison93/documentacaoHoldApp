# Funcionalidades do App

Ultima revisao: 13/04/2026

Referencia complementar:
- Para detalhamento de request/response das rotas no backend real, consultar docs/integracao-backend-holdMobile.md.

## 1. Autenticacao e Sessao
Principais arquivos:
- app/components/login/page.tsx
- app/components/splashscreen/splashscreen.tsx
- app/components/buttons/btnLogout.tsx

Capacidades:
- Login de motorista.
- Restauracao de sessao por credenciais salvas.
- Remocao de token de notificacao no logout.
- Encaminhamento por status de cadastro.

APIs relacionadas:
- /usuarios/login
- /deleteTokenNotification/remover

## 2. Cadastro de Motorista e Veiculo
Principais arquivos:
- app/cadastro/dados_motorista.tsx
- app/cadastro/dados_endereco.tsx
- app/cadastro/dados_veiculo.tsx
- app/cadastro/dados_login.tsx
- app/cadastro/ocr_dadosMotorista.tsx
- app/cadastro/ocr_dadosEndereco.tsx
- app/cadastro/ocr_dadosVeiculo.tsx

Capacidades:
- Cadastro inicial em etapas.
- Atualizacao de cadastro existente.
- Validacao de email e placa.
- Upload de documentos do motorista e do veiculo.
- Preenchimento assistido por OCR/Gemini.
- Consulta de CEP para preencher endereco.

APIs relacionadas:
- /Cadastro/newUser
- /AttCadastro/editDadosMotorista
- /AttCadastro/editDadosMotoristaCpf
- /AttCadastro/dadosEndereco
- /AttCadastro/dadosEndereco_existente
- /CadastroVeiculo/
- /CadastroVeiculo/motorista_existente
- /AttCadastro/update_dados_veiculo
- /AttCadastro/senha
- /AttCadastro/senha_esquecida
- /AttCadastro/senha_existente
- /Veiculos/placa
- /Veiculos/getDados
- /Veiculos/especie
- /Candidaturas/emailExistente
- /upload_foto
- /ocrGoogleVision/
- /geminiLerVeiculos/
- /geminiExtrairAntt/
- /geminiComprovanteEntrega/
- CEP externo (awesomeapi)

## 3. Vagas e Candidaturas
Principais arquivos:
- app/pages/vagas/page.tsx
- app/pages/candidaturas/page.tsx
- hooks/useVagasDisponiveis.ts
- hooks/useListaCandidaturas.ts
- hooks/useAlertVagasDisponiveis.ts

Capacidades:
- Listagem de vagas disponiveis para o motorista.
- Candidatura em servico.
- Consulta de status de candidatura e detalhes.
- Remocao de candidatura.
- Notificacao de novas vagas via contexto global.

APIs relacionadas:
- /Vagas/vagas_disponiveis
- /Candidatar/
- /Candidaturas/motorista_filter
- /Candidaturas/status_candidatura
- /Candidaturas/detalhes_servico
- /deleteCandidatura/remover

## 4. Servico Ativo
Principais arquivos:
- app/pages/servico/page.tsx
- hooks/useServicosAtivos.ts
- hooks/useDetalhesServico.ts
- utils/atualizarStatusServico.ts
- utils/aceitarProposta.ts
- utils/recusarCandidatura.ts

Capacidades:
- Exibicao de servicos ativos.
- Atualizacao de status do servico (transito, manutencao, descarga etc).
- Registro de manutencao.
- Controle de notificacao e etapa operacional.

APIs relacionadas:
- /Servicos/ativos
- /Servicos/detalhes
- /Servicos/status_filtrados
- /UpdateStatus/
- /UpdateStatus/status_arquivos_baixados
- /StatusNotificacao/
- /StatusNotificacao/attStatus
- /AttManutencao/
- /InsertManutencao/
- /RecusarServico/

## 5. Historico
Principais arquivos:
- app/pages/historico/page.tsx
- hooks/useListaHistorico.ts

Capacidades:
- Listagem de servicos concluidos.
- Acesso a documentos historicos.

APIs relacionadas:
- /Historico/motorista_filter
- Sisgen: /consulta_arquivos.php e /exibe_arquivos.php

## 6. Informacoes do Motorista
Principais arquivos:
- app/pages/informacoes/page.tsx
- hooks/useListaInformacoes.ts
- hooks/useConsultaCpf.ts

Capacidades:
- Exibir dados de usuario e veiculos.
- Consultar status de veiculo.
- Fluxo de atualizacao de informacoes.

APIs relacionadas:
- /Informacoes/gerais
- /Informacoes/usuarios
- /Informacoes/statusVeiculo
- /Informacoes/cpfFilter
- /Informacoes/buscarId
- /Informacoes/motivoRecusado

## 7. Notificacoes Push
Principais arquivos:
- utils/gerarTokenNotificacao.ts
- utils/notificationHandler.ts

Capacidades:
- Registro do token Expo no backend.
- Recepcao de clique em push e redirecionamento por rota recebida.

APIs relacionadas:
- /EnviarNotificacao/salvar_token

## 8. Localizacao, Offline e Sincronizacao
Principais arquivos:
- utils/locationTracking.ts
- utils/salvarLocalizacao.ts
- hooks/useFiltrarLocalizacoes.ts
- hooks/usePermissaoLocalizacaoObrigatoria.ts

Capacidades:
- Captura de localizacao foreground/background.
- Validacao obrigatoria e recorrente de permissao foreground, permissao background e GPS.
- Reaproveitamento da tela de bloqueio para nova tentativa de permissao e retorno ao fluxo principal quando regularizado.
- Persistencia offline com SQLite.
- Sincronizacao automatica quando volta internet.
- Inicio de rastreamento protegido contra reinicializacoes redundantes.
- Registro de logs de envio para Sisgen, incluindo log de entrada da funcao antes da chamada externa.

APIs relacionadas:
- /InsertLocation/detalhes
- /InsertLocation/sincronizar
- /InsertLocation/log_sisgen
- /InsertLocation_sisgen/
- Sisgen: /atualiza_localizacao.php
