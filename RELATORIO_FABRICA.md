# Magic Edit V11.21 — instalador para a fábrica

Correção do destino do atualizador para:
`C:\Magicedit\MagicEdit_Desktop_V11_Atualizacao\MagicEdit_Desktop_V11`.

A captura mostra essa pasta dentro de MagicEdit_Desktop_V11_Atualizacao.
O instalador confere arquivos identificadores e versão no computador antes de
substituir código. Não cria uma instalação vazia se o caminho não existir.
O aplicativo continua na versão 0.11.21; esta revisão altera apenas o instalador,
a documentação e os testes. O código de edição, exportação, Groq e o modelo
Silero são idênticos ao pacote V11.21 anterior.

## Instalar

1. Feche o Magic Edit e o servidor.
2. Extraia o ZIP em Downloads, fora da pasta instalada.
3. Dentro de Magic_Edit_Desktop_V11_21_Fabrica, execute ATUALIZAR_V11_21.bat.
4. Confira a mensagem de conclusão. O backup integral fica ao lado da instalação,
   em _BACKUP_MagicEdit_Desktop_V11_preV11_21_<data>, com manifesto SHA-256.
5. Abra INICIAR_MAGIC_EDIT.bat na pasta instalada indicada acima. Mantenha o backup.

Não mova a instalação nem copie os arquivos manualmente por cima dela.
Se o atualizador interromper, envie a mensagem completa; não apague os backups.

## Verificação desta revisão na nuvem Linux

- Node: 94 testes aprovados, nenhuma falha.
- Python: 84 testes reportados, 77 aprovados, 7 ignorados porque as fixtures
  históricas V11.10–V11.16 não acompanham o pacote original. Nenhuma falha.
- Oito testes da pasta da fábrica, incluindo backup integral, preservação de
  vídeo/projeto/configuração, backups antigos e pastas irmãs, bloqueio de
  destinos protegidos e rollback após falha de cópia ou verificação final.
- Atualização pela CLI em uma pasta com a mesma estrutura da captura: validações
  reais antes/depois, backup de 107 arquivos conferido por SHA-256, instalação
  de 105 arquivos da lista fechada, sentinelas preservadas. Instalação simulada
  com runtime V11.21 e marcador 0.11.14, mídia/projeto/configuração fictícios;
  isso verifica o mecanismo, não o conteúdo de uma instalação real V11.14.
- Revisão independente não identificou defeitos concretos na correção.
- Diferença contra V11.21 restrita a update_desktop.py, ATUALIZAR_V11_21.bat,
  LEIA_PRIMEIRO.txt, RELATORIO_VALIDACAO.md e tests/test_upgrade_factory.py.
- O destino da fábrica é passado explicitamente e entre aspas pelo BAT.
  O padrão da CLI permanece Desktop_V10 por compatibilidade. São aceitos os
  nomes Desktop_V10 e MagicEdit_Desktop_V11, com identificação e versão válidas;
  destinos dentro de src, Motion, Remotion e _BACKUP_ são recusados.

Não houve acesso ao Windows da fábrica, execução do BAT no Windows, backup
na máquina real, abertura real da interface nessa máquina ou teste no DaVinci.
Essas confirmações dependem de executar o pacote no computador. Os resultados
anteriores da interface na nuvem constam do relatório V11.21 e não foram refeitos
nesta revisão do instalador. A branch principal e o plugin DaVinci não mudam.
