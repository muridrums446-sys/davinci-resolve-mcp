# Magic Edit V11.21 — fábrica, revisão 2 do instalador

O usuário confirmou pelo erro no Windows: instalação 0.11.14 encontrada em
C:\Magicedit\MagicEdit_Desktop_V11_Atualizacao\MagicEdit_Desktop_V11.
O atualizador anterior interrompeu por falta de Node.js antes de copiar o backup
ou trocar os arquivos. O problema era uma exigência da validação, não do app:
Magic Edit inicia com Python e executa seu JavaScript no navegador.

Esta revisão não exige instalar Node.js. Sempre confere os sete módulos JS
por SHA-256 contra o manifesto embutido da distribuição que passou nos testes.
Se Node estiver disponível, executa também a checagem sintática --check.
Sem Node, informa a alternativa e continua. Não ignora JavaScript alterado.
Python/Groq/NumPy/ONNX Runtime, modelo Silero e FFmpeg/FFprobe continuam sendo
verificados. Backup integral por SHA-256, manifesto e rollback são preservados.
Nenhum código de edição, exportação, atalhos ou integração Groq foi modificado.
A versão do app continua 0.11.21. A revisão é apenas do instalador.

## Executar no PC da fábrica

1. Feche o Magic Edit e o servidor; feche também a janela do atualizador antigo.
2. Extraia MagicEdit_V11_21_Fabrica_R2.zip em Downloads, fora da instalação.
3. Abra Magic_Edit_Desktop_V11_21_Fabrica_R2 e execute ATUALIZAR_V11_21.bat.
4. Aguarde a conclusão. Mantenha o backup criado ao lado da instalação.
5. Abra INICIAR_MAGIC_EDIT.bat da pasta instalada indicada acima.

Não copie os arquivos por cima manualmente nem mova a instalação.
Se houver nova interrupção, envie a mensagem completa e preserve os backups.

## Evidências desta revisão — Linux na nuvem

- Node: 94 testes aprovados, nenhuma falha.
- Python: 86 reportados, 79 aprovados, 7 ignorados por ausência das fixtures
  históricas V11.10–V11.16 no pacote original. Nenhuma falha.
- Teste de preflight sem Node, com checagens Python/modelo/FFmpeg reais;
  teste de rejeição de JavaScript adulterado mesmo sem Node.
- Oito testes de atualização no caminho da fábrica, incluindo preservação,
  backup, falha de cópia e rollback após falha de validação final.
- Atualização CLI completa com PATH sem Node, mantendo somente FFmpeg/FFprobe:
  preflight e postflight reais passaram, backup integral de 107 arquivos
  idêntico por SHA-256, 106 arquivos da lista fechada instalados, vídeo/projeto/
  configuração fictícios, pastas protegidas e backup antigo preservados.
  Fixture: runtime V11.21 com marcador de versão 0.11.14, não uma instalação
  real V11.14. Mensagem de Node opcional registrada antes/depois da cópia.
- Código de edição e exportação comparado com a V11.21 original: idêntico.
- Revisão independente sem problemas críticos ou importantes; corrigida uma
  contagem incorreta de módulos apenas na documentação.
- Logs e resultado da simulação acompanham o ZIP. O aviso do ONNX sobre não
  persistir identificador de telemetria na nuvem não impediu a validação.

Não acessamos o Windows, executamos o BAT no computador ou testamos DaVinci real.
A instalação real e seu backup só serão confirmados ao executar esse pacote.
A branch principal e o código do plugin DaVinci permanecem preservados.
