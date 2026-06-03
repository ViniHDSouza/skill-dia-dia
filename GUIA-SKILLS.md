# Guia Prático das 16 Skills Instaladas

> Situações reais do dia a dia e exemplos concretos de como usar cada skill.
> Fontes: [pedronauck/skills](https://github.com/pedronauck/skills), [rodrigobranas/iadevt6_2](https://github.com/rodrigobranas/iadevt6_2)

---

## 1. systematic-debugging

**O que faz:** Metodologia de debugging em 4 fases — observar, instrumentar, isolar, corrigir. A regra central: nenhuma correção sem causa raiz identificada primeiro.

### Situações reais

**Situação A — Teste de integração falhando com timeout:**
Você roda os testes e um teste de integração que chamava o serviço de pagamentos começa a falhar com timeout. A tentação é aumentar o timeout de 5s para 30s. A skill impede isso e guia a investigação real.

```
Prompt para o agente:
"O teste PaymentServiceIntegrationTest está falhando com timeout.
Use systematic-debugging para investigar. Não proponha nenhuma
correção até identificar a causa raiz."
```

**Situação B — Bug em produção que não reproduz localmente:**
Clientes reportam erro 500 esporádico no endpoint de login. Na sua máquina funciona.

```
Prompt para o agente:
"Temos erro 500 intermitente no POST /api/auth/login em produção
mas não reproduz localmente. Siga as 4 fases do systematic-debugging:
observe os logs de produção, instrumente as fronteiras de componente,
isole onde o fluxo quebra, e só então proponha a correção."
```

**Situação C — Build do CI quebrou sem ninguém ter feito mudança:**
O pipeline de CI que passava ontem agora falha no step de testes.

```
Prompt para o agente:
"O CI quebrou no step de testes unitários. Nenhum commit novo foi
feito desde ontem. Investigue sistematicamente: pode ser dependência
atualizada, variável de ambiente, expiração de token, ou mudança
de infra. Cause raiz primeiro."
```

---

## 2. no-workarounds

**O que faz:** Bloqueia gambiarras e exige que toda correção ataque a causa raiz. Impede patches temporários que viram permanentes.

### Situações reais

**Situação A — Dev quer colocar try/catch genérico:**
Uma NullPointerException aparece em produção. A "solução rápida" seria colocar um try/catch que loga e segue em frente.

```
Prompt para o agente:
"Estamos recebendo NullPointerException no OrderService.calculateTotal().
Não quero um try/catch genérico. Descubra por que o campo é null e
corrija na origem."
```

**Situação B — Feature toggle para contornar bug:**
Em vez de corrigir um bug no cálculo de desconto, alguém sugere criar um feature toggle para desabilitar descontos temporariamente.

```
Prompt para o agente:
"O cálculo de desconto para clientes premium está retornando valor
negativo em pedidos acima de R$10.000. Corrija a lógica de cálculo.
Não quero feature toggle, flag booleana ou qualquer contorno."
```

**Situação C — Duplicar código para evitar refatorar:**
Um método utilitário está em um módulo difícil de importar. A "solução" seria copiar o método.

```
Prompt para o agente:
"Preciso usar o método DateUtils.parseISODate() no módulo de relatórios,
mas ele está no módulo core que tem dependência circular. Resolva a
dependência circular, não duplique o código."
```

---

## 3. verification-before-completion

**O que faz:** Exige execução dos comandos de verificação do projeto e confirmação da saída antes de marcar qualquer tarefa como concluída.

### Situações reais

**Situação A — Refatoração de um serviço:**
Você refatorou o UserService para extrair a lógica de validação. Parece correto, mas sem rodar os testes não dá pra saber.

```
Prompt para o agente:
"Refatore o UserService extraindo a validação para um ValidatorService.
Antes de considerar pronto, execute:
- mvn test (Java) / dotnet test (C#) / go test ./... (Go)
- O lint do projeto
- Confirme que todos passam com output real."
```

**Situação B — Adição de novo endpoint:**
Você criou um novo endpoint REST. O código compila, mas você não testou.

```
Prompt para o agente:
"Crie o endpoint GET /api/v1/reports/{id}/summary.
Após implementar, execute os testes, faça uma chamada de teste
via curl, e mostre o output de cada verificação."
```

**Situação C — Atualização de dependência:**
Atualizar o Spring Boot de 3.1 para 3.2.

```
Prompt para o agente:
"Atualize o Spring Boot de 3.1.x para 3.2.x.
Após a atualização, execute './mvnw clean verify' e mostre o
output completo. Só considere pronto se TODOS os testes passarem."
```

---

## 4. find-rules

**O que faz:** Descobre automaticamente convenções do projeto — linters, formatters, .editorconfig, guidelines, CONTRIBUTING.md, etc.

### Situações reais

**Situação A — Primeiro dia em um projeto novo:**
Você foi alocado em um projeto que já existe há 2 anos. Não sabe os padrões.

```
Prompt para o agente:
"Acabei de entrar neste projeto. Descubra todas as convenções:
linters, formatters, coding standards, guidelines arquiteturais,
configurações de editorconfig, e qualquer regra documentada."
```

**Situação B — Contribuir para um projeto open source:**
Você quer fazer um PR para uma lib open source e não quer ter o PR rejeitado por estilo.

```
Prompt para o agente:
"Quero contribuir para este repositório. Antes de escrever qualquer
código, descubra as regras de contribuição: CONTRIBUTING.md,
convenções de commit, regras de lint, e padrões de código."
```

**Situação C — Auditoria de padronização entre microserviços:**

```
Prompt para o agente:
"Temos 5 microserviços. Analise as regras e convenções de cada um
e identifique inconsistências entre eles: linters diferentes,
formatters conflitantes, padrões divergentes."
```

---

## 5. writing-clearly-and-concisely

**O que faz:** Aplica regras de Strunk para escrita clara e concisa. Elimina voz passiva desnecessária, palavras redundantes e frases longas.

### Situações reais

**Situação A — Escrever descrição de PR:**
Seu PR tem 15 arquivos mudados e você precisa explicar o que foi feito.

```
Prompt para o agente:
"Escreva a descrição deste PR. O que mudou: extraí a lógica de
cálculo de frete do OrderController para um FreightCalculator,
adicionei testes unitários e corrigi o bug do cálculo para
regiões Norte e Nordeste. Aplique writing-clearly-and-concisely."
```

**Situação B — Documentar uma decisão arquitetural (ADR):**

```
Prompt para o agente:
"Escreva um ADR sobre a decisão de migrar de REST para gRPC na
comunicação entre os serviços de pedido e inventário. Motivação:
latência, contratos tipados, streaming. Escreva de forma clara
e concisa, sem enrolação."
```

**Situação C — Mensagem de commit:**

```
Prompt para o agente:
"Preciso de uma mensagem de commit para esta mudança: corrigi o bug
onde o cálculo de imposto não considerava produtos isentos na
categoria 'livros', causando cobrança indevida de 12% de ICMS.
Formato Conventional Commits, claro e direto."
```

---

## 6. requirements-clarity

**O que faz:** Identifica ambiguidades, contradições, requisitos faltantes e edge cases ocultos em requisitos antes de implementar.

### Situações reais

**Situação A — Ticket vago do Jira:**
Ticket diz: "Implementar sistema de notificações para os usuários."

```
Prompt para o agente:
"Recebi este requisito: 'Implementar sistema de notificações para
os usuários.' Use requirements-clarity para identificar tudo que
está faltando antes de eu começar a codar. Que perguntas eu deveria
fazer ao PO?"
```

A skill vai revelar questões como: Que tipo de notificação (email, push, in-app, SMS)? Tempo real ou batch? Quais eventos disparam notificação? O usuário pode configurar preferências? Existe limite de volume? Retry em caso de falha?

**Situação B — Requisito com contradição escondida:**
"O relatório deve ser gerado em tempo real e deve consolidar dados dos últimos 12 meses."

```
Prompt para o agente:
"Analise este requisito: 'Relatório em tempo real com dados
consolidados de 12 meses.' Identifique contradições e suposições
problemáticas."
```

**Situação C — Feature que parece simples mas não é:**
"Adicionar botão de 'desfazer' na tela de pedidos."

```
Prompt para o agente:
"O PO pediu um botão de 'desfazer' na tela de pedidos. Antes de
implementar, use requirements-clarity para mapear a complexidade
real: desfazer o quê? Até quando? E se o pedido já foi faturado?
E se o estoque já foi reservado?"
```

---

## 7. brainstorming

**O que faz:** Explora abordagens, restrições e trade-offs por meio de diálogo estruturado antes de se comprometer com uma direção.

### Situações reais

**Situação A — Escolher entre arquiteturas:**
Você precisa decidir se o novo módulo de mensageria será síncrono ou assíncrono.

```
Prompt para o agente:
"Preciso implementar comunicação entre o serviço de pedidos e o
serviço de estoque. Faça um brainstorming das opções:
REST síncrono, mensageria com RabbitMQ/Kafka, gRPC.
Para cada uma, liste trade-offs de performance, complexidade,
resiliência e manutenção."
```

**Situação B — Estratégia de cache:**

```
Prompt para o agente:
"Nosso endpoint de catálogo de produtos responde em 2s. Preciso
reduzir para <200ms. Brainstorming de estratégias: cache em
memória, Redis, CDN, materializar views no banco. Quais os
trade-offs de invalidação, consistência e custo de cada uma?"
```

**Situação C — Decidir entre buy vs build:**

```
Prompt para o agente:
"Precisamos de full-text search no sistema. Brainstorming:
implementar com ElasticSearch, usar o full-text do PostgreSQL,
ou contratar um SaaS como Algolia? Considere custo, complexidade
operacional, performance e time-to-market."
```

---

## 8. creating-spec

**O que faz:** Gera especificação técnica estruturada: contexto, solução proposta, design detalhado, API surface, plano de migração, riscos.

### Situações reais

**Situação A — Migração de autenticação:**

```
Prompt para o agente:
"Crie uma spec técnica para migrar nosso sistema de autenticação
de session-based (server-side sessions em Redis) para JWT
stateless. Inclua: contexto do problema, solução proposta,
design dos tokens (access + refresh), plano de migração sem
downtime, e riscos com mitigações."
```

**Situação B — Novo microserviço:**

```
Prompt para o agente:
"Crie uma spec para o novo serviço de notificações. Contexto:
hoje as notificações estão espalhadas em 4 microserviços.
Queremos centralizar. Spec deve cobrir: API surface (endpoints),
contratos, modelo de dados, integrações com email/push/SMS,
e como migrar gradualmente os 4 serviços."
```

**Situação C — RFC para o time:**

```
Prompt para o agente:
"Crie uma RFC propondo a adoção de feature flags com OpenFeature.
Formato: problema atual (deploys tudo-ou-nada), solução proposta,
SDKs por linguagem (Java/JS), estratégia de rollout, impacto
no pipeline de CI/CD, e riscos."
```

---

## 9. context7

**O que faz:** Busca documentação atualizada, referências de API e exemplos de código para qualquer biblioteca via Context7 CLI.

### Situações reais

**Situação A — Verificar API de uma lib antes de usar:**
Você quer usar o novo `HttpClient` do Java 21 mas não lembra a API exata.

```
Prompt para o agente:
"Use context7 para buscar a documentação atualizada do
java.net.http.HttpClient no Java 21. Preciso de exemplos de
requisição GET/POST com timeout e tratamento de erro."
```

**Situação B — Conferir breaking changes após update:**

```
Prompt para o agente:
"Atualizei o Spring Boot para 3.3. Use context7 para buscar
as notas de release e breaking changes. Preciso saber se algo
mudou em relação a auto-configuration, security filters ou
propriedades do application.yml."
```

**Situação C — Aprender lib nova rapidamente:**

```
Prompt para o agente:
"Preciso implementar rate limiting na API. Use context7 para
buscar a documentação do Bucket4j (Java) com exemplos de
configuração, integração com Spring Boot e estratégias de
rate limit por IP e por API key."
```

**Situação D — Verificar sintaxe correta de configuração:**

```
Prompt para o agente:
"Use context7 para buscar a documentação do Flyway sobre
configuração via application.yml no Spring Boot. Quero
confirmar os nomes corretos das propriedades para locations,
baseline-on-migrate e out-of-order."
```

---

## 10. executing-plans

**O que faz:** Executa planos de implementação em batches com checkpoints de revisão entre cada lote.

### Situações reais

**Situação A — Refatoração grande em etapas:**
Você precisa refatorar um monolito em módulos. São 12 tarefas.

```
Prompt para o agente:
"Tenho 12 tarefas para modularizar o OrderService:
1. Extrair validação
2. Extrair cálculo de frete
3. Extrair cálculo de imposto
4-6. Criar interfaces e injeção de dependência
7-9. Mover testes
10-12. Atualizar chamadas nos controllers

Execute em batches de 3. Após cada batch, mostre o que foi feito,
execute os testes, e espere meu OK antes de continuar."
```

**Situação B — Implementação de feature com múltiplas camadas:**

```
Prompt para o agente:
"Implemente o CRUD de Produtos com esta ordem:
Batch 1: Model + Repository + Migration
Batch 2: Service + Validações
Batch 3: Controller + DTOs + Testes de integração
Checkpoint entre cada batch com testes passando."
```

**Situação C — Migração de banco de dados em steps:**

```
Prompt para o agente:
"Migração do schema de endereços: preciso normalizar a tabela
addresses que hoje tem tudo inline no customer. Plano:
Batch 1: Criar nova tabela addresses com FK
Batch 2: Script de migração de dados
Batch 3: Atualizar queries no código
Batch 4: Remover colunas antigas
Execute com checkpoint e rollback plan entre cada step."
```

---

## 11. devops-engineer

**O que faz:** Gera Dockerfiles, pipelines de CI/CD, manifests Kubernetes e templates de IaC.

### Situações reais

**Situação A — Containerizar uma API Java:**

```
Prompt para o agente:
"Crie um Dockerfile multi-stage para nossa API Spring Boot:
- Stage 1: build com Maven e JDK 21
- Stage 2: runtime com Eclipse Temurin JRE 21 Alpine
- Otimize camadas para cache de dependências
- Inclua health check
- Non-root user"
```

**Situação B — Pipeline de CI/CD:**

```
Prompt para o agente:
"Crie um pipeline GitHub Actions para nosso projeto Java:
- Trigger em push para main e PRs
- Steps: checkout, setup JDK 21, cache Maven, build,
  testes unitários, testes de integração (com Testcontainers),
  build Docker image, push para ECR
- Separe em jobs paralelos onde possível"
```

**Situação C — Manifests Kubernetes para produção:**

```
Prompt para o agente:
"Gere os manifests Kubernetes para o serviço de pagamentos:
- Deployment com 3 réplicas, resource limits, liveness/readiness probes
- Service ClusterIP
- Ingress com TLS
- ConfigMap para variáveis de ambiente
- Secret para credenciais do banco
- HPA com target de 70% CPU"
```

---

## 12. fix-coderabbit-review

**O que faz:** Workflow sistemático para processar feedback de review automatizado de PRs.

### Situações reais

**Situação A — PR com 15 comentários do CodeRabbit:**

```
Prompt para o agente:
"O CodeRabbit fez 15 comentários no meu PR #247. Use
fix-coderabbit-review para:
1. Categorizar por severidade (critical, high, medium, low)
2. Corrigir os critical e high primeiro
3. Avaliar se os medium/low são válidos ou falsos positivos
4. Após cada correção, rodar os testes
5. Confirmar que o CI passa no final"
```

**Situação B — SonarQube bloqueou o merge:**

```
Prompt para o agente:
"O SonarQube quality gate falhou no PR com:
- 3 bugs
- 5 code smells
- 2 security hotspots
- Coverage abaixo de 80%
Processe cada categoria sistematicamente. Comece pelos bugs
e security hotspots, depois code smells, depois aumente coverage."
```

**Situação C — Review com comentários contraditórios:**

```
Prompt para o agente:
"Recebi review do CodeRabbit sugerindo extrair um método, mas
outro comentário diz que a classe já tem métodos demais.
Use fix-coderabbit-review para avaliar qual direção faz mais
sentido arquiteturalmente e aplique a correção coerente."
```

---

## 13. adversarial-review

**O que faz:** Cria revisores oponentes que desafiam adversarialmente o trabalho, buscando falhas, edge cases e vulnerabilidades.

### Situações reais

**Situação A — Antes de deploy de feature crítica:**

```
Prompt para o agente:
"Vou fazer deploy do novo fluxo de pagamento com cartão de crédito.
Faça uma revisão adversarial:
- Tente encontrar edge cases não cobertos
- Simule cenários de falha (timeout gateway, cartão recusado,
  valor zero, valor negativo, moeda inválida)
- Verifique se há vulnerabilidades (injeção, bypass de validação)
- Questione as suposições do código"
```

**Situação B — Validar lógica de permissões:**

```
Prompt para o agente:
"Implementei RBAC com 4 roles (admin, manager, user, viewer).
Faça uma revisão adversarial tentando escalar privilégios:
- Um user consegue acessar endpoints de admin?
- Um viewer consegue modificar dados?
- O que acontece com tokens expirados?
- E se o role for null ou string vazia?"
```

**Situação C — Antes de release de API pública:**

```
Prompt para o agente:
"Vamos publicar a API v2 externamente. Revisão adversarial:
- Rate limiting está implementado corretamente?
- Dados sensíveis estão expostos em alguma response?
- Paginação tem limite máximo ou permite dump do banco?
- O que acontece com payloads muito grandes?
- Input validation cobre injection em todos os campos?"
```

---

## 14. lesson-learned

**O que faz:** Extrai lições de engenharia do histórico git e mudanças recentes de código.

### Situações reais

**Situação A — Final de sprint:**

```
Prompt para o agente:
"Analise os commits das últimas 2 semanas neste repositório.
Use lesson-learned para identificar:
- Quais arquivos foram mais alterados (hotspots)
- Padrões de bugs recorrentes
- Decisões que geraram retrabalho
- O que funcionou bem e deve ser repetido"
```

**Situação B — Após resolver um bug crítico em produção:**

```
Prompt para o agente:
"Acabamos de resolver o bug de race condition no serviço de
estoque que causou venda de produtos sem estoque. Use
lesson-learned para documentar:
- Como o bug foi introduzido
- Por que não foi pego nos testes
- O que precisamos mudar no processo para evitar bugs similares"
```

**Situação C — Onboarding de dev novo:**

```
Prompt para o agente:
"Analise o histórico dos últimos 3 meses deste repositório e
gere um documento de 'lições aprendidas' para onboarding.
Quais são as armadilhas comuns? Quais módulos são mais frágeis?
Quais convenções os devs mais erram?"
```

---

## Fluxo Completo: Exemplo Real de Ponta a Ponta

**Cenário:** Implementar sistema de cupons de desconto.

```
FASE 1 — Entender o requisito
→ requirements-clarity
"O PO pediu 'sistema de cupons'. Clarifique: cupons de valor fixo
ou percentual? Com validade? Limite de uso? Por usuário ou global?
Cumulativo com outras promoções?"

FASE 2 — Explorar abordagens
→ brainstorming
"Brainstorming: cupons como entidade separada vs campo no pedido?
Validação no frontend ou backend? Tabela de regras vs hard-coded?
Trade-offs de cada abordagem."

FASE 3 — Documentar a decisão
→ creating-spec
"Crie a spec técnica: modelo de dados do cupom, endpoint de
validação, regras de negócio, API surface, edge cases."

FASE 4 — Buscar docs das libs
→ context7
"Use context7 para buscar docs do Bean Validation no Spring Boot
para validar regras de cupom com custom validators."

FASE 5 — Implementar em batches
→ executing-plans
"Batch 1: Model + Migration + Repository
Batch 2: Service com regras de validação
Batch 3: Controller + DTOs + Testes
Checkpoint entre cada batch."

FASE 6 — Verificar cada batch
→ verification-before-completion
"Rode 'mvn verify' após cada batch e mostre o output."

→ no-workarounds
(Ativa automaticamente: se alguma regra de cupom não funcionar,
a skill impede um if/else paliativo e exige correção na raiz.)

FASE 7 — Review final
→ adversarial-review
"Revisão adversarial: cupom com valor maior que o pedido? Cupom
expirado com timezone diferente? Cupom aplicado 2x no mesmo pedido?
SQL injection no campo de código?"

FASE 8 — Processar review do CI
→ fix-coderabbit-review
"Processe os 8 comentários do CodeRabbit no PR."

FASE 9 — Documentar lições
→ lesson-learned
"O que aprendemos implementando cupons? Hotspots, decisões
que mudaram, complexidades inesperadas."
```

---

## 15. frontend-design

**O que faz:** Cria interfaces frontend distintas e production-grade, evitando estética genérica de IA. Guia tipografia, cores, animações, composição espacial e detalhes visuais.

### Situações reais

**Situação A — Landing page para produto:**

```
Prompt para o agente:
"Crie uma landing page para um app de meditação. Use frontend-design
para garantir um design memorável: tipografia única, paleta coesa,
animações de entrada orquestradas, e composição que surpreenda.
Nada de Inter/Roboto com gradiente roxo genérico."
```

**Situação B — Dashboard admin:**

```
Prompt para o agente:
"Redesigne o dashboard de analytics. Use frontend-design para criar
uma estética editorial/magazine: tipografia marcante, uso intencional
de espaço negativo, micro-interações nos cards de métricas,
e tema escuro com acentos vibrantes."
```

**Situação C — Componente React estilizado:**

```
Prompt para o agente:
"Crie um card de produto para e-commerce. Use frontend-design
para evitar o padrão genérico. Quero algo com personalidade:
hover effects surpreendentes, tipografia expressiva, sombras
dramáticas, e transições suaves com Motion."
```

---

## 16. prompt-enhancement

**O que faz:** Transforma prompts vagos ou mal estruturados em prompts estruturados com XML e Markdown, aplicando técnicas de prompt engineering (goals, workflow, Chain-of-Thought, output format, few-shot).

### Situações reais

**Situação A — Ticket vago que precisa virar prompt:**

```
Prompt para o agente:
"Recebi este pedido: 'Implemente um painel de clima que mostra o tempo
atual de uma cidade.' Use prompt-enhancement para transformar isso
em um prompt estruturado com task, role, requirements (business,
technical, UI/UX), workflow, endpoints e critical constraints."
```

**Situação B — Feature complexa que precisa de contexto:**

```
Prompt para o agente:
"Preciso implementar um sistema de notificações em tempo real.
Use prompt-enhancement para estruturar: definir o papel do agente,
separar requisitos por categoria, incluir workflow com checkpoints,
documentar os endpoints WebSocket, e listar skills obrigatórias."
```

**Situação C — Refatoração que precisa de escopo claro:**

```
Prompt para o agente:
"Quero refatorar o módulo de autenticação de session-based para JWT.
Use prompt-enhancement para criar um prompt que defina exatamente
o escopo, o que está fora do escopo (NUNCA alterar X), e os
passos de migração em ordem."
```

---

## Fluxo Completo: Exemplo Real de Ponta a Ponta (Atualizado)

**Cenário:** Implementar sistema de cupons de desconto.

```
FASE 0 — Estruturar o prompt
→ prompt-enhancement
"O PO mandou: 'sistema de cupons'. Transforme em prompt estruturado
com task, role, requirements, workflow e critical."

FASE 1 — Entender o requisito
→ requirements-clarity
"Clarifique: cupons de valor fixo ou percentual? Com validade?
Limite de uso? Por usuário ou global?"

FASE 2 — Explorar abordagens
→ brainstorming
"Cupons como entidade separada vs campo no pedido?
Trade-offs de cada abordagem."

FASE 3 — Documentar a decisão
→ creating-spec
"Spec técnica: modelo de dados, endpoint de validação, regras."

FASE 4 — Buscar docs das libs
→ context7
"Docs do Bean Validation no Spring Boot para custom validators."

FASE 5 — Implementar em batches
→ executing-plans
"Batch 1: Model + Migration + Repository
Batch 2: Service com regras de validação
Batch 3: Controller + DTOs + Testes"

FASE 6 — Design da UI
→ frontend-design
"Crie a UI do formulário de aplicação de cupom com design
marcante, feedback visual de sucesso/erro, e animações."

FASE 7 — Verificar cada batch
→ verification-before-completion + no-workarounds

FASE 8 — Review final
→ adversarial-review

FASE 9 — Processar review do CI
→ fix-coderabbit-review

FASE 10 — Documentar lições
→ lesson-learned
```

---

## Referência Rápida

| Preciso de... | Use esta skill |
|---|---|
| Investigar um bug | `systematic-debugging` |
| Evitar gambiarra | `no-workarounds` |
| Confirmar que funciona | `verification-before-completion` |
| Saber as regras do projeto | `find-rules` |
| Escrever melhor | `writing-clearly-and-concisely` |
| Entender requisitos vagos | `requirements-clarity` |
| Decidir entre opções | `brainstorming` |
| Documentar decisão técnica | `creating-spec` |
| Buscar docs atualizados | `context7` |
| Implementar em etapas | `executing-plans` |
| Docker/CI/CD/K8s | `devops-engineer` |
| Processar review do PR | `fix-coderabbit-review` |
| Validar antes do deploy | `adversarial-review` |
| Aprender com o que foi feito | `lesson-learned` |
| Criar UI marcante e única | `frontend-design` |
| Estruturar prompt vago | `prompt-enhancement` |
