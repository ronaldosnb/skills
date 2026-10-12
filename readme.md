# Minhas Skills para Codex

Uma coleção de skills em português para tornar o trabalho com o Codex mais consistente em tarefas de investigação, Git e continuidade de projetos.

Cada skill contém instruções que orientam o agente sobre quando agir, quais cuidados tomar e como estruturar a resposta.

## Skills disponíveis

| Skill | Para que serve | Exemplos de pedido |
| --- | --- | --- |
| `bug-investigator` | Investiga bugs, falhas em testes, regressões, erros de build e comportamentos inesperados antes de propor uma correção. | “Investigue por que este teste falha.” / “Descubra a causa deste erro.” |
| `git-workflow` | Aplica o fluxo pessoal de Git: branches e commits em português, convenções de nomenclatura e nenhuma integração automática. | “Crie uma branch para esta implementação.” / “Prepare o commit.” |
| `handoff-context` | Prepara o contexto técnico para continuar o trabalho em outra conversa, como resumo no chat ou em um `HANDOFF_CODEX.md`. | “Gere um handoff.” / “Prepare o contexto para um novo chat.” |

## Como instalar

A forma mais simples é usar a CLI [`skills`](https://github.com/vercel-labs/skills), que exige apenas Node.js. Ela instala por symlink, funciona com vários agentes (Codex, Claude Code e outros) e permite atualizar depois.

Instalar todas as skills deste repositório:

```bash
npx skills add ronaldosnb/skills -g --skill '*'
```

Instalar apenas uma:

```bash
npx skills add ronaldosnb/skills -g --skill bug-investigator
```

Comandos úteis depois da instalação:

```bash
npx skills list -g     # mostra o que está instalado
npx skills update -g   # atualiza para a versão mais recente
```

Use `-a <agente>` para escolher em quais agentes instalar. Reinicie o agente ou inicie uma nova conversa para que ele carregue as novas skills.

### Instalação manual

Se preferir não usar a CLI, clone o repositório e copie as pastas desejadas:

```bash
git clone https://github.com/ronaldosnb/skills.git
mkdir -p ~/.codex/skills
cp -R skills/skills/* ~/.codex/skills/
```

## Skills de terceiros

| Skill | Fonte | Onde está | Para que serve |
| --- | --- | --- | --- |
| `impeccable` | [pbakaus/impeccable](https://github.com/pbakaus/impeccable) (Apache 2.0) | Cópia em `skills/impeccable/` | Design, crítica e polimento de interfaces frontend. |
| `grill-with-docs` | [mattpocock/skills](https://github.com/mattpocock/skills) | Fora deste repositório | Entrevista para refinar um plano ou design, gerando ADRs e glossário. |

A `impeccable` é instalada junto com as demais skills deste repositório. A `grill-with-docs` deve ser instalada a partir da fonte original; leia o conteúdo antes de instalar:

```bash
npx skills add mattpocock/skills -g --skill grill-with-docs grilling domain-modeling
```

Ela depende das skills `grilling` e `domain-modeling`, do mesmo repositório; por isso as três são instaladas juntas.

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
├── handoff-context/
└── impeccable/
```

Cada pasta de skill possui um arquivo `SKILL.md`, que contém as instruções e os critérios de acionamento. Algumas também incluem configurações complementares em `agents/`.

## Contribuições

Sugestões, melhorias e novas skills são bem-vindas. Abra uma issue ou envie um pull request com uma explicação clara do caso de uso.

Minha intenção é continuar trazendo novas skills para esta coleção.
