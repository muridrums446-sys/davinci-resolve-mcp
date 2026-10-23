# Magic Edit Desktop V11.25 — instalação em casa e diagnóstico Gemini

Entrega cumulativa para a instalação existente de casa em
`C:\MagicEdit\Desktop_V10`. Use **ATUALIZAR_V11_25_CASA.bat**.
O **INSTALAR_V11.bat** agora chama esse mesmo atualizador de casa.
O **ATUALIZAR_V11_25.bat** permanece explícito para a pasta da fábrica.
Não use o atualizador da fábrica no PC de casa. O backup integral continua
obrigatório, verificado por hashes antes de qualquer substituição.

## Problema e correção

O usuário vê somente “Liste os modelos primeiro”, sem diagnóstico visível.
Confirmamos falhas de interface: resultado distante do botão, progresso sem
mudança de rótulo e aviso de análise sobrescrevendo o resultado do teste.
A causa real da consulta no Windows/Google ainda não foi observada. Não temos
chave nem sessão do usuário e não ativamos qualquer cobrança ou faturamento.

Agora o teste tem status próprio imediatamente abaixo do botão, com rótulo de
consulta, mensagem visível e estados sucesso/erro. Falhas rolam o painel até o
aviso e também aparecem no toast. A análise só libera depois de selecionar um
modelo; um clique nela não apaga o diagnóstico da consulta. Alterar chave remove
a lista antiga. A consulta tem abort45s no navegador e20s por chamada Google,
com limite de tempo entre páginas; geração de áudio mantém seu comportamento.
Servidor local antigo404 recebe orientação para reiniciar o Python instalado.

Erros Google usam somente códigos estruturados permitidos para orientar chave
inválida, Generative Language API desativada ou restrição de chave. Nenhum corpo
bruto/mensagem bruta/metadado/URL com chave é mostrado ou salvo. A chave segue
no cabeçalho HTTPS, na sessão, e fora de JSON/XML/cache. Não houve alteração de
regras de corte, Groq, mídia original ou parâmetros de silêncio.

Encontramos também o atalho antigo da V11.24 apontando para um BAT V11.23 ausente.
O defeito foi reproduzido em teste da integridade de dependências da distribuição,
antes da correção para o BAT de casa. Isso não é execução Windows de um BAT.

## Validação V11.25

-118 testes Node passaram;109Python executados,102passaram e7ignorados por fixtures
históricasV11.10–16 indisponíveis. Sem falhas.
-17 testes focados de áudio/transporte incluem o novo caso de diagnóstico por
código Google com corpo contendo segredo fictício, garantindo não vazar esse dado.
-Chromium real:5 verificações novas de modelos (erro visível403, carregamento,
sucesso/seleção, troca de chave, servidor antigo404 e timeout45s com relógio
controlado), além das11 do fluxo Gemini existente. HTTP e FFmpeg reais; somente
transporte Google e diálogos de arquivos simulados. Não houve chamadas reais
à conta Gemini, medição de qualidade do áudio ou validação da cota gratuita.
-Backup/instalação conferidos na nuvem com pacote extraído e Node ausente: casa
partindo dos arquivosV11.18, casaV11.24 e fábricaV11.24. Nos3cenários foram instalados
130arquivos, com inventários/hashes do backup e manifesto iguais ao destino anterior.
Projetos/brutos/configurações fictícios, pastas irmãs e backups anteriores preservados.
Atalhos têm destinos explícitos; validação de dependências BAT passou. Não foi execução
real dos BATs no Windows. Evidência em `evidencias/upgrade.json`.
-Regressões de interface adicionais:16gerais,10seleção/exportação leve e8retomadas;
50verificações de interface ao todo com as5+11acima, sem erros JavaScript.
-Ainda sem acesso ao Windows/DaVinci do usuário. Instalação e backup no seu PC
somente ocorrerão ao executar o atualizador e confirmar o sucesso na janela.

Abaixo permanece o relatório técnico da integração V11.24, que continua válida.
Os resultados acima se referem às mudanças V11.25; dados históricos abaixo não
substituem a validação de instalação/conta do usuário.

---

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
