---
name: review-quality
description: Use esta skill para revisar qualidade de código, organização, arquitetura, coerência do projeto, alterações antes de commit, git diff, staged changes, revisão geral do projeto, refatoração, padrões, legibilidade, testes e sugestão de mensagem de commit. Acione quando o usuário pedir revisão de mudanças, revisão antes de commitar, análise de PR, git status/diff, revisão da última implementação, revisão geral do projeto, arquitetura, organização, codebase, dívida técnica, manutenibilidade ou qualidade geral.
---

# Revisão de Qualidade e Coerência

Realizar uma revisão técnica de qualidade do código em um de dois modos:

1. Revisão das alterações recentes antes de um commit.
2. Revisão geral do projeto inteiro.

Decidir automaticamente o modo com base no pedido do usuário.

## Decisão de Modo

Usar o modo "alterações antes do commit" quando o pedido mencionar alterações, mudanças, diff, staged, commit, antes de commitar, revisão antes do commit, revise o que alterei, git diff, git status, PR, pull request, última implementação ou o que foi feito agora.

Usar o modo "revisão geral do projeto" quando o pedido mencionar projeto inteiro, revisão geral, arquitetura, organização, estrutura, qualidade geral, codebase, padrões do projeto, escalabilidade, manutenibilidade, coerência geral ou dívida técnica.

Em caso de ambiguidade:

- Se o repositório tiver alterações não commitadas, priorizar "alterações antes do commit".
- Se não houver alterações relevantes no Git, usar "revisão geral do projeto".
- Não fazer perguntas desnecessárias. Tomar uma decisão razoável, explicar o modo usado e seguir.

## Modo 1: Alterações Antes do Commit

Verificar se as alterações recentes são coerentes, seguras do ponto de vista de qualidade, bem organizadas e prontas para commit. Sugerir uma ou mais mensagens de commit.

### Processo

1. Inspecionar o estado do Git:
   - `git status --short`
   - `git diff --stat`
   - `git diff`
   - `git diff --staged --stat`
   - `git diff --staged`
2. Identificar arquivos criados, alterados, removidos, alterações staged e unstaged, e o objetivo provável da mudança.
3. Avaliar se as alterações são coerentes com o objetivo aparente.
4. Procurar problemas de arquivos esquecidos, código morto, logs temporários, comentários de debug, duplicação, nomes ruins, excesso de responsabilidade, acoplamento desnecessário, inconsistência com padrões existentes, alterações grandes demais para um único commit, falta de testes, documentação desatualizada e impacto em build, lint, tipos ou testes.
5. Quando possível, rodar comandos de validação existentes: testes, lint, typecheck, build e formatação. Antes de rodar comandos potencialmente caros ou destrutivos, explicar o motivo.
6. Não alterar arquivos automaticamente, a menos que o usuário peça explicitamente.

### Saída Obrigatória

```md
# Revisão das alterações

## Modo usado
Alterações antes do commit.

## Resumo do que mudou

## Veredito
Escolha uma opção:
- Pronto para commit
- Quase pronto, com ajustes pequenos
- Não recomendado commitar ainda

## Pontos positivos

## Problemas encontrados

Separe por severidade:
- Crítico
- Alto
- Médio
- Baixo
- Observação

## Ajustes recomendados antes do commit

## Testes e validações

Informe:
- comandos executados
- resultado dos comandos
- comandos que não foram executados e por quê

## Sugestões de commit

Dê de 1 a 5 sugestões de mensagem de commit.

Preferir Conventional Commits quando fizer sentido:
- feat:
- fix:
- refactor:
- chore:
- docs:
- test:
- perf:
- build:
- ci:

## Melhor sugestão

Escolha uma mensagem principal e explique rapidamente por quê.
```

### Regras de Commit

- A mensagem deve refletir exatamente o que mudou.
- Não inventar escopo que não aparece nas alterações.
- Se houver múltiplas mudanças independentes, sugerir dividir em commits menores.
- Se as alterações forem só organização, preferir `refactor:` ou `chore:`.
- Se corrigirem bug, preferir `fix:`.
- Se adicionarem funcionalidade, preferir `feat:`.
- Se alterarem documentação, preferir `docs:`.
- Se adicionarem ou corrigirem testes, preferir `test:`.

## Modo 2: Revisão Geral do Projeto

Avaliar o projeto como um todo, considerando organização, arquitetura, qualidade, coerência, manutenibilidade, padrões e riscos técnicos.

### Processo

1. Inspecionar a estrutura do projeto: árvore de diretórios, arquivos de configuração, documentação, dependências, scripts, testes e organização por domínio, feature ou camada.
2. Ler arquivos importantes quando existirem: `README`, `AGENTS.md`, `package.json`, `pyproject.toml`, `requirements.txt`, `pom.xml`, `go.mod` ou equivalentes, configurações de build/lint/test, entrypoints da aplicação, módulos principais, rotas, controllers, services e models.
3. Identificar a arquitetura real do projeto, não a arquitetura idealizada.
4. Avaliar clareza da estrutura, separação de responsabilidades, consistência de nomes, duplicações, acoplamento, complexidade desnecessária, ausência de testes, documentação insuficiente, scripts ausentes, dependências mal utilizadas, arquivos mortos ou temporários, padrões inconsistentes e riscos de manutenção futura.
5. Não reestruturar arquivos automaticamente, a menos que o usuário peça explicitamente.

### Saída Obrigatória

```md
# Revisão geral do projeto

## Modo usado
Revisão geral do projeto.

## Diagnóstico geral

## Pontos fortes

## Problemas por categoria

### Arquitetura

### Organização de pastas

### Qualidade de código

### Testes

### Documentação

### Build, scripts e ambiente

### Manutenibilidade

## Riscos técnicos

Classifique por:
- Crítico
- Alto
- Médio
- Baixo

## Recomendações priorizadas

Separe em:
1. Fazer agora
2. Fazer depois
3. Melhorias opcionais

## Roadmap de melhoria

Monte uma sequência objetiva de próximos passos.

## Sugestão para o próximo prompt

No final, sugira um prompt curto que o usuário possa enviar ao Codex para executar a próxima melhoria.
```

## Regras Gerais

- Ser direto, técnico e prático.
- Não elogiar genericamente.
- Não inventar problemas.
- Citar caminhos reais de arquivos quando possível.
- Diferenciar fato, hipótese e recomendação.
- Não modificar arquivos sem pedido explícito.
- Quando encontrar algo grave, explicar o impacto.
- Quando sugerir melhoria, dizer onde aplicar.
- Se a revisão for grande, priorizar os achados mais importantes.
- Evitar microcomentários irrelevantes.
- Focar no que ajuda o usuário a decidir o próximo passo.
