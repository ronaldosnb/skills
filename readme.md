# Minhas Skills para Codex

Uma coleção de skills em português para tornar o trabalho com o Codex mais consistente em tarefas de investigação, Git e continuidade de projetos.

Cada skill contém instruções que orientam o agente sobre quando agir, quais cuidados tomar e como estruturar a resposta.

## Skills disponíveis

| Skill | Para que serve | Exemplos de pedido |
| --- | --- | --- |
| `bug-investigator` | Investiga bugs, falhas em testes, regressões, erros de build e comportamentos inesperados antes de propor uma correção. | “Investigue por que este teste falha.” / “Descubra a causa deste erro.” |
| `git-workflow` | Aplica o fluxo pessoal de Git: branches e commits em português, convenções de nomenclatura e nenhuma integração automática. | “Crie uma branch para esta implementação.” / “Prepare o commit.” |
| `handoff-context` | Prepara o contexto técnico para continuar o trabalho em outra conversa, como resumo no chat ou em um `HANDOFF_CODEX.md`. | “Gere um handoff.” / “Prepare o contexto para um novo chat.” |

## Skills de terceiros que uso

Estas skills não estão neste repositório. Instale a partir da fonte original e leia o conteúdo antes de instalar.

| Skill | Fonte | Para que serve |
| --- | --- | --- |
| `impeccable` | [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | Design, crítica e polimento de interfaces frontend. |
| `grill-with-docs` | [mattpocock/skills](https://github.com/mattpocock/skills) | Entrevista para refinar um plano ou design, gerando ADRs e glossário. |

## Como instalar

1. Clone este repositório:

   ```bash
   git clone https://github.com/ronaldosnb/my-skills.git
   ```

2. Copie as pastas desejadas para o diretório de skills do Codex:

   ```bash
   mkdir -p ~/.codex/skills
   cp -R my-skills/skills/* ~/.codex/skills/
   ```

3. Reinicie o Codex ou inicie uma nova conversa para que ele carregue as novas skills.

Também é possível instalar apenas uma skill. Por exemplo:

```bash
cp -R my-skills/skills/bug-investigator ~/.codex/skills/
```

## Como usar

Depois de instalada, basta pedir a tarefa em linguagem natural. O Codex identifica a skill adequada pelo contexto do pedido. Você também pode mencionar o nome da skill para deixar a intenção explícita.

Exemplos:

```text
Use a skill bug-investigator para investigar este erro de build.
```

```text
Crie uma branch e prepare o commit desta implementação.
```

```text
Gere um HANDOFF_CODEX.md para que eu continue este projeto em outro chat.
```

## Estrutura do repositório

```text
skills/
├── bug-investigator/
├── git-workflow/
└── handoff-context/
```

Cada pasta de skill possui um arquivo `SKILL.md`, que contém as instruções e os critérios de acionamento. Algumas também incluem configurações complementares em `agents/`.

## Contribuições

Sugestões, melhorias e novas skills são bem-vindas. Abra uma issue ou envie um pull request com uma explicação clara do caso de uso.

Minha intenção é continuar trazendo novas skills para esta coleção.
