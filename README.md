# Magic Edit Desktop V11.20

[Baixar MagicEdit_V11_20.zip](https://github.com/muridrums446-sys/davinci-resolve-mcp/raw/refs/heads/magic-edit-v11-20-download/MagicEdit_V11_20.zip)

Atualização cumulativa para a instalação existente em `C:\MagicEdit\Desktop_V10`.

1. Feche o Magic Edit e a janela do servidor.
2. Baixe e extraia o ZIP fora da pasta Desktop_V10.
3. Abra a pasta extraída e execute `ATUALIZAR_V11_20.bat`.
4. Aguarde o backup completo e a atualização. Depois abra `C:\MagicEdit\Desktop_V10\INICIAR_MAGIC_EDIT.bat`.

O atualizador verifica o backup antes de trocar o código. Preserve o backup.
Projetos e mídias do usuário são mantidos. Motion, Remotion e plugin DaVinci não são alterados.

## Novidades

- Arrastar um intervalo na timeline e clicar com o botão direito corta e risca o texto.
- Espaço corrigido após botões, rolagem da timeline, foco no vídeo e durante saltos de cortes.
- Exportar DaVinci gera FCPXML 1.9 com clipes editáveis e referência ao bruto completo, mantendo sobras para ajustes.
- Opção adicional para criar um master MP4 completo compatível, junto do FCPXML. O original é preservado.
- XML antigo FCP7, exportação MP4 final, Groq e recursos da V11.19 continuam disponíveis.

No DaVinci, importe o novo `.fcpxml` como linha de tempo. Mantenha o vídeo bruto na pasta original.
Se ativar o master compatível, mantenha o `.media.mp4` junto do FCPXML.

[Relatório de validação](RELATORIO_V11_20.md) · [SHA-256](MagicEdit_V11_20_SHA256.txt)

Testado na nuvem Linux com Chromium e FFmpeg reais. Não houve acesso ao Windows ou importação real no DaVinci.
Esta branch distribui o instalador; o código e a branch principal do plugin MCP não foram alterados.
Os pacotes V11.18/V11.19 anteriores permanecem disponíveis nesta branch.
