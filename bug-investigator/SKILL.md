---
name: bug-investigator
description: Use esta skill para investigar bugs, erros, regressões, falhas em testes, comportamento inesperado, crash, exceções, logs de erro, problemas de build, lint, typecheck, integração, deploy local, diferenças entre esperado e observado, causa raiz e plano de correção. Acione quando o usuário pedir para descobrir por que algo falha, analisar um erro, investigar um bug, reproduzir problema, comparar comportamento esperado/atual, diagnosticar regressão ou validar uma hipótese de bug.
---

# Bug Investigator

Investigar bugs de forma metódica, factual e reproduzível antes de propor ou aplicar correções.

## Objetivo

Entender o problema real, localizar a causa raiz provável e indicar uma correção segura com validação objetiva.

Trabalhar em três modos:

1. Investigação sem alteração de arquivos.
2. Investigação com correção, quando o usuário pedir explicitamente para corrigir.
3. Investigação de falha de validação, quando o ponto de partida for teste, lint, typecheck, build ou comando quebrando.

## Decisão de Modo

- Usar investigação sem alteração quando o usuário pedir para analisar, diagnosticar, descobrir causa, explicar erro ou investigar.
- Usar investigação com correção quando o usuário pedir para corrigir, consertar, implementar fix ou resolver.
- Usar investigação de falha de validação quando o pedido trouxer saída de teste/lint/typecheck/build, stack trace, log de erro ou comando específico falhando.

Em caso de ambiguidade, investigar primeiro sem editar arquivos. Não fazer perguntas desnecessárias quando o repositório, logs ou testes permitirem avançar.

## Processo

1. Capturar o relato do bug:
   - comportamento observado;
   - comportamento esperado;
   - ambiente ou comando afetado;
   - mensagens de erro, stack traces ou logs;
   - quando começou, se houver pista.
2. Inspecionar contexto local:
   - `git status --short`;
   - `git diff --stat`;
   - arquivos citados pelo usuário;
   - arquivos citados por stack traces;
   - testes ou comandos relacionados;
   - configuração do framework, build, lint ou runtime quando relevante.
3. Reproduzir de forma mínima quando possível:
   - executar o comando falho indicado pelo usuário;
   - executar teste específico antes de suíte ampla;
   - reduzir escopo antes de rodar comandos caros;
   - não executar comandos destrutivos, deploys, migrações ou operações contra produção.
4. Formular hipóteses a partir de evidência, não de intuição genérica.
5. Validar ou descartar hipóteses lendo código, executando comandos seguros e comparando fluxo real com esperado.
6. Identificar causa raiz provável:
   - arquivo e trecho afetado;
   - condição que dispara o bug;
   - por que o comportamento ocorre;
   - impacto provável;
   - risco de regressão.
7. Se o usuário pediu correção, editar somente os arquivos necessários e preservar mudanças não relacionadas.
8. Validar a correção com o menor conjunto confiável de testes/comandos.
9. Se não for possível reproduzir ou confirmar, declarar claramente o que ficou `incerto` e qual evidência falta.

## Regras de Investigação

- Priorizar evidência concreta: logs, testes, stack traces, diffs, código e configuração.
- Diferenciar fato observado, hipótese, inferência e recomendação.
- Não inventar causa raiz.
- Não tratar sintoma como causa.
- Não mudar arquivos automaticamente sem pedido explícito de correção.
- Não reverter alterações do usuário.
- Não rodar comandos destrutivos, migrações, deploys ou ações externas sem pedido claro.
- Preferir comandos específicos a suítes inteiras quando o escopo do bug for claro.
- Se um comando puder ser caro, explicar rapidamente o motivo antes de rodar.
- Ao corrigir, manter o patch pequeno e alinhado aos padrões do projeto.
- Adicionar ou ajustar testes quando isso for o jeito mais direto de prevenir regressão.

## O Que Procurar

- Condicionais invertidas ou incompletas.
- Tipos incorretos, valores `null`/`undefined`/vazios e conversões implícitas.
- Mudanças de contrato entre camadas, APIs, DTOs, models e banco.
- Corridas assíncronas, promises não aguardadas e estado desatualizado.
- Erros de serialização, parsing, timezone, encoding e locale.
- Validação ausente ou validação divergente entre frontend/backend.
- Cache, memoização ou invalidação incorreta.
- Query incorreta, filtros faltando, joins errados ou paginação quebrada.
- Dependências, configuração, variáveis de ambiente ou scripts inconsistentes.
- Testes frágeis, mocks incompletos ou fixtures desatualizadas.
- Regressões introduzidas por diffs recentes.

## Saída Para Investigação Sem Correção

Responder com:

```md
# Investigação do bug

## Resumo do problema

## Evidências analisadas

## Reprodução

## Hipóteses avaliadas

## Causa raiz provável

## Impacto

## Correção recomendada

## Validação recomendada

## O que permanece incerto
```

## Saída Para Investigação Com Correção

Responder com:

```md
# Bug corrigido

## Resumo do problema

## Causa raiz

## Alterações feitas

## Validação executada

## Riscos restantes

## Arquivos alterados
```

## Saída Para Falha de Validação

Responder com:

```md
# Investigação da falha

## Comando que falhou

## Erro observado

## Causa raiz provável

## Correção aplicada ou recomendada

## Comandos executados

## Resultado final

## Pendências
```

## Critérios de Conclusão

Uma investigação está concluída quando pelo menos um destes pontos for verdadeiro:

- a causa raiz foi localizada com evidência suficiente e há plano de correção;
- a correção foi aplicada e validada por comando relevante;
- o bug não pôde ser reproduzido, mas foram documentadas as tentativas, evidências e lacunas;
- a investigação depende de dado externo indisponível, e isso foi declarado objetivamente.
