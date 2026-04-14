# Arquitetura e Fluxo de Execucao

Ultima revisao: 13/04/2026

## 1. Objetivo
Este documento descreve como o app inicia, como a navegacao principal funciona e quais modulos sustentam o comportamento em tempo real (alertas, localizacao e sincronizacao).

## 2. Bases de Integracao
- Backend principal: https://apps.uhlelo.com.br
- Sisgen: https://frotas.sisgen.com.br:34593/API/V3/public
- Servico externo de CEP: https://cep.awesomeapi.com.br
- Verificacao de internet real: https://clients3.google.com/generate_204

Arquivos de configuracao:
- utils/config.js
- utils/configSisgen.js

## 3. Bootstrap do App
Sequencia de inicializacao:
1. O Expo Router inicia pelo entry definido no package.json.
2. app/_layout.tsx monta o Stack raiz, registra usePushNotificationListener e envolve tudo com VagasProvider.
3. app/index.tsx renderiza app/components/splashscreen/splashscreen.tsx.
4. Splash executa:
   - checagem de conectividade com NetInfo
   - leitura de credenciais salvas no SecureStore
   - login em /usuarios/login
   - roteamento por status_cadastro
  - tentativa de inicio do rastreamento de localizacao quando status_cadastro >= 6

## 4. Decisao de Roteamento no Splash
Regras principais em app/components/splashscreen/splashscreen.tsx:
- Sem internet: envia para tela de usuario offline.
- Sem credenciais salvas: envia para tela de login.
- status_cadastro < 5: envia para alerta de candidatura em analise.
- status_cadastro == 5: envia para alerta de candidatura reprovada.
- status_cadastro >= 6: envia para /pages/informacoes/page.

Regra de push:
- Se existir globalThis.__PUSH_DATA__.rota, o splash prioriza essa rota e faz replace.

## 5. Navegacao Principal (Tabs)
Arquivo: app/pages/_layout.tsx

Abas:
- /pages/servico/page
- /pages/historico/page
- /pages/candidaturas/page
- /pages/vagas/page
- /pages/informacoes/page

No layout de tabs tambem acontecem:
- verificacao de permissao obrigatoria de localizacao
- sincronizacao de dados offline com useFiltrarLocalizacoes
- revalidacao periodica de permissao foreground, background e GPS pelo hook obrigatorio de localizacao
- exibicao de overlays de alerta:
  - motorista pre-selecionado
  - motorista selecionado
  - carga liberada

## 6. Estado Global e Eventos
### 6.1 VagasProvider
Arquivo: context/VagasContext.tsx
- Mantem novasVagas e showNotification.
- Usa useAlertVagasDisponiveis para detectar novas vagas em polling.

### 6.2 Push Notification Listener
Arquivo: utils/notificationHandler.ts
- Captura clique da notificacao.
- Armazena payload em globalThis.__PUSH_DATA__.
- Redireciona para splash para reaplicar regras de roteamento.

## 7. Localizacao e Execucao em Background
Arquivo principal: utils/locationTracking.ts

Comportamento:
- Antes de iniciar o rastreamento, o app valida permissao foreground, permissao background e GPS ativo.
- Se faltar permissao, tenta solicitar novamente; se continuar negada, orienta o usuario a abrir as configuracoes.
- A inicializacao do rastreamento e idempotente: chamadas concorrentes ou repetidas nao reiniciam tarefas ja registradas.
- Registra tarefa de localizacao em background com expo-task-manager.
- Registra background fetch para manter rastreamento ativo.
- Para cada servico ativo (exceto status 1, 2 e 6):
  - online: envia localizacao para backend/Sisgen via camada de servico
  - offline: salva no SQLite para sincronizacao posterior
- Quando hooks ou telas pedem inicio de rastreamento, o utilitario retorna um status explicito para indicar se iniciou, ja estava ativo, falhou por permissao ou falhou por GPS.

Arquivos relacionados:
- utils/salvarLocalizacao.ts
- utils/locationService.ts
- utils/sqliteLocalizacao.ts
- hooks/useFiltrarLocalizacoes.ts
- hooks/usePermissaoLocalizacaoObrigatoria.ts
- app/components/bloqueioConexao/bloqueado-localizacao.tsx

## 8. Polling e Atualizacao em Tempo Real
Hooks com polling continuo:
- hooks/useAlertVagasDisponiveis.ts (intervalo de 3s)
- hooks/usePreSelecionado.ts (intervalo de 1s)
- hooks/useSelecionado.ts (intervalo de 1s)
- hooks/useCargaLiberada.ts (intervalo de 1s)

Ao reconectar a internet:
- app/pages/_layout.tsx escuta NetInfo e chama sincronizar() para enviar pendencias locais.

Observacao:
- Esse desenho prioriza reatividade. Em ambiente de pouca bateria ou rede ruim, pode aumentar consumo.

## 9. Persistencia Local
- SecureStore: token, idMotorista, credenciais e chaves de sessao.
- AsyncStorage: cache de servicos e dados auxiliares.
- SQLite: fila offline de localizacao para sincronizacao.

## 10. Ordem Recomendada de Leitura
1. docs/funcionalidades.md
2. docs/apis.md
3. docs/fluxo-operacional.md
