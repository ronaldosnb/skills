---
name: review-security
description: Use esta skill para revisão defensiva de segurança, cybersegurança, análise de vulnerabilidades, revisão segura de git diff, alterações antes de commit, auditoria de projeto, autenticação, autorização, secrets, variáveis de ambiente, OWASP, dependências, CORS, SQL injection, XSS, SSRF, RCE, logs sensíveis, LGPD e hardening. Acione quando o usuário pedir revisão de segurança de mudanças, PR, código novo, endpoint novo, rota nova, feature nova, projeto inteiro, auditoria, threat model, superfície de ataque, arquitetura segura ou segurança geral da aplicação.
---

# Revisão de Segurança e Cybersegurança

Realizar uma revisão defensiva de segurança do código em um de dois modos:

1. Revisão de segurança das alterações recentes.
2. Revisão de segurança do projeto inteiro.

Decidir automaticamente o modo com base no pedido do usuário.

## Escopo Permitido

Esta skill é exclusivamente defensiva.

Pode identificar vulnerabilidades, explicar riscos, sugerir correções, propor hardening, melhorar validações, revisar configurações, analisar dependências, revisar autenticação e autorização, revisar tratamento de secrets e revisar exposição de dados sensíveis.

Não deve ensinar exploração ofensiva, criar payloads para ataque real, orientar invasão, burlar autenticação, extrair dados de terceiros, automatizar exploração, criar malware, spyware, backdoor ou persistência.

## Decisão de Modo

Usar o modo "segurança das alterações" quando o pedido mencionar alterações, mudanças, diff, staged, commit, antes de commitar, revisão de segurança do que alterei, git diff, PR, pull request, última implementação, código novo, endpoint novo, rota nova ou feature nova.

Usar o modo "segurança do projeto inteiro" quando o pedido mencionar segurança geral, cybersegurança do projeto, auditoria do projeto, projeto inteiro, revisão completa, hardening, threat model, superfície de ataque, arquitetura segura, pentest interno defensivo, OWASP, LGPD ou segurança da aplicação.

Em caso de ambiguidade:

- Se houver alterações não commitadas no Git, priorizar "segurança das alterações".
- Se não houver alterações relevantes, usar "segurança do projeto inteiro".
- Explicar o modo escolhido no começo da resposta.

## Modo 1: Revisão de Segurança das Alterações

Analisar se as alterações recentes introduzem vulnerabilidades, vazamento de dados, exposição indevida, falhas de validação ou problemas de configuração.

### Processo

1. Inspecionar o estado do Git:
   - `git status --short`
   - `git diff --stat`
   - `git diff`
   - `git diff --staged --stat`
   - `git diff --staged`
2. Identificar partes afetadas: rotas, controllers, services, models, migrations, autenticação, autorização, uploads, integrações externas, banco de dados, variáveis de ambiente, Docker, CI/CD, infraestrutura e logs.
3. Verificar riscos comuns: secrets commitados, tokens/senhas/chaves/credenciais em código, `.env` exposto, validação insuficiente, SQL injection, NoSQL injection, command injection, path traversal, SSRF, XSS, CSRF, IDOR, mass assignment, falhas de autenticação/autorização, CORS permissivo, logs com dados sensíveis, upload inseguro, stack trace exposto, tratamento fraco de erros, dependências vulneráveis, permissões excessivas, endpoints administrativos expostos, dados pessoais desnecessários e quebra de isolamento entre usuários, empresas ou clientes.
4. Verificar se as alterações exigem testes de segurança ou regressão.
5. Não alterar arquivos automaticamente, a menos que o usuário peça explicitamente.

### Saída Obrigatória

```md
# Revisão de segurança das alterações

## Modo usado
Segurança das alterações recentes.

## Resumo das alterações analisadas

## Veredito de segurança
Escolha uma opção:
- Sem bloqueios aparentes
- Pode seguir com ajustes
- Não recomendado commitar ainda
- Bloqueado por risco crítico

## Achados de segurança

Classifique cada achado com:
- Severidade: Crítica, Alta, Média, Baixa ou Informativa
- Arquivo/caminho
- Descrição
- Impacto
- Recomendação
- Prioridade

## Pontos que parecem seguros

## Testes ou validações recomendadas

## Checklist antes do commit

## Sugestão de commit seguro

Se a revisão estiver ligada a alterações antes do commit, sugira mensagens de commit compatíveis com o que foi alterado.
```

### Severidade

- Crítica: credenciais expostas, bypass claro de autenticação, acesso indevido a dados de outros usuários/clientes, execução remota de código, injeção explorável em fluxo sensível ou vazamento direto de dados sensíveis.
- Alta: autorização fraca, validação ausente em entrada crítica, CORS muito permissivo com credenciais, upload inseguro, logs sensíveis em produção ou dependência vulnerável com impacto relevante.
- Média: erro de configuração, exposição excessiva de dados, tratamento de erro fraco, ausência de rate limit em fluxo sensível ou risco dependente de contexto.
- Baixa: melhoria de hardening, cabeçalhos de segurança ausentes, mensagens de erro melhoráveis ou pequenos ajustes preventivos.
- Informativa: observações, boas práticas ou itens a monitorar.

## Modo 2: Revisão de Cybersegurança do Projeto

Avaliar a segurança do projeto como um todo, incluindo arquitetura, fluxos sensíveis, autenticação, autorização, dados, infraestrutura, dependências e práticas de desenvolvimento seguro.

### Processo

1. Mapear a aplicação: tipo de aplicação, frameworks, entrypoints, rotas/endpoints, integrações externas, banco de dados, autenticação, autorização, armazenamento de arquivos, filas/jobs/RPAs, Docker/infraestrutura, CI/CD e ambiente de produção quando houver pistas no projeto.
2. Identificar ativos sensíveis: dados pessoais, financeiros, credenciais, tokens, documentos fiscais, informações de clientes, arquivos enviados, dados internos, logs e relatórios.
3. Avaliar superfície de ataque: endpoints públicos, painéis administrativos, APIs internas, webhooks, uploads, autenticação, integrações com terceiros, banco de dados, workers, scripts operacionais e deploy.
4. Verificar controles: autenticação, autorização por perfil/empresa/cliente, validação de entrada, sanitização de saída, criptografia em trânsito, criptografia em repouso quando aplicável, gestão de secrets, logs, auditoria, rate limiting, CORS, headers HTTP, tratamento de erros, backups, dependências, permissões de arquivos e princípio do menor privilégio.
5. Considerar riscos de LGPD quando houver dados pessoais ou dados de clientes.
6. Não executar testes intrusivos, exploração, fuzzing agressivo ou ataques contra sistemas externos.
7. Não alterar arquivos automaticamente, a menos que o usuário peça explicitamente.

### Saída Obrigatória

```md
# Revisão de cybersegurança do projeto

## Modo usado
Segurança do projeto inteiro.

## Visão geral da aplicação

## Ativos sensíveis identificados

## Superfície de ataque

## Principais riscos

Classifique por:
- Crítico
- Alto
- Médio
- Baixo
- Informativo

## Achados detalhados

Para cada achado:
- Severidade
- Área afetada
- Evidência no projeto
- Impacto
- Recomendação
- Prioridade

## Checklist OWASP adaptado ao projeto

Inclua somente itens relevantes ao projeto.

## Riscos de dados e LGPD

Quando aplicável, avalie:
- coleta excessiva
- exposição indevida
- retenção de dados
- logs sensíveis
- controle de acesso
- rastreabilidade

## Recomendações de hardening

Separe em:
1. Fazer agora
2. Fazer em seguida
3. Melhorias futuras

## Plano de correção seguro

Monte uma sequência objetiva de implementação.

## Sugestão para o próximo prompt

No final, sugira um prompt curto que o usuário possa enviar ao Codex para corrigir o risco mais importante.
```

## Checklist Base

Adaptar o checklist ao projeto e incluir somente itens relevantes.

- Autenticação: autenticação existente, proteção de tokens, hash forte de senhas, expiração de sessões, proteção de refresh tokens e defesa contra brute force.
- Autorização: usuários só acessam seus próprios dados, isolamento por empresa/cliente/tenant, endpoints administrativos exigem permissão adequada e IDs enviados pelo usuário são validados contra o usuário autenticado.
- Entrada e saída: validação de entrada, sanitização quando necessária, queries parametrizadas, erros sem stack trace e uploads com validação de tipo, tamanho e destino.
- Secrets: senhas/tokens/chaves fora do código, `.env` fora do Git, `.env.example` seguro e logs sem secrets.
- API e Web: CORS restrito, cookies com flags seguras quando aplicável, headers de segurança, rate limit em fluxos sensíveis e webhooks com assinatura validada.
- Banco de dados: queries parametrizadas, migrações sem exposição de dados, usuário do banco com permissões mínimas, backups considerados e dados sensíveis protegidos.
- Infraestrutura: Docker sem privilégios desnecessários, portas expostas necessárias, configurações de produção fortes, CI/CD sem vazamento de secrets e dependências verificadas.
- Logs e auditoria: logs sem dados sensíveis, ações críticas auditáveis, falhas de login/acesso indevido registradas e retenção adequada.

## Regras Gerais

- Ser defensivo e responsável.
- Não ensinar exploração ofensiva.
- Não gerar payloads de ataque real.
- Não inventar vulnerabilidades.
- Diferenciar evidência, hipótese e recomendação.
- Citar arquivos e caminhos reais quando possível.
- Não modificar arquivos sem pedido explícito.
- Priorizar riscos reais sobre checklist genérico.
- Explicar impacto de negócio quando fizer sentido.
- Para projetos com dados contábeis, financeiros, fiscais ou de clientes, tratar confidencialidade e controle de acesso como prioridade alta.
