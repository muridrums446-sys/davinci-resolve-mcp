# Magic Edit Desktop V11.27 — diagnostico de conexao Gemini

A V11.26 mostrava a mesma mensagem para timeout, erro DNS, HTTPS/certificado,
conexao interrompida e outros erros de rede. A V11.27 distingue essas categorias
por tipo de excecao real, com codigo fixo seguro, tempo decorrido da requisicao
que falhou e etapa do timeout. HTTP503 continua identificado como HTTP503.

Nenhuma chave, corpo bruto do provedor, URL privada, caminho local ou mensagem
bruta do sistema e incluida nesses avisos. Chave continua somente na sessao.
Timeouts mantidos:20s na consulta de modelos,120s por operacao de analise.
Sem retentativa automatica, troca de modelo, mudanca de payload/prompt, cortes,
silencios, transcricao, exportacao, salvamento ou faturamento.

## Verificacao

- RED:10 subcasos falharam com o aviso generico antigo; GREEN:23 testes Gemini.
- Node:118 passam; Python:117 totais,110 passam,7 skips por fixtures historicas
  V11.10–16 ausentes. Nenhuma falha.
- Chromium/HTTP/FFmpeg reais, transporte Google simulado:14 verificacoes incluindo
  timeout,HTTP503,conexao interrompida no aviso final; cortes preservados, sem chave
  no aviso/projeto e sem corte parcial. Listagem de modelos permanece coberta.
- O pacote e extraido e verificado; atualizador CLI exercitado na nuvem sem Node
  em casa V11.26 e fabrica V11.24/V11.26, com pre/postflight reais, backup integral
  conferido por hashes e preservacao de midia/projetos/configuracoes ficticias,
  pastas protegidas e backups anteriores.

## Instalacao

Extraia o ZIP em Downloads, fora da instalacao. Salve o projeto e feche aplicativo
e servidor antes de atualizar. Na FABRICA execute ATUALIZAR_V11_27.bat; destino:
C:\Magicedit\MagicEdit_Desktop_V11_Atualizacao\MagicEdit_Desktop_V11
Na CASA execute ATUALIZAR_V11_27_CASA.bat; destino:C:\MagicEdit\Desktop_V10.
Backup integral verificado antes da troca. Abra INICIAR_MAGIC_EDIT.bat na pasta
instalada apos sucesso; Ctrl+F5; confira V11.27.

## Limites

Esta versao melhora o diagnostico. A causa da falha real do usuario permanece
pendente de um teste no PC dele. Nao foi testada uma chave Gemini real, cota,
qualidade editorial, rede da empresa, BAT em Windows ou importacao no DaVinci.
Dashboard agregado com tokens nao comprova entrega/conclusao da tentativa atual.
Nao e necessario ativar faturamento para instalar esta atualizacao.
