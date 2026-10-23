# Magic Edit Desktop V11.23 — tomadas interrompidas e reformuladas

[Baixar MagicEdit_V11_23_Fabrica.zip](https://github.com/muridrums446-sys/davinci-resolve-mcp/raw/refs/heads/magic-edit-v11-23-download/MagicEdit_V11_23_Fabrica.zip)

1. Feche Magic Edit e servidor.
2. Extraia o ZIP em Downloads, fora da instalação.
3. Execute `ATUALIZAR_V11_23.bat`. Destino da fábrica:
   `C:\Magicedit\MagicEdit_Desktop_V11_Atualizacao\MagicEdit_Desktop_V11`.
4. Aguarde a conclusão e inicie pelo `INICIAR_MAGIC_EDIT.bat` da instalação.

O atualizador faz backup integral e confere SHA-256 antes de trocar código.
Mantenha esse backup. Node.js continua opcional; não precisa mover a instalação.

## Aplicar o refinamento no projeto já salvo

Abra o JSON e use **Ferramentas → Editar automaticamente este projeto**.
Abrir sozinho preserva sua edição. A reedição acrescenta cortes e não retranscreve.
Clique direito restaura; Ctrl+Z desfaz.

A detecção local agora cobre os exemplos fornecidos:
- Cadeias incompletas de "Ao comprar...", preservando "então, quando você compra...".
- Perguntas próximas retomadas com outra introdução, mantendo "Próximo passo...".
- Tentativa interrompida "Então um exemplo de...10 reais e você...", preservando
  a explicação posterior com 100 reais. A introdução da tentativa também sai.

Sujeitos, negações e informação exclusiva são protegidos. Exemplos completos com
valores diferentes continuam mantidos. Casos incertos ficam para revisão.
São regras locais de comparação e alinhamento; o modelo Groq/Whisper não foi trocado
nem treinado. O padrão 0,9 s, seleção MP4 leve, MP4 final e DaVinci permanecem.

[Relatório](RELATORIO_V11_23.md) · [SHA-256](MagicEdit_V11_23_Fabrica_SHA256.txt)

Na nuvem Linux: 111 testes Node e 80 Python aprovados; 7 testes históricos ignorados
por fixtures ausentes. Chromium/HTTP/FFmpeg reais: 8 verificações das retomadas,
16 da interface anterior e 10 da seleção leve, sem erros JS. Novos casos usam
palavras/tempos do JSON original rebaseados para mídia sintética. Backup de 114
arquivos e atualização sem Node conferidos. Não houve acesso ao Windows ou DaVinci.

O MP4 recebido acrescenta outra passagem ("Então como você ganha... Basicamente...");
não foi usado como prova dos pontos de áudio das marcações. O arquivo e os modelos
ASR de diagnóstico não são publicados. Projetos, mídias, SDK/cache Groq e Silero
são preservados. Branch principal e plugin DaVinci permanecem intactos.
