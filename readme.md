# Minhas Skills para Codex

Uma coleção de skills em português para tornar o trabalho com o Codex mais consistente em tarefas de investigação, revisão e continuidade de projetos.

Cada skill contém instruções que orientam o agente sobre quando agir, quais cuidados tomar e como estruturar a resposta.

## Skills disponíveis

| Skill | Para que serve | Exemplos de pedido |
| --- | --- | --- |
| `bug-investigator` | Investiga bugs, falhas em testes, regressões, erros de build e comportamentos inesperados antes de propor uma correção. | “Investigue por que este teste falha.” / “Descubra a causa deste erro.” |
| `handoff-generator` | Cria ou atualiza um `HANDOFF_CODEX.md` com o contexto técnico necessário para continuar o trabalho em outra conversa. | “Gere um handoff.” / “Prepare o contexto para um novo chat.” |
| `review-quality` | Revisa alterações recentes ou o projeto inteiro quanto a qualidade, organização, arquitetura, testes e prontidão para commit. | “Revise minhas alterações antes do commit.” / “Faça uma revisão geral do projeto.” |
| `review-security` | Faz uma revisão defensiva de segurança de alterações ou do projeto, cobrindo riscos como autenticação, autorização, secrets e vulnerabilidades comuns. | “Revise a segurança deste PR.” / “Faça uma auditoria de segurança do projeto.” |

## Como instalar

1. Clone este repositório:

   ```bash
   git clone https://github.com/SEU-USUARIO/my-skills.git
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
Revise as alterações atuais antes de eu fazer commit.
```

```text
Gere um HANDOFF_CODEX.md para que eu continue este projeto em outro chat.
```

```text
Faça uma revisão de segurança completa deste projeto.
```

## Estrutura do repositório

```text
skills/
├── bug-investigator/
├── handoff-generator/
├── review-quality/
└── review-security/
```

Cada pasta de skill possui um arquivo `SKILL.md`, que contém as instruções e os critérios de acionamento. Algumas também incluem configurações complementares em `agents/`.

## Contribuições

Sugestões, melhorias e novas skills são bem-vindas. Abra uma issue ou envie um pull request com uma explicação clara do caso de uso.

Minha intenção é continuar trazendo novas skills para esta coleção.
