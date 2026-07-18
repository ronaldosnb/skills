---
name: handoff-generator
description: Gera ou atualiza HANDOFF_CODEX.md na raiz de um projeto com o estado técnico necessário para continuar o trabalho em outra conversa. Use quando o usuário disser "gerar handoff", "contexto cheio", "resumir contexto para novo chat", "preparar continuidade", pedir um resumo para outra conversa ou solicitar a criação ou atualização de HANDOFF_CODEX.md.
---

# Handoff Generator

Gerar um retrato factual e acionável do projeto para que outro agente continue o trabalho sem depender do histórico da conversa.

## Fluxo

1. Localizar a raiz do repositório. Preferir a raiz indicada pelo ambiente; confirmar com `git rev-parse --show-toplevel` quando Git estiver disponível.
2. Inspecionar o repositório antes de escrever. Usar comandos somente de leitura e priorizar `rg --files`, `git status --short`, `git branch --show-current`, `git log -n 10 --oneline` e `git diff --stat`.
3. Ler o `HANDOFF_CODEX.md` existente, se houver, para preservar contexto ainda válido e remover informações obsoletas.
4. Ler os arquivos relevantes que existirem:
   - `README.md`, `AGENTS.md` e arquivos equivalentes de orientação;
   - manifestos e locks, como `package.json`, `pnpm-lock.yaml`, `yarn.lock`, `package-lock.json`, `requirements.txt` e `pyproject.toml`;
   - infraestrutura, como `docker-compose.yml`, `compose.yaml`, `Dockerfile` e arquivos de CI;
   - banco e configuração, como `prisma/schema.prisma`, `.env.example`, configurações de framework, build, lint e TypeScript;
   - código, rotas, módulos e arquivos diretamente relacionados ao trabalho atual;
   - documentação, histórico Git e diffs locais necessários para distinguir trabalho concluído de trabalho pendente.
5. Inferir a arquitetura e o estado atual somente a partir de evidências observadas. Marcar qualquer conclusão não confirmada como `incerto`.
6. Criar ou atualizar apenas `HANDOFF_CODEX.md` na raiz do projeto, usando exatamente as seções obrigatórias abaixo.
7. Revisar o documento contra os arquivos e o estado Git atuais. Confirmar que caminhos, comandos, pendências e validações são reais.

## Regras De Conteúdo

- Priorizar informações que permitam a outro agente retomar a tarefa: objetivo, arquitetura, arquivos relevantes, mudanças locais, decisões, problemas, pendências, próximos passos e validação.
- Distinguir claramente fatos observados, decisões já tomadas, trabalho concluído e recomendações.
- Em `Dados analisados`, listar os caminhos efetivamente lidos e indicar brevemente o que cada um confirmou.
- Em `Estado atual do repositório`, registrar branch, alterações locais relevantes e situação de build/testes quando essas informações estiverem disponíveis.
- Em `O que já foi feito`, incluir somente mudanças confirmadas pelo código, Git, documentos ou resultados de comandos.
- Em `Problemas encontrados`, registrar erros reproduzidos ou evidências concretas. Marcar hipóteses como `incerto`.
- Em `Pendências`, manter itens específicos e verificáveis.
- Em `Comandos úteis`, incluir apenas comandos existentes no projeto ou comandos de inspeção aplicáveis.
- Em `Critérios de validação`, explicar como o próximo agente deve confirmar que o trabalho está correto.
- Fazer a seção `Resumo rápido para colar no novo chat` ter entre 10 e 20 linhas não vazias, com contexto suficiente para iniciar outra conversa.
- Ser completo, mas evitar despejar arquivos inteiros, logs extensos, artefatos gerados ou detalhes sem impacto na continuidade.

## Restrições

- Não alterar código, configuração ou dados da aplicação.
- Não instalar ou atualizar dependências.
- Não executar migrações, deploys, comandos destrutivos ou tarefas que modifiquem dados.
- Não reverter, formatar ou sobrescrever alterações existentes.
- Não inventar resultados de testes, decisões, causas de bugs ou trabalho concluído.
- Não copiar segredos, credenciais, tokens ou valores de `.env`. Ler preferencialmente `.env.example`; quando for necessário mencionar configuração secreta, registrar somente o nome da variável.
- Não incluir dados pessoais ou conteúdo sensível de logs e dados operacionais.
- Se um comando de validação não foi executado, declarar explicitamente `não executado`.

## Estrutura Obrigatória

Escrever os títulos exatamente nesta ordem:

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

## Conclusão

Após escrever, informar:

- o caminho absoluto de `HANDOFF_CODEX.md`;
- se o arquivo foi criado ou atualizado;
- quais verificações foram feitas;
- qualquer informação relevante que permaneceu `incerto`.
