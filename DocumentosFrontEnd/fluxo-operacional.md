# Fluxos Operacionais do App

Ultima revisao: 13/04/2026

## 1. Fluxo de Entrada no App
1. Usuario abre o app.
2. Splash valida conectividade e credenciais locais.
3. App chama /usuarios/login.
4. Com base em status_cadastro:
   - menor que 5: alerta candidatura em analise
   - igual a 5: alerta candidatura reprovada
   - maior ou igual a 6: entra nas tabs
5. Se houve push clicado, a rota recebida tem prioridade.

## 2. Fluxo de Vagas e Candidatura
1. Tela de vagas carrega lista por /Vagas/vagas_disponiveis.
2. Usuario visualiza vaga compativel.
3. Ao candidatar, app envia /Candidatar/.
4. Tela de candidaturas consulta:
   - /Candidaturas/motorista_filter
   - /Candidaturas/status_candidatura
   - /Candidaturas/detalhes_servico
5. Se necessario, usuario remove candidatura por /deleteCandidatura/remover.

## 3. Fluxo de Servico Ativo
1. Aba Servico carrega /Servicos/ativos e /Servicos/status_filtrados.
2. App ajusta botoes e etapas conforme status.
3. Acao operacional dispara /UpdateStatus/.
4. App atualiza notificacao de etapa com /StatusNotificacao/attStatus.
5. Em manutencao, app atualiza etapa com /AttManutencao/ e pode registrar ocorrencia em /InsertManutencao/.

## 4. Fluxo de Documentos
1. App autentica no Sisgen por /auth-integracao.php.
2. App consulta disponibilidade via /consulta_arquivos.php e /consulta_contrato_assinado.php.
3. App baixa por /exibe_arquivos.php e atualiza backend em /UpdateStatus/status_arquivos_baixados.
4. Para upload:
   - /upload_foto
   - /uploadProcesso
   - /uploadProcessoLote
   - /inserir_arquivo_processo.php (Sisgen)

## 5. Fluxo de Notificacoes e Alertas
1. App gera token Expo em utils/gerarTokenNotificacao.ts.
2. Envia token para /EnviarNotificacao/salvar_token.
3. Ao clicar em push, listener salva payload em memoria global.
4. App retorna ao splash e reaplica roteamento.
5. Em paralelo, hooks de polling exibem alertas:
   - pre-selecionado
   - selecionado
   - carga liberada

## 6. Fluxo de Localizacao (Online/Offline)
1. Rastreamento inicia apos login aprovado e permissoes de localizacao.
2. Antes de registrar tarefas, o app valida permissao foreground, permissao background e GPS; se necessario, solicita novamente ou direciona o usuario para configuracoes.
3. Se o rastreamento ja estiver ativo ou em inicializacao, a chamada e ignorada para evitar restart duplicado.
4. Task de background coleta coordenadas periodicamente.
5. Se online:
   - envia para backend (/InsertLocation/detalhes)
   - envia para Sisgen (/atualiza_localizacao.php)
   - grava log de entrada da funcao Sisgen com status 0000 em /InsertLocation/log_sisgen
   - grava logs de retorno, timeout ou erro em /InsertLocation/log_sisgen
6. Se offline:
   - salva ponto no SQLite local
7. Ao reconectar:
   - sincroniza pendencias via /InsertLocation/sincronizar

## 7. Fluxo de Sincronizacao de Pendencias Locais
1. app/pages/_layout.tsx executa carregarDados() e sincronizar() na entrada das tabs.
2. Listener de conectividade (NetInfo) detecta retorno da internet.
3. App chama sincronizar() novamente para subir pendencias de localizacao/operacao.

## 8. Fluxo de Cadastro Assistido por OCR
1. Usuario captura imagem no passo de cadastro.
2. App envia imagem para OCR/IA:
   - /ocrGoogleVision/
   - /geminiLerVeiculos/
   - /geminiExtrairAntt/
   - /geminiComprovanteEntrega/
3. Campos detectados preenchem formularios.
4. Usuario confirma e app grava nas rotas de cadastro.
