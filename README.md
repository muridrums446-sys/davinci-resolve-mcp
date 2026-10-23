# Magic Edit V11.21 — PC da fábrica

[Baixar MagicEdit_V11_21_Fabrica.zip](https://github.com/muridrums446-sys/davinci-resolve-mcp/raw/refs/heads/magic-edit-v11-21-fabrica-download/MagicEdit_V11_21_Fabrica.zip)

Este pacote corrige o atualizador para a instalação mostrada na captura:
`C:\Magicedit\MagicEdit_Desktop_V11_Atualizacao\MagicEdit_Desktop_V11`.
A versão do aplicativo continua V11.21.

1. Feche o Magic Edit e o servidor.
2. Extraia o ZIP em Downloads, fora da pasta instalada.
3. Abra a pasta extraída `Magic_Edit_Desktop_V11_21_Fabrica` e execute `ATUALIZAR_V11_21.bat`.
4. Aguarde a conclusão e abra `INICIAR_MAGIC_EDIT.bat` na pasta instalada acima.

O atualizador confere a instalação e a versão antes de trocar arquivos; faz backup
integral e verifica SHA-256. Mantenha o backup ao lado da instalação. Não precisa
mover a pasta instalada nem copiar arquivos manualmente.

[Relatório desta revisão](RELATORIO_FABRICA.md) · [SHA-256](MagicEdit_V11_21_Fabrica_SHA256.txt)

Validação na nuvem Linux: 94 testes Node e 77 Python aprovados, 7 históricos ignorados.
Atualização CLI simulada com backup integral conferido, preservação de arquivos e
rollback testados. O BAT não foi executado no Windows e não houve acesso à sua máquina
ou ao DaVinci. O código de edição da V11.21 permanece igual.

Os arquivos e branches anteriores continuam disponíveis. Esta branch distribui
somente os pacotes do Magic Edit; a branch principal e o código do plugin DaVinci
não são alterados.
