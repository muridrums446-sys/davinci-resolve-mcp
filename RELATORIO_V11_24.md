# Magic Edit Desktop V11.24 — Gemini pelo áudio

Atualização cumulativa da V11.23. Instalação da fábrica:
`C:\Magicedit\MagicEdit_Desktop_V11_Atualizacao\MagicEdit_Desktop_V11`.
A origem anterior, os projetos, as amostras e os pacotes antigos foram preservados.

## Mudança

Integração opcional com Gemini para analisar áudio e contexto. A Groq continua
transcrevendo e sua análise textual continua disponível. A interface lista modelos
acessíveis à chave da conta, sem presumir um modelo atualmente gratuito ou disponível.
A lista confirma geração; a primeira análise verifica na prática se o modelo aceita
áudio e JSON estruturado. Não existe troca silenciosa de modelo ou ativação de cobrança.
A chave fica somente na sessão e o envio de áudio/texto exige ativação explícita.
O plano, a cota e eventual faturamento são controlados no Google AI Studio; o aplicativo
não consegue consultar um saldo financeiro ou garantir que uma chamada seja gratuita.

Áudio mono16k FLAC em janelas de até60s, avanço48s, com contexto sobreposto para procurar
tomadas próximas. É possível analisar o vídeo completo ou a seleção na timeline; o
contexto pode incluir segundos ao redor, mas cortes novos precisam ficar na seleção.
Limites: vídeo de até60min e transcrição de até12000palavras por análise. No máximo30
candidatos e45s por candidato por janela, resposta8192tokens, sem retries automáticos. A cota pode exigir espera maior do que o intervalo local; nesse caso a análise interrompe para retomada explícita.
Há intervalo entre chamadas; 429/interrupção conserva cache de partes concluídas.
Resultado parcial nunca é aplicado automaticamente depois de erro.

O modelo retorna intervalos, citações, motivo e tomada posterior a manter. Tempos finitos,
pertencimento à janela/seleção, limites, citações e bordas das palavras são conferidos.
Repetições exigem>=3palavras consecutivas compartilhadas, tentativa posterior próxima e
limites que não representem apenas o início comum de duas frases diferentes. Negação
alterada impede corte automático. Indicação de certeza do modelo não é probabilidade
calibrada. Trechos sem transcrição, ruídos ou tempos incertos são sugestões para ouvir.
Não foi instalada uma nova transcrição nem WhisperX nesta entrega: Gemini não corrige
silenciosamente as palavras existentes. Ainda pode errar ou deixar erros para revisão.

Cortes são intervalos reversíveis do editor existente: riscos no texto/timeline,
restauração pelo botão direito, sugestões com Cortar/Restaurar e Ctrl+Z. Campo aditivo
`audioEditingReport` acompanha JSON e recuperação automática; schema1 permanece.
Abrir projeto antigo não recalcula cortes nem chama Gemini. Chave, áudio e resposta
bruta não entram no projeto/cache; o cache guarda apenas candidatos validados. HTTP
usa host Google fixo e chave no cabeçalho, nunca URL; redirects são recusados e erros
externos são convertidos em mensagens sem corpo bruto ou credenciais.

## Testes

Resultados finais na nuvem: **118 testes Node passaram**; **107 testes Python executados,
100 passaram e7 foram ignorados** por ausência de versões históricas V11.10–16 usadas
apenas como fixtures antigas. Nenhuma falha. Chromium: **11 verificações Gemini**, mais
**16 regressões gerais**, **10 de seleção/exportação leve** e **8 de retomadas**;
nenhum erro JavaScript. Exportação real MP4 e XML da regressão:13,4s cada.
As imagens/JSON/logs correspondentes estão em `evidencias/`.

Revisão independente encontrou dois problemas importantes antes da entrega, ambos
reproduzidos por testes que falhavam e corrigidos: (1) expansão de bordas sobre uma
palavra vizinha com timestamps sobrepostos, agora impede aplicação automática; (2)
nova análise que cortava uma tomada mantida anteriormente, agora vetada pelo relatório
persistente inclusive depois de salvar/reabrir. As suítes completas passaram após
as correções; não restaram achados importantes pendentes.
Testes automatizados incluem cliente HTTP, modelos/paginação, erros401/403/404/429,
seleções inválidas, tempos inválidos, citações divergentes, tomada mantida, negação,
início comum de frases diferentes, geração de FLAC real, limpeza de temporários,
cache por vídeo/modelo/contexto/transcrição/seleção, retomada após erro parcial e
exclusão de segredo; aplicação/restauração JS e proteção da última fala restante.

Chromium real com servidor HTTP, FFmpeg, MP4 e arquivos de projeto reais de teste.
Somente transporte Google e diálogo nativo de arquivos simulados. O cenário usa
vídeo e áudio sintéticos com palavras de teste, portanto não mede compreensão do áudio:
verifica payload/extração/aplicação/restore/save/reopen/cache/erro e integração.
Regressões preservam transcrição navegável, espaço, silêncio>0,9s, seleção, retomadas,
exportação leve, MP4 único e FCPXML1.9. XML validado estruturalmente; não importado em Resolve.
Os exemplos de JSON/Gling continuam referência estrutural/editorial, não listas de
cortes copiadas. Nenhum vídeo do usuário ou chave entra na distribuição GitHub.

## Instalador e limites de validação

Atualizador usa lista fechada de arquivos, hashes JavaScript, verificação Python/Silero,
FFmpeg/ffprobe, Node opcional, backup integral com SHA256 antes das trocas e rollback
em falha de cópia/pós-verificação. Mantém pastas/projetos/brutos/configurações fora da
lista. Não modifica Motion, Remotion, src irmão ou o plugin DaVinci. Instalação é testada
na nuvem com o pacote extraído, contra a V11.23 e simulação com marcador0.11.14.
A simulação não equivale a ter todos os arquivos reais daquela instalação antiga.

Não houve acesso ao Windows do usuário ou ao vídeo completo original. Não foram
validados instalação/backup no PC, DaVinci real, chave/quota/modelo Gemini da conta,
precisão de cortes em gravações reais, desempenho no i7 ou qualidade equivalente ao Gling.
A integração está preparada para esses testes; não é alegação de precisão já medida.

Verificação do pacote extraído:125 arquivos instalados;120 arquivos do destino
copiados integralmente para backup verificado nos dois cenários. Todos os hashes do
backup e manifesto conferidos; projetos/bruto/configuração fictícios, pastas irmãs
protegidas e backups anteriores permaneceram iguais. Pré e pós-verificação reais,
sem Node.js, usando o Python da nuvem e FFmpeg/ffprobe reais. Evidência em
`evidencias/upgrade.json`. O cenário0.11.14 usa arquivosV11.23 com marcador antigo:
é teste de compatibilidade de versão/caminho, não uma instalação WindowsV11.14 real.
