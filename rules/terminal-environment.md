# Ambiente para qualquer comando de terminal

Aplica-se a todo comando executado em qualquer terminal, em qualquer projeto, incluindo backend e frontend.

1. Antes de executar comandos no terminal, identifique o diretório de trabalho e use ferramentas de leitura de arquivos para procurar a configuração do mise (`mise.toml` ou `.mise.toml`) nesse diretório, na raiz do projeto e nos diretórios ancestrais aplicáveis. Confira as ferramentas e versões declaradas.
2. Quando houver configuração, execute todos os comandos no diretório de trabalho apropriado com `mise exec -- <comando>`, inclusive Git, instalações, scripts, testes e subprocessos. Confirme as versões efetivas das ferramentas necessárias usando o mesmo ambiente, por exemplo `mise exec -- node --version` e `mise exec -- pnpm --version`.
3. Refaça a checagem ao mudar de projeto ou diretório com outra configuração, abrir um novo terminal ou quando a configuração mudar. Não presuma que o shell já ativou o mise.
4. Se não houver configuração do mise, confira os requisitos de versão nas configurações do projeto antes de usar as ferramentas do shell.
5. Se o mise estiver indisponível ou não conseguir fornecer as versões declaradas, informe o impedimento antes de prosseguir. Não altere dependências, lockfiles ou configurações para contornar uma divergência de ambiente, nem pule hooks sem autorização explícita.
