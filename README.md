# Magic Edit V11.21 — fábrica, instalador revisão 2

[Baixar MagicEdit_V11_21_Fabrica_R2.zip](https://github.com/muridrums446-sys/davinci-resolve-mcp/raw/refs/heads/magic-edit-v11-21-fabrica-r2-download/MagicEdit_V11_21_Fabrica_R2.zip)

Corrige a interrupção "Node.js ausente". Node é opcional: o atualizador confere
os sete módulos JavaScript contra o SHA-256 da distribuição validada e, se Node
estiver disponível, executa também --check. Não precisa instalar Node para usar
o Magic Edit. As verificações Python/modelo/FFmpeg e o backup integral continuam.

Destino confirmado na captura:
`C:\Magicedit\MagicEdit_Desktop_V11_Atualizacao\MagicEdit_Desktop_V11`.

1. Feche Magic Edit, servidor e a janela do atualizador anterior.
2. Extraia o novo ZIP em Downloads, fora da pasta instalada.
3. Entre em `Magic_Edit_Desktop_V11_21_Fabrica_R2` e execute `ATUALIZAR_V11_21.bat`.
4. Aguarde a conclusão e abra `INICIAR_MAGIC_EDIT.bat` na instalação acima.

Mantenha o backup criado ao lado da instalação. Não copie os arquivos manualmente.
A versão continua 0.11.21; o código de edição e exportação permanece idêntico.

[Relatório](RELATORIO_FABRICA_R2.md) · [SHA-256](MagicEdit_V11_21_Fabrica_R2_SHA256.txt)

Na nuvem Linux: 94 testes Node e 79 Python aprovados; 7 testes históricos ignorados
por fixtures ausentes. Atualização CLI completa sem Node, backup de 107 arquivos
conferido e preservação de arquivos simulados validada. Não houve acesso ao
Windows, execução real do BAT ou teste real do DaVinci. Pacotes anteriores
permanecem disponíveis e a branch principal/código do plugin não são alterados.
