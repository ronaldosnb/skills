---
name: handoff-context
description: Use esta skill para preparar contexto de continuidade entre conversas, gerar resumo técnico para novo chat, consolidar estado do projeto, registrar decisões, pendências, próximos passos, comandos úteis e riscos. Acione quando o usuário mencionar handoff, contexto cheio, continuar em outro chat, resumir contexto, preparar continuidade, criar contexto para outro agente, documentar estado atual ou gerar/atualizar HANDOFF_CODEX.md.
---

# Handoff Context

Preparar um contexto factual, compacto e acionável para que outro agente ou outra conversa continue o trabalho sem depender do histórico anterior.

## Objetivo

Gerar um handoff técnico que preserve:

- objetivo atual;
- estado real do repositório;
- arquitetura e arquivos relevantes;
- mudanças feitas;
- decisões técnicas;
- problemas encontrados;
- pendências;
- próximos passos;
- validações executadas ou não executadas.

## Modo de Saída

Decidir a saída pelo pedido do usuário:

- Se o usuário pedir arquivo, criar ou atualizar `HANDOFF_CODEX.md` na raiz do projeto.
- Se o usuário pedir resumo para colar em outro chat, responder no chat sem criar arquivo.
- Se o pedido for ambíguo, preferir criar ou atualizar `HANDOFF_CODEX.md` quando houver um repositório local claro; caso contrário, entregar resumo no chat.

Não modificar código, configuração, dados da aplicação ou outros arquivos sem pedido explícito.

## Processo

1. Localizar a raiz do projeto. Preferir o diretório atual informado pelo ambiente; confirmar com `git rev-parse --show-toplevel` quando Git estiver disponível.
2. Inspecionar o estado atual usando comandos de leitura:
   - `git status --short`
   - `git branch --show-current`
   - `git log -n 10 --oneline`
   - `git diff --stat`
   - `rg --files`
3. Ler o handoff existente, se houver, para preservar contexto ainda válido e remover conteúdo obsoleto.
4. Ler arquivos relevantes que existirem:
   - `README.md`, `AGENTS.md` e documentos equivalentes de orientação;
   - manifestos e locks, como `package.json`, `pnpm-lock.yaml`, `yarn.lock`, `package-lock.json`, `requirements.txt`, `pyproject.toml`, `go.mod`, `Cargo.toml` ou equivalentes;
   - arquivos de build, lint, teste, TypeScript, framework e CI;
   - infraestrutura, como `Dockerfile`, `docker-compose.yml`, `compose.yaml` e workflows;
   - entrypoints, rotas, módulos principais e arquivos relacionados ao trabalho atual;
   - diffs locais necessários para separar trabalho concluído de pendências.
5. Inferir arquitetura e estado atual somente a partir de evidências observadas.
6. Marcar qualquer conclusão não confirmada como `incerto`.
7. Registrar comandos de validação realmente executados e resultados observados. Se algo não foi executado, declarar `não executado`.
8. Revisar o handoff contra o estado Git e os arquivos lidos antes de finalizar.

## Conteúdo Obrigatório

Quando criar ou atualizar `HANDOFF_CODEX.md`, escrever os títulos exatamente nesta ordem:

```markdown
# Handoff do projeto

## Objetivo geral

## Estado atual do repositório

## Estrutura relevante

## O que já foi feito

## Decisões técnicas

## Dados analisados

## Problemas encontrados

## Pendências

## Próximos passos recomendados

## Cuidados para o próximo chat

## Comandos úteis

## Critérios de validação

## Resumo rápido para colar no novo chat
```

Para resumo no chat, usar a mesma estrutura quando couber, mas condensar para facilitar leitura.

## Regras de Conteúdo

- Priorizar informação útil para continuidade: objetivo, arquivos relevantes, decisões, pendências, riscos, comandos e validação.
- Diferenciar fato observado, hipótese, decisão tomada e recomendação.
- Em `Dados analisados`, listar os caminhos realmente lidos e o que cada um confirmou.
- Em `Estado atual do repositório`, registrar branch, alterações locais relevantes e situação de build/testes quando disponíveis.
- Em `O que já foi feito`, incluir somente mudanças confirmadas por código, Git, documentos ou comandos.
- Em `Problemas encontrados`, registrar erros reproduzidos ou evidências concretas; marcar hipóteses como `incerto`.
- Em `Pendências`, manter itens específicos, verificáveis e acionáveis.
- Em `Comandos úteis`, incluir apenas comandos existentes no projeto ou comandos de inspeção aplicáveis.
- Em `Critérios de validação`, explicar como o próximo agente deve confirmar que o trabalho está correto.
- Fazer `Resumo rápido para colar no novo chat` ter entre 10 e 20 linhas não vazias quando o contexto do projeto permitir.
- Evitar despejar arquivos inteiros, logs extensos, artefatos gerados ou detalhes sem impacto na continuidade.

## Restrições

- Não alterar código, configuração ou dados da aplicação.
- Não instalar, remover ou atualizar dependências.
- Não executar migrações, deploys, comandos destrutivos ou tarefas que modifiquem dados.
- Não reverter, formatar ou sobrescrever alterações existentes.
- Não inventar resultados de testes, decisões, causas de bugs ou trabalho concluído.
- Não copiar segredos, credenciais, tokens ou valores de `.env`.
- Ler preferencialmente `.env.example`; quando for necessário mencionar configuração secreta, registrar somente o nome da variável.
- Não incluir dados pessoais ou conteúdo sensível de logs e dados operacionais.

## Conclusão

Ao finalizar, informar:

- se entregou resumo no chat ou criou/atualizou arquivo;
- caminho absoluto do arquivo quando houver;
- principais dados inspecionados;
- validações feitas;
- itens relevantes que permaneceram `incerto`.
