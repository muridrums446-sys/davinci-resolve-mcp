# Magic Edit Desktop V11.19 — repeticoes e selecao direta

Atualizacao cumulativa sobre a V11.18. A V11.18 original e seu ZIP foram preservados.
O usuario confirmou que instalou a V11.18 no Windows; esta V11.19 foi testada na nuvem Linux,
sem acesso direto ao computador ou aos videos originais.

## Alteracoes solicitadas

1. Repeticoes aceitas pelo detector passam a cortes riscados automaticamente, inclusive frases
   curtas e palavras comuns repetidas. O detector considera frases de ate 48 palavras,
   preserva a ultima tomada em sequencias de tres ou mais versoes e reconhece indicacoes
   de erro entre tomadas iguais. Tentativas interrompidas reconhecidas tambem podem ser
   riscadas. O clique direito restaura e Ctrl+Z desfaz. Nao existe garantia editorial:
   repeticoes intencionais nao sinalizadas podem exigir restauracao. Negacoes, intensificadores
   e sinais didaticos explicitos continuam protegidos. Reformulacoes ambiguas com mudanca de
   informacao ficam para revisao. As sugestoes nao aplicadas nao usam mais fundo amarelo.
2. Arrastar diretamente na onda, regua ou miniaturas seleciona X-Y, sem ativar um botao.
   Arrastar ao contrario normaliza os limites. Delete remove o intervalo da previa/exportacoes,
   mostra o corte na timeline e risca as palavras atingidas. Sem palavras, surge um marcador
   temporal restauravel. Ctrl+Z restaura. Clique simples posiciona; C e clique em segmento
   dividido continuam funcionando. Cancelar o arrasto nao cria corte.

Projetos antigos nao sao recortados automaticamente ao abrir: isso preserva restauracoes.
Para aplicar a nova deteccao em JSON existente, use Ferramentas > Editar automaticamente
este projeto. Nao e preciso retranscrever. Os campos schema 1, Groq, VAD, autosave,
restauracao, MP4 e FCP XML permanecem.

## Verificacao

- Node: npm test — 77 aprovados, nenhuma falha.
- Python: unittest discover — 60 reportados, 53 aprovados e 7 ignorados por atualizadores
  historicos V11.10 a V11.16 ausentes do pacote original. Nao sao testes aprovados.
- Testes novos cobrem frase curta, palavra repetida, frase longa, tres tomadas, erro entre
  versoes, protecao de enfase/negacao, numeros diferentes e preservacao de restauracoes.
- Teste de eventos da aplicacao cobre arrasto normal/inverso, tres superficies, clique simples,
  cancelamento, Delete, palavras riscadas, persistencia do intervalo e Ctrl+Z.
- Chromium real + servidor real + FFmpeg real: importacao, aplicacao automatica, reanalise de
  JSON sem retranscrever, restauracao, saltos, exportacoes e 6.848 palavras. Seis arrastos
  reais (tres faixas, nos dois sentidos) confirmaram Delete/risco e Ctrl+Z. Um corte sem texto
  foi restaurado pelo marcador. Nenhum erro JavaScript. Respostas Groq simuladas, sem API real.
- MP4 unico e XML representaram a mesma duracao sintetica: 13,4 s. Estrutura de audio/video
  alinhada. Isso nao equivale a importar o XML no DaVinci.
- Na transcricao longa fornecida (6.848 palavras), a analise local levou cerca de 431 ms nesta
  maquina e selecionou 113 palavras (aproximadamente 41,408 s antes de eventuais cortes de
  silencio/contexto). E apenas uma medicao de candidatos, nao uma validacao por escuta.
  A comparacao Gling da V11.18 permanece referencia com ajustes manuais, sem copiar seus cortes.

Evidencias atuais: interface.json, testes-node.txt, testes-python.txt e capturas em evidencias/.
O modelo real Groq, a qualidade editorial no video original, o desempenho no i7-3770,
a execucao dos BAT no Windows e a importacao real no DaVinci nao foram testados nesta sessao.

## Atualizar

Feche o Magic Edit e o servidor. Extraia fora de C:\MagicEdit\Desktop_V10 e execute
ATUALIZAR_V11_19.bat. Ele confere a versao instalada e faz backup integral, com hashes,
antes de atualizar a pasta definitiva. Mantem JSON, videos e configuracoes do usuario.
Motion, C:\MagicEdit\src, Remotion e plugin DaVinci nao sao alterados. Guarde o backup.
Abra INICIAR_MAGIC_EDIT.bat na pasta definitiva e confira o cabecalho V11.19.
