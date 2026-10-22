# Magic Edit Desktop 0.11.18

Atualização preparada a partir do pacote V11.17 fornecido pelo usuário. O objetivo é aplicar a edição bruta automaticamente e finalizar no DaVinci, preservando o original e permitindo revisão e restauração.

**Esta entrega é um pacote instalável. Não foi instalado no computador do usuário.** A sessão só teve acesso ao Linux na nuvem. Não foi possível conferir a versão efetivamente instalada em `C:\MagicEdit\Desktop_V10`, fazer seu backup, abrir os vídeos originais ou importar no DaVinci. O atualizador confere a versão e faz o backup quando executado no Windows. Não foi modificado o repositório/plugin DaVinci nem qualquer pasta Windows, Motion ou Remotion.

## Mudanças

- Importação aplica a edição local e, com “Edição completa com Groq” ligada, executa também a análise textual no mesmo fluxo. A opção informa uso da cota. Não há nova API ou chave no pacote.
- Duplicatas completas com evidência local são cortadas mantendo a tomada posterior. Repetições curtas e sinais didáticos ficam. A análise Groq classifica duplicata, recomeço e fala lateral; aplica candidatos com confiança declarada pelo modelo >=0,97 e validações de índices, duração e categoria. Duplicatas de IA também exigem uma tomada posterior literalmente correspondente, protegendo mudanças de números. Confiança declarada não é precisão medida.
- Silêncio continua exigindo VAD e energia baixa, protegendo voz sem legenda. Ruídos breves podem sair junto com uma pausa confirmada. Tosse marcada como voz e sons ambíguos continuam para revisão: não foi criada uma classificação acústica comprovada de toda tosse/ruído.
- Falha na etapa de contexto mantém a edição local, informa pendência e permite tentar novamente. “Só sugestões” continua disponível. Motivos e decisões aparecem na interface e são salvos como campos opcionais no JSON/autosave; Ctrl+Z e restauração permanecem.
- Abrir projeto antigo não acrescenta cortes nem chama transcrição/IA. As listas de palavras, exclusões e cortes salvos permanecem. O formato segue schema 1. A nova proteção de bordas pode ajustar a duração efetiva de uma exclusão para preservar uma palavra vizinha; os JSON originais não são regravados pelo instalador.
- Palavras do Whisper com duração zero não desaparecem: conservam o texto, com tempo estimado identificado no tooltip. A junção continua preservando ordem e repetições dentro do bloco. **Isso não recupera palavras que a própria API não devolveu**, nem as já ausentes de um JSON antigo.
- Cliques nos espaços entre palavras usam a palavra próxima na mesma linha; seleção nativa permanece. A prévia deixa de acrescentar 30 ms ao salto de corte. Palavras vizinhas sobrepostas recebem proteção nos cortes textuais.
- Exportações preservam trechos de um frame. O FFprobe usa taxa nominal padrão quando praticamente igual à média do contêiner, evitando rejeitar metadados como `746600/24881` quando o arquivo confirma nominal `30/1`. Não há garantia de conform de vídeo VFR sem teste no DaVinci.
- Cabeçalho e exportações foram ajustados para telas de notebook. Mantidos forma de onda, miniaturas, atalhos, velocidades, autosave, posição, projetos recentes, integração Groq, XML e MP4.

## Comparação dos projetos e Gling

Comparação por tempos da fonte, usando a definição de cortes V11.17 para reproduzir os números anteriores. O XML Gling contém ajustes manuais e não foi tratado como verdade absoluta nem importado como decisões do Magic Edit.

| Janela original 00:00–08:22 | Tempo removido |
|---|---:|
| Magic antes da edição manual | 13,840 s |
| Magic depois da edição manual | 146,627 s |
| Gling com ajustes manuais | 171,433 s |
| Interseção Magic editado / Gling | 113,973 s |
| Apenas Gling | 57,461 s |
| Apenas Magic editado | 32,655 s |

Os dois JSON longos têm as mesmas 6.848 palavras, inclusive as mesmas omissões potenciais; não são duas transcrições independentes. O XML tem 208 asset-clips e remove 460,801 s no vídeo completo de 2.447,934 s. Há 36 intervalos removidos nos primeiros 502 s, quatro maiores de dez segundos. As divergências em torno de 02:11–02:30 e 03:24–03:47 exigem decisão editorial/escuta, não cópia de cortes.

Aplicado isoladamente à transcrição longa, o detector local novo encontra 62 sugestões textuais e seleciona 26 palavras de duplicatas (aproximadamente 7,034 s no vídeo todo; 2,276 s na janela inicial). Isso **não demonstra resultado equivalente ao Gling**: o ganho em tomadas longas/falas fora do contexto depende da etapa de IA, cuja qualidade real não foi medida aqui. Os cortes Gling não foram usados como treinamento nem como lista automática de exclusões.

Reproduzir: `python validacao/comparar_amostras.py CAMINHO_DA_PASTA_AMOSTRAS`. Números em `evidencias/comparacao.json`.

## Verificação executada

Ambiente: Python 3.12, Node 24, FFmpeg 7.1.5, Chromium 154, Linux. Bibliotecas do ambiente de teste: Groq 1.7.0, NumPy 2.5.4, ONNX Runtime 1.31.0. São versões observadas, não uma confirmação de compatibilidade com todo Python/Windows.

- Node: `npm test`, **68 aprovados**, nenhuma falha.
- Python: `python -m unittest discover -s tests -p 'test_*.py'`, **60 testes reportados: 53 aprovados e 7 ignorados**, nenhuma falha na execução final. Os sete ignorados são `test_upgrade_v11_10` até `test_upgrade_v11_16`: os atualizadores históricos não vieram no anexo. A ausência agora é explicitamente reportada, em vez de falha de importação. As respectivas asserções foram mantidas e executarão se as versões históricas forem fornecidas. O atualizador V11.17 original foi preservado como fixture e seu teste executou.
- Na linha de base do pacote: 62 Node passaram; a descoberta Python terminou com 9 erros, oito por atualizadores não extraídos/ausentes e um por ONNX Runtime ausente. Instalamos as dependências, extraímos o V11.17 fornecido e distinguimos os sete fixtures restantes. Não foram inventadas versões históricas para forçar aprovação.
- Regressões exercitaram: JSON antigo sem novos cortes, proteção de ênfase, duplicata completa, palavras vizinhas sobrepostas, um frame mantido, palavra de duração zero, repetição entre blocos, categorias/índices/confiança inválidos da IA, taxa nominal de FPS, clique nos espaços, backup corrompido, falha de cópia, falha após instalação e destino Motion proibido.

### Interface real no navegador

`validacao/interface_real.py` abre Chromium real e o servidor HTTP real. As respostas de transcrição e análise Groq são simuladas explicitamente; não há chave real nem chamadas externas. O vídeo de teste é sintético.

- Abrir JSON antigo preservou texto, cortes e posição, sem Groq.
- Importar acionou transcrição e edição completas. Duplicata e fala lateral simuladas chegaram cortadas automaticamente. A chave de teste não entrou no JSON.
- Clique posicionou/pausou; clique direito restaurou; Ctrl+Z desfez; a reprodução saltou cortes e restabeleceu o áudio.
- Documento de 6.848 palavras: clique em palavra distante, acompanhamento e suspensão ao rolar manualmente funcionaram.
- Exportação pela interface gerou um MP4 único real com FFmpeg e um XML real. Ambos representaram **13,4 s**. O MP4 teve faixas de áudio/vídeo; o teste automatizado de exportação também verificou diferença de início A/V <0,08 s e de duração <0,15 s em outro vídeo sintético.
- Nenhum erro JavaScript; vídeo e JSON de entrada mantiveram seus hashes.
- Resoluções 1280×720, 1366×768 e 1920×1080: botões de exportação dentro da tela e sem overflow horizontal.
- Resultados em `evidencias/interface.json`, `evidencias/responsividade.json` e capturas PNG.

Reproduzir em pasta de saída nova:

```text
pip install playwright groq numpy onnxruntime
python validacao/interface_real.py --output PASTA_NOVA --chromium CAMINHO_DO_CHROMIUM
```

O teste usa FFmpeg/FFprobe no PATH. Não é um teste presencial do Windows, do arquivo original ou da qualidade do modelo Groq.

### Áudio e instalação

A amostra MP3 de 124,452 s foi processada pelo modelo Silero original em CPU: 32 regiões de voz, somando 50,976 s; cerca de 0,759 s de processamento nesta máquina, sem cache. Isso valida execução e integridade do modelo, sem comprovar que todas as fronteiras são editorialmente corretas. O áudio é a amostra curta anterior, não o original do vídeo de 40 minutos.

Foram feitas simulações independentes de upgrade 0.11.2, 0.11.16 e 0.11.17 em pastas temporárias: conferência de versão, preflight real (imports, sintaxe JS, hash ONNX, FFmpeg disponível), backup integral/hash, atualização e postflight real. Vídeos e JSON de teste permaneceram iguais ao backup. Há testes de corrupção de backup, rollback por falha de cópia e por falha de verificação final. Ambas as entradas de instalação usam a mesma rotina segura.

O atualizador não toca no destino antes de verificar o backup. Só aceita a pasta `Desktop_V10`, recusa links/junções e pastas Motion/Remotion, e escreve apenas uma lista explícita de arquivos do Desktop. O manifesto fica ao lado do backup. O pacote não contém chave Groq.

## O que falta validar no computador do usuário

1. Versão instalada, requisitos e espaço livre; executar o atualizador com o aplicativo fechado e conferir seu backup real.
2. Reproduzir o vídeo original, conferir sílabas nas bordas e a relação entre áudio, imagem e palavras. A transcrição pode continuar errando conteúdo.
3. Usar a conta Groq e avaliar o modelo de contexto em edição real, limites/cota e decisões intencionais. O modo automático pode errar; revisão antes da entrega continua necessária.
4. Exportar o vídeo completo, conferir sincronismo ao longo dos 40 minutos, importar o XML no DaVinci, relink e taxa de quadros. Estrutura XML verificada não equivale a importação real aprovada.
5. Medir fluidez e tempo no i7-3770/16 GB. O desempenho na nuvem não é o desempenho desse computador.

## Instalar

Consulte `LEIA_PRIMEIRO.txt`. Extraia fora da instalação e execute `ATUALIZAR_V11_18.bat`. O destino padrão é `C:\MagicEdit\Desktop_V10`; o backup integral verificado é obrigatório. Para iniciar, use `INICIAR_MAGIC_EDIT.bat` na pasta definitiva. Não substitua manualmente arquivos nem apague o backup antes da conferência.
