# Magic Edit Desktop V11.21

Atualização cumulativa da V11.20. Foram implementados os dois ajustes autorizados:
pausas acima de 0,7 segundo e alternância cortar/restaurar a seleção da timeline.
O usuário aprovou depois a regra de repetição com três ou mais palavras em
tentativas próximas, mantendo a última. Essa regra também está implementada.

## Comportamento

O limite padrão de pausa é 0,7 segundo. Uma pausa exatamente nesse limite ou
menor fica mantida. Pausas maiores são cortadas na edição automática quando
energia e Silero confirmam o intervalo disponível. Palavras e voz continuam
protegidas. A duração mínima é medida antes das margens, inclusive os 0,22 s
que o Silero acrescenta em cada borda. As margens de voz não são removidas.
O valor aparece em Ferramentas, acompanha JSON/autosave e altera somente a prévia
até aplicar o novo ritmo num projeto aberto. Abrir JSON antigo preserva seus cortes.

Direito alterna a seleção entre cortada e restaurada, nas três faixas: onda,
régua e miniaturas. A seleção continua visível; o botão e a indicação mostram
se o próximo clique corta ou restaura. Seleção parcialmente cortada corta o
conjunto; seleção totalmente cortada restaura somente o intervalo escolhido.
Partes de um corte maior fora da seleção ficam preservadas. A restauração
materializa as sobras dos cortes efetivos em extraCuts, mantendo schema 1.
Palavra parcialmente cortada continua riscada enquanto parte dela estiver removida.
Clique esquerdo/Limpar seleção limpa a seleção; Ctrl+Z e Delete permanecem.
Sem seleção, direito sobre um corte restaura o bloco como na versão anterior.

FCPXML 1.9, referências ao bruto completo, opção de master MP4, MP4 final,
atalho Espaço e integração Groq permanecem. Modelo ONNX e licença preservados.
Nenhuma alteração em Motion, src irmã, Remotion ou plugin DaVinci.

## Repetições aprovadas

Frases repetidas exigem pelo menos três palavras consecutivas iguais na mesma
ordem. Normaliza maiúsculas e pontuação. Mantém a última tentativa de uma
sequência; repetições de uma ou duas palavras ficam como sugestões, sem autocorte.
O exemplo do usuário, "no vídeo de hoje — no vídeo de hoje", remove a primeira.
Falas distantes e começos comuns de frases com continuações diferentes ficam
preservados. Ênfase e repetições didáticas sinalizadas continuam protegidas.

As duplicatas consecutivas usam a proximidade já existente: até 4 s de intervalo,
com janela total de 90 s para tomadas longas. Com indicação explícita de erro ou
validação Groq, a retomada precisa estar em até 12 s. Tentativa interrompida
exige três palavras correspondentes; comandos explícitos de erro mantêm o
tratamento anterior. A primeira tomada precisa corresponder, não só ter um
começo comum com pausa. Frases inteiras têm prioridade sobre sugestões curtas
internas. Casos incertos continuam para revisão, e o clique direito restaura.

A regra também vale para duplicatas da Groq. O cache textual foi versionado para
não reutilizar decisões automáticas anteriores; transcrição/cache de áudio,
SDK, chaves e mecanismo de cota foram preservados. Projetos salvos continuam
abrindo com os cortes que já tinham; restaurar cortes antigos de uma/duas
palavras continua sendo decisão do usuário, sem modificar seu JSON original.

## Validação

- Node: 94 testes aprovados. Inclui limiares abaixo/no/acima de 0,7 s,
  limite ajustável, margens reais de Silero, voz baixa sem legenda,
  palavras fora do VAD, energia sustentada, áudio incompleto, intensidade,
  alternância temporal, restauração parcial e persistência de cortes externos.
  Novos casos de repetição cobrem o exemplo do usuário, três palavras exatas,
  palavras funcionais, tomada com repetição interna, erro/retomada, distância
  e frases diferentes com começo comum, inclusive com pausa.
- Python: 76 reportados, 69 aprovados e 7 ignorados por fixtures dos atualizadores
  V11.10–V11.16 ausentes no pacote original. Os sete não são testes aprovados.
- FFmpeg e Silero reais processaram uma fixture sintética com pausa de 0,8 s
  e outra de 0,6 s. Somente a maior passou ao corte. As palavras foram fornecidas
  pela fixture; tons não equivalem a validar reconhecimento de voz humana.
  Testes de fronteira usam intervalos com a mesma margem do VAD de produção.
- Chromium real, servidor e FFmpeg reais: seis seleções nos dois sentidos e
  nas três faixas; cada uma cortada/restaurada/cortada pelo mesmo clique direito.
  Ctrl+Z, palavras riscadas/ativas, silêncio sem texto, projetos antigos,
  Espaço, rolagem de 6.848 palavras e exportações permaneceram funcionais.
  A regra de três palavras também foi aplicada e restaurada na interface real.
  Nenhum erro JavaScript. MP4 final e FCPXML: 13,4 s no cenário sintético.
- Atualizador CLI real: 0.11.20 -> 0.11.21 em instalação de teste na nuvem.
  Backup integral de 104 arquivos conferido por hashes, incluindo vídeo sintético,
  projeto e configuração. Pastas irmãs protegidas intactas. Verificações antes
  e depois executadas de verdade. No destino atualizado: 94 testes Node e
  69 Python aprovados, com os mesmos 7 históricos ignorados. Nenhum BAT Windows.
- O seletor nativo e as respostas Groq foram simulados nesse teste da interface.
  Nenhuma chamada real à Groq nem chave real foi usada.
- Revisão independente encontrou o problema da margem Silero na primeira versão
  do cálculo. Foi reproduzido em teste que falhou e corrigido. Revisor confirmou
  a correção. Na regra de repetições, apontou dois casos adicionais (sugestão
  curta escondendo tomada completa e pausa autorizando começo comum); ambos
  foram reproduzidos, corrigidos e reconferidos sem problemas importantes. Verificou também
  30 mil casos gerados de restauração de intervalos sem perda de cortes externos.

Evidências em interface.json, testes-node.txt, testes-python.txt e capturas.
A comparação estrutural FCPXML e a responsividade de versões anteriores continuam
identificadas nos arquivos legados; não são uma importação nova no DaVinci.

## Instalação

Feche o Magic Edit e o servidor. Extraia fora de C:\MagicEdit\Desktop_V10 e
execute ATUALIZAR_V11_21.bat. O atualizador informa a versão instalada e verifica
backup integral com SHA-256 antes de substituir código, com rollback em falha.
Depois abra C:\MagicEdit\Desktop_V10\INICIAR_MAGIC_EDIT.bat e confira V11.21.
Mantenha o backup. Projetos, vídeo original e configurações são preservados.

Não houve acesso ao Windows do usuário ou ao vídeo bruto completo. Execução dos
BAT, escuta editorial do original, importação real no DaVinci e chamadas reais
à Groq não foram validadas nesta nuvem Linux. Não se promete detectar todo silêncio
nem garantir transcrição completa quando os modelos deixam de reconhecer voz.
