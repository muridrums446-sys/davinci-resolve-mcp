# Magic Edit Desktop V11.20

Atualização cumulativa da V11.19: clique direito na timeline, FCPXML para DaVinci
e correção do Espaço. Detecção automática, Groq, projetos e mídia original mantêm
o comportamento da V11.19. Os pacotes anteriores foram preservados.

## Resultado

- Arraste X-Y na onda, régua ou miniaturas e clique direito: corta a seleção,
  risca o texto atingido e remove o intervalo da prévia/exportação. Funciona
  arrastando ao contrário ou clicando fora da seleção. A seleção tem prioridade
  sobre restaurar cortes antigos sob o mouse. Sem seleção, direito sobre corte
  restaura. Delete, botão Cortar seleção e Ctrl+Z permanecem.
- Espaço inicia/pausa após clicar em botões, rolar a timeline e com foco no vídeo.
  A captura do teclado ocorre antes do controle nativo, evitando a alternância
  duplicada do Chromium. Segurar Espaço não alterna repetidamente. Pausar durante
  uma busca para saltar corte cancela a retomada e restaura o mute anterior.
  Digitação em campos e Enter nos botões continuam disponíveis.
- Exportar DaVinci salva FCPXML 1.9 real, com recursos/asset/media-rep e
  asset-clips separados. Áudio e vídeo pertencem ao mesmo clipe. Entradas na
  fonte, duração e posições usam frações exatas de frames, incluindo
  30000/1001 e 24000/1001. Trechos de um frame permanecem. Não é FCP7 renomeado.
- Por padrão, aponta ao vídeo bruto completo existente. Preserva qualidade,
  sobras e referência à fonte para ajustes de cortes no Resolve. Não cria MP4
  nem altera o original. Escapa URI Windows/UNC, acentos e caracteres reservados.
  O arquivo precisa continuar na pasta indicada pelo FCPXML.
- Em Ferramentas > Exportação para DaVinci, a opção de compatibilidade cria um
  master COMPLETO H.264/AAC ao lado do .fcpxml. Mantém sobras; não usa o MP4
  concatenado da edição. CRF 16, taxa constante e áudio estéreo 48 kHz.
  É opcional e pode demorar/ocupar espaço. Valida a mídia antes de publicar
  a timeline, recusa arquivos existentes e limpa saídas parciais em falhas.
  Mantenha nome.media.mp4 junto do FCPXML.
- Exportar MP4 final continua separado; o XML antigo FCP7 fica em Ferramentas.

## Referência Gling fornecida nesta conversa

O usuário confirmou que o novo exemplo abre no DaVinci. É FCPXML 1.9,
1920×1080, 30 fps, com 99 clipes e referência ao MKV bruto completo de
1866,701 s. A montagem de referência dura 1124,7 s.

Uma fixture do exportador reproduziu a estrutura com a mesma URI da mídia,
as mesmas 99 durações e posições na timeline. Entradas alinhadas aos frames:
diferença máxima de 1/60 s em relação aos milissegundos do exemplo. Isso verifica
a estrutura do exportador, sem importar/copiar os cortes do Gling para projetos
do aplicativo. O arquivo original foi apenas lido. Veja fcpxml-referencia.json.

A captura anterior mostra mídia não localizada após ler o XML. FCPXML também
precisa do vídeo: se mudar de pasta, será necessário localizá-lo no Resolve.
A estrutura nova segue o formato confirmado pelo usuário, mas não houve
importação real no Resolve nesta máquina.

## Validação executada na nuvem

- Node: npm test, 77 aprovados, nenhuma falha.
- Python: unittest discover, 72 reportados, 65 aprovados e 7 ignorados por
  fixtures dos atualizadores V11.10–V11.16 ausentes no pacote original. Não são
  testes aprovados. A fixture V11.17 continua presente e testada.
- Atualizador: backup integral, corrupção, rollback, proteção de pastas e
  arquivos do usuário. Testes antigos V11.18/V11.19 mantidos e adaptados à
  versão corrente para não deixar expectativas desatualizadas na instalação.
- FCPXML: frações, um frame, URI Windows/UNC, preservação da fonte, sobras,
  ausência de sobrescrita e limpeza após falhas de verificação/publicação.
  FFmpeg real converteu MKV sintético para H.264/yuv420p/AAC com todos os
  100 frames e áudio/vídeo sincronizados.
- Chromium real + servidor HTTP real + FFmpeg real: 14 verificações, incluindo
  seis arrastos em duas direções, direito fora da seleção, Ctrl+Z, texto riscado,
  restauração, Espaço após botões e no vídeo, repetição da tecla, pausa durante
  salto, projetos antigos, rolagem com 6.848 palavras, FCPXML com original e com
  master de 400 frames, e MP4 único. Nenhum erro JavaScript. MP4 final e FCPXML
  representaram a mesma duração sintética de 13,4 s.
- CLI real do atualizador: instalação de teste 0.11.19 -> 0.11.20, imports e
  verificações reais antes/depois. Backup de 100 arquivos conferido por hashes;
  vídeo sintético, JSON, configuração e pastas irmãs protegidas intactos.
  Suítes executadas novamente no destino atualizado: Node 77 aprovados;
  Python 65 aprovados e os mesmos 7 históricos ignorados. Isso foi no Linux,
  não executou BAT nem acessou a instalação Windows do usuário.
- Revisão independente do código: nenhum problema crítico/importante identificado.
- Respostas Groq e seletores de arquivo simulados no teste de interface.
  Nenhuma chave real nem chamada real à API foi usada.

Comandos, a partir da pasta do pacote:

```
npm test
python -m unittest discover -s tests -p "test_*.py"
python validacao/interface_real.py --output PASTA_NOVA --chromium CAMINHO_CHROMIUM
```

O teste de interface requer Playwright para Python, Chromium e FFmpeg/FFprobe;
não são dependências adicionais para executar o editor normalmente.

## Instalação e limites

Feche o Magic Edit e o servidor. Extraia fora de C:\MagicEdit\Desktop_V10 e
execute ATUALIZAR_V11_20.bat. O atualizador informa a versão instalada e valida
Python/Node/imports/FFmpeg/modelo antes de alterar código. Faz backup integral,
compara SHA-256 de cada arquivo e conserva manifesto. Copia somente uma lista
fechada de arquivos Desktop e revalida. Falha provoca rollback do código.
Abra C:\MagicEdit\Desktop_V10\INICIAR_MAGIC_EDIT.bat e confira V11.20.

JSON, vídeo original e configurações são preservados. Motion, C:\MagicEdit\src,
Remotion e plugin DaVinci não são alterados. Evidências antigas de comparação
editorial e responsividade V11.18 continuam identificadas nos arquivos legados;
não representam nova medição editorial do vídeo completo.

Não houve acesso ao Windows do usuário, ao vídeo bruto completo nem ao DaVinci.
Não foram validados execução dos BAT, importação real no Resolve, desempenho
no computador do usuário ou qualidade editorial de chamadas reais à Groq.
O relato sobre o Gling é referência de compatibilidade, não uma importação
feita por nós. Capturas e logs da nuvem estão em evidencias/.
