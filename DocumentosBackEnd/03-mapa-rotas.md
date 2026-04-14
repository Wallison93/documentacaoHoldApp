# 03 - Mapa De Rotas

## Prefixos montados no servidor

Definidos em `index.js`:

- `/usuarios`
- `/localizacao`
- `/cadastro_motorista`
- `/servicos`
- `/servicos_por_motorista`
- `/candidatura`
- `/status`
- `/lookup_status`
- `/lookup_enderecos`
- `/cpf`
- `/dados_veiculo`
- `/dados_motorista`
- `/notificacao_motorista`
- `/diario_bordo`
- `/recuperar_senha`
- `/upload_foto`
- `/uploadProcesso`
- `/uploadProcessoLote`
- `/ocrGoogleVision`
- `/geminiLerVeiculos`
- `/geminiComprovanteEntrega`
- `/geminiLerContratoAssinado`
- `/geminiExtrairAntt`
- `/Candidaturas`
- `/Historico`
- `/Servicos`
- `/Informacoes`
- `/Enderecos`
- `/Vagas`
- `/Veiculos`
- `/PreSelecionado`
- `/Selecionado`
- `/CargaLiberada`
- `/ArquivosMotorista`
- `/ArquivosProcesso`
- `/Estados_cidades`
- `/Manutencao`
- `/UpdateStatus`
- `/RecusarServico`
- `/StatusNotificacao`
- `/AttCadastro`
- `/AttManutencao`
- `/Candidatar`
- `/Cadastro`
- `/CadastroVeiculo`
- `/InsertLocation`
- `/InsertLocation_sisgen`
- `/InsertManutencao`
- `/deleteCandidatura`
- `/deleteTokenNotification`
- `/EnviarNotificacao`
- `/ProxySisgen`

## Rotas com autenticacao JWT (amostra)

Arquivos que aplicam `authenticateToken` diretamente nas rotas:

- `routes/inserir/localizacao/localizacao.js`
- `routes/inserir/localizacao/localizacao_sisgen.js`
- `routes/inserir/candidatar/candidatar.js`
- `routes/inserir/manutencao/manutencao.js`
- `routes/atualizar/status_servico/status_servico.js`
- `routes/atualizar/status_candidaturas/status_candidaturas.js`
- `routes/atualizar/recusar_servico/recusar_servico.js`
- `routes/atualizar/manutencao/manutencao.js`
- `routes/buscas/candidaturas/candidaturas.js`
- `routes/buscas/historico/historico.js`
- `routes/buscas/servicos/servicos.js`
- `routes/buscas/informacaoes/informacoes.js`
- `routes/buscas/enderecos/enderecos.js`
- `routes/buscas/vagas/vagas.js`
- `routes/buscas/veiculos/veiculos.js`
- `routes/buscas/preselecionado/preselecionado.js`
- `routes/buscas/selecionado/selecionado.js`
- `routes/buscas/cargaLiberada/cargaLiberada.js`
- `routes/deletes/candidaturas/candidaturas.js`
- `routes/deletes/tokenNotification/tokenNotification.js`

## Observacao de mapeamento

- O projeto possui arquivos com trechos antigos comentados e alguns handlers repetidos no mesmo arquivo.
- Para manutencao futura, recomenda-se padronizar:
  - nome de prefixos (minusculo)
  - verbo e recurso (REST)
  - remocao de blocos duplicados/comentados
