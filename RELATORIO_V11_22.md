# Magic Edit Desktop V11.22 — seleção leve e pausas de 0,9 s

Atualização cumulativa da V11.21 fábrica R2, para a instalação em
C:\Magicedit\MagicEdit_Desktop_V11_Atualizacao\MagicEdit_Desktop_V11.

## Comportamento entregue

A timeline tem o botão **Exportar seleção leve**. Selecione X–Y na onda,
régua ou miniaturas e escolha onde salvar. O intervalo é extraído do original,
incluindo partes já riscadas, sem modificar a seleção nem os cortes do projeto.
Funciona mesmo sem palavras na transcrição. Não sobrescreve o original ou saída
existente; cancelamento e erro permitem tentar novamente.

O arquivo é MP4 H.264/AAC leve para análise: até 854×480, mantendo proporção sem
aumentar imagem pequena, até 30 fps, CRF 32, vídeo com maxrate 600 kbps e áudio
mono 16 kHz/64 kbps. O tamanho varia conforme conteúdo/duração. Bordas acompanham
frames da fonte; no máximo uma fração de frame adicional em cada ponta. Esse
perfil é usado apenas na seleção. O MP4 final e a exportação DaVinci mantêm seus
perfis, incluindo a referência ao bruto completo e master compatível opcional.

Padrão de pausas: **maiores que 0,9 s**, com as mesmas proteções de palavras,
voz Silero e energia. O padrão anterior 0,7 migra nas preferências e JSON antigos;
valores personalizados diferentes são preservados. Novos ajustes, inclusive
escolher manualmente 0,7, persistem por campo opcional silenceSettingsVersion=22
no JSON/autosave (schema 1). Abrir JSON não recalcula nem restaura cortes salvos.
Aplicar novo ritmo continua acrescentando cortes, sem restaurar os anteriores.
Para testar o novo ritmo integralmente, importe um vídeo novo.

Não houve mudança no reconhecimento da fala ou no detector de contexto. Esta
ferramenta permite fornecer exemplos para investigar tentativas omitidas.
Groq/Whisper, caches, modelo Silero e licença, reprodução/Espaço, restauração
com botão direito, Ctrl+Z e funções de exportação anteriores foram preservados.

## Validação em Linux na nuvem

- Node: 101 testes aprovados, nenhuma falha. Novos casos cobrem seleção normal,
  reversa, bordas, um frame, NTSC, seleção final de divisões com duração do
  container diferente do último frame, inválidos, migração do limite e pausas
  abaixo/iguais/acima de 0,9 s. Casos anteriores de 0,7 continuam funcionando
  quando o valor é solicitado explicitamente.
- Python: 87 testes reportados, 80 aprovados, 7 ignorados por ausência das fixtures
  históricas V11.10–V11.16 no pacote original. Não são contados como aprovados.
  Perfil leve testado com FFmpeg real em fonte 1280×720/60 fps: resolução/fps
  reduzidos, áudio mono 16 kHz, duração de dois segundos, arquivo menor que 40%
  da fonte e original preservado por SHA-256. Demais testes verificam exportação
  usual, FCPXML, backup, rollback e ausência de Node.
- Chromium/HTTP/FFmpeg reais: 10 verificações específicas da seleção, incluindo
  fonte correta verde/azul, partes riscadas presentes, áudio e sincronia,
  cancelamento, nome já existente, seleção sem texto/reversa/um frame, limites
  personalizados persistidos, API recusando perfil inválido, botões visíveis
  em 1366/1024 px e original/JSON de entrada preservados. Zero erros JavaScript.
- Outras 16 verificações reais da interface: projetos antigos, reedição,
  duplicata de três palavras, botão direito nas três faixas, Espaço, rolagem
  com 6848 palavras, MP4 único e FCPXML com referência ao original/master.
  MP4 final e timeline exportados concordaram em 13,4 s no cenário sintético.
- Seletores de arquivo do sistema e respostas Groq foram simulados. Nenhuma
  chave real ou chamada real à API. O aviso ONNX de telemetria não persistida
  no ambiente da nuvem não impediu a execução das verificações.
- Atualização CLI sem Node, com verificações reais antes/depois: instalação
  anterior V11.21 R2 e simulação de marcador 0.11.14. Backup integral de 109
  arquivos conferido por SHA-256 em cada cenário, projetos/mídia/configuração
  fictícios e pastas irmãs/backup antigo preservados. No cenário 0.11.14 o
  runtime é o da V11.21 R2 com marcador antigo: teste de compatibilidade do
  instalador, não teste de uma instalação V11.14 real.
- Revisão independente identificou um caso de seleção final NTSC; foi reproduzido
  por teste falhando, corrigido e testado novamente. Manifesto JS atualizado.

## Instalador e preservação

ATUALIZAR_V11_22.bat usa o destino da fábrica explicitamente. Versões aceitas:
0.10.x e 0.11.0–0.11.22, com arquivos identificadores obrigatórios. A CLI mantém
Desktop_V10 como padrão compatível, enquanto o BAT passa o caminho da fábrica.
Node continua opcional; os sete módulos JS são sempre conferidos contra SHA-256
embutido e, com Node disponível, recebem também --check. Python/modelo/FFmpeg
continuam obrigatórios. Backup integral verificado precede qualquer substituição;
falha de cópia ou pós-verificação restaura arquivos. Só a lista fechada é copiada.

Modelo ONNX preservado: SHA-256
1a153a22f4509e292a94e67d6f9b85e8deb25b4988682b7e174c65279d8788e3.
Motion, src irmã, Remotion, plugin DaVinci e branches anteriores são preservados.
Arquivos comparativos históricos V11.17/Gling permanecem como referência, sem
copiar decisões do Gling. Evidências de interface/testes desta versão acompanham
o pacote; responsividade-v11-18.json e comparações antigas são históricas.

## Limites

Não houve acesso ao computador, backup/instalação reais no Windows ou importação
real no DaVinci. Qualidade editorial em vídeos reais e desempenho no PC da fábrica
não foram medidos. Os trechos leves exportados pelo usuário permitirão investigar
os casos reais. A instalação e o backup reais dependem de executar o atualizador.
