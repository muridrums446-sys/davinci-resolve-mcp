# Integração Magic Edit Resolve — silêncio >0,9s

Pacote de teste dirigido ao painel/motor fornecidos pelo usuário em26/10/2026.
Não altera o projeto MCP, Motion, Remotion nem o painel de Transcrição.

## Implementação

- Reutiliza os3módulos JS do DesktopV11.28 sem alterar bytes e o mesmo Silero,
  audio_wave.py e vad_local.py. Decoder de energia2000Hz/20bins, normalização e
  FPS nominal idênticos aos do Desktop. Pausas de0,9s exatos são preservadas.
- Painel com5intensidades, padrão Equilibrado50. Análise local em processo
  separado, UI com timer/tempo decorrido/cancelamento. Sem Gemini ou envio de mídia.
- Proteção de palavras quando existe JSON/autosave do Desktop com caminho/duração
  correspondentes. Sem esse JSON, informa ausência e usa Silero+energia;
  resultados podem diferir de um projeto externo que tinha mais proteção textual.
- Marcadores em coordenadas relativas à timeline; aplicação verifica fingerprint
  de clipes/fontes e cria NOVA timeline V1/A1, com fontes semiabertas convertidas
  a endFrame inclusivo. GetLeftOffset controla offsets, não o leitor instável
  GetSourceStartFrame. Confere quantidade/posições/durações/vínculo A/V no resultado.
- Uso no bruto antes de efeitos: não transporta grades/FX/mixagem para a montagem.
  Original preservada. Camadas adicionais/fontes V1/A1 diferentes/Fusion/transformações
  são recusadas. Não é integração de repetição/Gemini/pigarro isolado do Desktop.

## Instalação e recuperação

Verifica hashes exatos do painel e motor enviados antes de substituir. Salva e
confere snapshots de todos os arquivos afetados, mantém journal antes da primeira
mudança e inclui RESTAURAR.bat. Uma transação interrompida precisa ser restaurada
antes de reinstalar; não é falsamente tratada como concluída. Reinstalação normal
não cria backups adicionais e pode repor runtime ausente; runtime modificado é
preservado e bloqueia a reinstalação.

Só13nomes exatos de backup do levantamento são retirados da pasta Scripts;
as cópias ficam em LOCALAPPDATA/MagicEdit/Silencios09/history. Os4utilitários
não classificados como backup e backups de projetos/timelines ficam intactos.

## Evidência

-21testes passam, incluindo regressões RED/GREEN para limiar, energia600Hz,
  normalização, FPS médio próximo do nominal, fonte com leitor deslocado1quadro,
  painel original completo executado com UI simulada, marcador relativo,
  aplicação/verificação V1+A1 em adaptador simulado, falha de append,
  invalidação de plano, hashes/backup/restauração e interrupções da instalação.
- Python/ONNX/FFmpeg/Node reais exercitados no pré/pós-instalação de fixture,
  com13backups e4utilitários: restauração de todos os hashes originais conferida.
- Worker Silero+FFmpeg+Node real executado em dois trechos privados de8s e77s.
  Esses arquivos e suas transcrições não estão no pacote público.
- Revisão independente: achados de paridade/offset/journal/escopo de limpeza
  corrigidos; sem pendências importantes/críticas na versão revisada.

NÃO VALIDADO: instalação em Windows real, UIManager/timer/cancelamento/AppendToTimeline
no Resolve21.1.1 real, nem qualidade dos cortes no material completo. O primeiro
uso deve ser em timeline de bruto, conferindo a candidata e preservando a original.
