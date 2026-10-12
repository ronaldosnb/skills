---
name: git-workflow
description: "Aplica o fluxo pessoal de Git do usuário: branches e commits em português, convenções de nomenclatura e nenhuma integração automática. Use ao criar branches, preparar commits ou orientar operações Git."
---

# Git Workflow

Siga estas convenções ao trabalhar com Git neste ambiente.

## Branches

- Nunca faça commits diretamente em `main`.
- Crie uma branch própria para cada implementação distinta. Não misture implementações não relacionadas na mesma branch.
- Use nomes em português no padrão `prefixo/descrição-da-implementação`, com palavras em minúsculas separadas por hífens. Exemplo: `feat/adicionando-login`.
- Prefira prefixos coerentes com a mudança, como `feat`, `fix`, `refactor`, `docs`, `test`, `chore` e `style`.

## Commits

- Escreva commits em português no padrão `prefixo: descrição da implementação`. Exemplo: `feat: adiciona modo escuro na tela de login`.
- Cada commit deve conter uma mudança coesa e funcional; não inclua alterações não relacionadas.
- Antes de commitar, confira o repositório, a branch atual e o conteúdo de `git status` e do diff. Preserve alterações preexistentes que não pertençam à tarefa.
- Não inclua arquivos sensíveis, como `.env`, chaves, tokens ou credenciais.
- Execute testes, lint ou verificações disponíveis quando forem pertinentes. Se alguma verificação falhar, informe o resultado antes de commitar.

## Limites de operação

- Não faça merge: o usuário criará e gerenciará os PRs no GitHub.
- Não faça `push`, crie PRs ou altere branches remotas sem solicitação explícita do usuário.
- Não use `git commit --amend`, `rebase`, `push --force` ou `--no-verify` sem autorização explícita.
