# Magic Edit Desktop V11.21

[Baixar MagicEdit_V11_21.zip](https://github.com/muridrums446-sys/davinci-resolve-mcp/raw/refs/heads/magic-edit-v11-21-download/MagicEdit_V11_21.zip)

1. Feche o Magic Edit e o servidor.
2. Extraia o ZIP fora de `C:\MagicEdit\Desktop_V10`.
3. Execute `ATUALIZAR_V11_21.bat`. Ele verifica o backup integral antes de atualizar.
4. Abra `C:\MagicEdit\Desktop_V10\INICIAR_MAGIC_EDIT.bat` e confira V11.21.

## Ajustes

- Pausas confirmadas acima de **0,7 segundo** são cortadas automaticamente, preservando margens junto à voz. Limite ajustável em Ferramentas e salvo no projeto/autosave.
- Direito na seleção da timeline alterna cortar/restaurar. A seleção permanece; restaurar parte de um corte mantém as outras partes removidas.
- Repetições: **3 ou mais palavras consecutivas iguais, em tentativas próximas**, mantendo a última. Uma/duas palavras e começos comuns de frases diferentes ficam preservados para revisão.
- Projetos antigos mantêm cortes salvos ao abrir. FCPXML 1.9, bruto completo, opção de master, MP4 final, Espaço e Groq permanecem.

[Relatório de validação](RELATORIO_V11_21.md) · [SHA-256](MagicEdit_V11_21_SHA256.txt)

Testes na nuvem Linux: 94 Node e 69 Python aprovados; 7 testes históricos ignorados por fixtures ausentes. Interface Chromium e FFmpeg reais, respostas Groq simuladas. Atualização CLI com backup integral de 104 arquivos verificado. Windows/DaVinci reais não foram acessados nesta sessão.

Mantenha o backup. O original, JSON e configurações são preservados. Esta branch distribui o instalador; o código e a branch principal do plugin DaVinci MCP não foram alterados. Os pacotes anteriores continuam disponíveis.
