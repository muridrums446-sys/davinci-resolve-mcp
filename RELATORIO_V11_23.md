# Magic Edit Desktop V11.23 — refinamento de tomadas

Atualização cumulativa da V11.22 para a instalação da fábrica:
C:\Magicedit\MagicEdit_Desktop_V11_Atualizacao\MagicEdit_Desktop_V11.

## Comportamento

Identifica três classes de tentativas próximas:

- Perguntas correspondentes, retomadas com introduções como Então/Próximo passo,
  cujo conteúdo anterior está contido na pergunta posterior. Exemplo fornecido:
  riscar "Você ganha dinheiro no mercado?" e "Então como que você ganha?",
  preservando "Próximo passo, como que você ganha dinheiro no mercado?".
- Cadeias de pelo menos duas tentativas curtas de "ao + infinitivo", seguidas de
  versão conjugada com objeto correspondente. O exemplo de Ao comprar preserva
  "então, quando você compra 100 ações por mil reais...". Um fragmento isolado
  continua protegido; a regra literal de duplicatas curtas não foi relaxada.
- Tentativas com reticências, mesma abertura e conteúdo correspondente na retomada.
  Uma tentativa que termina no meio da frase pode corrigir um número; o exemplo
  "Então um exemplo de você comprou uma ação lá a 10 reais e você..." sai inteiro,
  preservando a explicação que começa com 100 reais. A introdução também sai.

A palavra exemplo deixa de ser um bloqueio genérico apenas nessas retomadas
verificadas. Ênfase/didatismo sinalizados permanecem protegidos. O alinhamento
conserva conteúdo substantivo, ordem, multiplicidade e sujeitos internos. Uma
negação alterada ou informação exclusiva faz a sugestão ficar para revisão.
Correção numérica exige interrupção, em vez de comparar dois exemplos completos.
A proteção vale também para o detector anterior de reticências, evitando que
esse caminho volte a cortar uma tentativa que o novo detector preservou.

São regras locais verificáveis de texto/tempos, não treinamento automático de
um modelo. Comparação semântica genérica e palavras omitidas na transcrição
continuam dependendo de investigação. Groq/Whisper, caches, VAD/energia, modelo
Silero, MP4 final, seleção leve, FCPXML e atalhos não foram substituídos.
O servidor apenas permite servir o novo módulo JS na lista fechada de assets.

A janela é de até 12 s entre fim da tentativa e início da retomada; cada trecho
novo descartado é limitado a 120 palavras/45 s. No JSON, os novos motivos e
âncoras da versão preservada ficam auditáveis; autoEditVersion passa a 5.
Schema continua 1. Abrir projeto preserva escolhas salvas e não reedita.
Para aplicar no projeto existente: Ferramentas > Editar automaticamente este
projeto. Reedição acrescenta cortes, sem retranscrever. Botão direito restaura;
Ctrl+Z desfaz. O padrão de pausa continua 0,9 s, com preferências preservadas.

## Evidências

- Node: 111 testes aprovados, nenhuma falha. Dez novos testes cobrem os três
  exemplos com palavras/tempos do JSON original, perguntas com introduções
  diferentes, proteção de valores diferentes em frases completas, resposta
  legítima a pergunta, didatismo, negação, informação exclusiva, sujeitos
  internos, retomada distante e abertura de JSON sem aplicar novos cortes.
- Python: 87 reportados, 80 aprovados, 7 ignorados por fixtures V11.10–V11.16
  ausentes no pacote original. Nenhuma falha. Inclui HTTP 200 do novo módulo,
  Groq/modelo/exportações e proteções de backup/rollback/Node opcional.
- Chromium/HTTP/FFmpeg reais: oito verificações das retomadas, com os três
  casos originais rebaseados para vídeo sintético. Abertura sem reeditar,
  aplicação explícita, primeira tentativa riscada, última ativa, corte manual
  conservado, restauração pelo direito, Ctrl+Z, exportação FCPXML com referência
  ao bruto completo e preservação dos arquivos de entrada. Sem erros JS.
- Outras 16 verificações de regressão da interface e dez da seleção leve passaram.
  MP4 final e FCPXML concordaram em 13,4 s no cenário sintético; seleção inclui
  partes riscadas e não sobrescreve saídas, com áudio sincronizado.
  Janelas nativas e respostas Groq simuladas; sem chamadas reais à API.
- Auditoria do JSON original de 6848 palavras: seis novas marcações locais,
  exatamente nos três grupos indicados (três fragmentos Ao comprar, duas
  perguntas e uma tentativa de exemplo). Não surgiram outras marcações desse
  novo detector nesse projeto. Gling continua referência, sem copiar seus cortes.
- Revisão independente identificou dois riscos de perda de sentido (negação/
  adjetivo e sujeito interno). Foram reproduzidos por testes falhando e corrigidos
  com alinhamento que conserva conteúdo/ordem, antes de aprovar o pacote.
- Atualizador testado em Linux sem Node e com backup integral por SHA-256,
  preservando arquivos do usuário e pastas irmãs. Foram conferidos 114 arquivos
  em cada backup e instalados 117 arquivos da lista fechada. O cenário anterior
  usa o pacote V11.22; o cenário 0.11.14 usa esse mesmo runtime com marcador
  antigo, portanto não representa uma instalação V11.14 real. A lista e manifesto
  dos oito módulos JS acompanham o pacote. Node é opcional; Python, Groq/NumPy/
  ONNX Runtime, modelo Silero e FFmpeg/FFprobe continuam verificados.

Modelo Silero preservado, SHA-256:
1a153a22f4509e292a94e67d6f9b85e8deb25b4988682b7e174c65279d8788e3.
Não houve alteração em Motion, src irmã, Remotion ou plugin DaVinci.

## MP4 recebido e limites da validação

O arquivo recebido tem 181458 bytes e duração de 13,233 s, H.264 854×480/30 fps,
AAC mono 16 kHz. A leitura automática local de diagnóstico encontrou outra
passagem: "Então como você ganha dinheiro com o mercado...", seguida de
"Basicamente...". Não foi usado como prova dos pontos de corte de Ao comprar
ou da troca de 10 por 100. Os testes desses casos usam os textos/tempos que já
existiam no JSON original, preservado, e vídeo sintético para a interface.

Foi usado Whisper base/ONNX em ambiente separado apenas para diagnóstico do
MP4; o reconhecimento também pode omitir/errar palavras. Esse modelo e essa
biblioteca não entram no app nem no ZIP. O arquivo recebido não é publicado
no GitHub. Os modelos Groq/Silero do app não foram trocados.

Não houve acesso ao Windows, backup/instalação reais ou teste real no DaVinci.
Os pontos exatos de áudio dos casos marcados ainda precisam dos trechos leves
correspondentes e de conferência no original. O novo detector não garante que
toda reformulação será reconhecida: conserva casos incertos para revisão.
Evidências históricas V11.17/18 e interface-selecao-v11-22.json são mantidas;
esta última contém a revalidação atual do recurso introduzido na V11.22.
