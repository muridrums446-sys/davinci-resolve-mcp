# Magic Edit Desktop V11.22 — seleção leve e pausas de 0,9 s

[Baixar MagicEdit_V11_22_Fabrica.zip](https://github.com/muridrums446-sys/davinci-resolve-mcp/raw/refs/heads/magic-edit-v11-22-download/MagicEdit_V11_22_Fabrica.zip)

1. Feche o Magic Edit e o servidor.
2. Extraia o ZIP em Downloads, fora da instalação.
3. Execute `ATUALIZAR_V11_22.bat` na pasta extraída.
4. Depois da conclusão, inicie pelo `INICIAR_MAGIC_EDIT.bat` instalado em
   `C:\Magicedit\MagicEdit_Desktop_V11_Atualizacao\MagicEdit_Desktop_V11`.

O atualizador identifica a instalação, faz backup completo e confere SHA-256 antes
de trocar arquivos. Mantenha o backup ao lado da instalação. Node.js é opcional.
Não precisa mover a instalação nem copiar arquivos manualmente.

## Exportar o trecho que precisa de atenção

Arraste de X até Y na timeline e clique **Exportar seleção leve**. Escolha onde
salvar o MP4 e envie o arquivo para análise. O trecho inclui as partes riscadas
do original, para ouvirmos erro e retomada juntos. A seleção e seus cortes ficam
preservados; funciona sem transcrição. Saídas existentes não são sobrescritas.

Perfil leve: imagem até 480p, até 30 fps, H.264 CRF32/maxrate600k e áudio mono
16 kHz/64 kbps. O tamanho depende do conteúdo e da duração. Trechos de 20 a 60
segundos costumam ser suficientes para investigar cada problema.
O MP4 final e a exportação DaVinci mantêm seus perfis anteriores.

## Pausas

Novo padrão: cortar pausas **maiores que 0,9 segundo**, com proteção de voz e palavras.
O padrão anterior 0,7 migra para 0,9; outros valores personalizados ficam.
Abrir projeto antigo conserva os cortes salvos. Para testar o novo ritmo desde
o início, importe um vídeo novo. Aplicar novo ritmo acrescenta cortes elegíveis,
sem restaurar os anteriores. Ajustes novos acompanham JSON/autosave.

[Relatório de validação](RELATORIO_V11_22.md) · [SHA-256](MagicEdit_V11_22_Fabrica_SHA256.txt)

Na nuvem Linux: 101 testes Node e 80 Python aprovados; 7 testes históricos ignorados
por fixtures ausentes. Chromium/HTTP/FFmpeg reais: 10 verificações da seleção e
16 da interface anterior, sem erros JavaScript. Atualizador sem Node e backup
integral de 109 arquivos verificados com instalação simulada. Groq e seletores
nativos de arquivos simulados; sem API real, acesso ao Windows ou DaVinci real.

Esta versão prepara os trechos para analisar as omissões da transcrição; não altera
o reconhecimento de fala ou detector de contexto. Projetos, vídeos e integração
Groq são preservados. Pacotes anteriores, branch principal e plugin DaVinci intactos.
