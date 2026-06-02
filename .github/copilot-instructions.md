# Copilot Instructions

> Regras extraidas de `.agents/skills/` — [pedronauck/skills](https://github.com/pedronauck/skills)

## Guardrails (sempre ativos)

### 1. no-workarounds

Toda correcao deve atacar a causa raiz. Nunca use try/catch vazio, `as any`, `@ts-ignore`, `eslint-disable`, `setTimeout` arbitrario, monkey patches, ou copia-e-adapta de codigo.

Se o problema esta em codigo externo que voce nao controla, documente com `// WORKAROUND: [motivo] -- ver [issue]` e isole o contorno. Nao deixe vazar para outros modulos.

### 2. systematic-debugging

Quatro fases antes de propor qualquer correcao:
1. **Observar**: Leia mensagens de erro completamente, reproduza o bug de forma consistente, verifique mudancas recentes (git diff/log)
2. **Instrumentar**: Adicione logs nas fronteiras dos componentes para rastrear o fluxo de dados
3. **Isolar**: Identifique exatamente onde o valor errado se origina, trace ate a fonte
4. **Corrigir**: Escreva um teste que falha reproduzindo o bug, implemente UMA unica correcao, verifique

NUNCA proponha correcao sem causa raiz identificada. Se 3+ tentativas de fix falharem, questione a arquitetura.

### 3. verification-before-completion

Antes de declarar qualquer tarefa como concluida:
1. Execute os comandos de verificacao do projeto (testes, lint, build)
2. Leia a saida completa
3. Confirme que nao ha falhas
4. So entao declare conclusao

Nunca use "deve funcionar", "provavelmente", "parece certo". Evidencia antes de afirmacoes.

### 4. find-rules

Na primeira interacao com qualquer codebase, descubra as convencoes existentes:
- Procure por `.editorconfig`, `.eslintrc*`, `tsconfig.json`, `biome.json`
- Leia `CONTRIBUTING.md`, `AGENTS.md`, `ARCHITECTURE.md` se existirem
- Siga os padroes de codigo ja estabelecidos (nao imponha seu estilo)

### 5. writing-clearly-and-concisely

Ao escrever texto que humanos lerao (commits, PRs, documentacao, erros):
- Use voz ativa
- Omita palavras desnecessarias
- Seja especifico e concreto
- Evite jargoes vazios: "robusto", "escalavel", "de ponta", "aproveitar sinergias"

## Roteamento por situacao

| Situacao | Acao |
|---|---|
| Requisito vago ou ambiguo | Pergunte: "Por que?" (YAGNI) e "Tem jeito mais simples?" (KISS) antes de codar |
| Nova feature ou decisao de arquitetura | Explore 2-3 abordagens com trade-offs antes de decidir |
| Precisa de docs atualizadas de lib | Busque via Context7 CLI (`npx ctx7@latest`) |
| Implementacao com multiplas etapas | Execute em batches com checkpoints de revisao |
| Docker, CI/CD, K8s, Terraform | Siga boas praticas DevOps: IaC, health checks, secrets managers, non-root users |
| Review automatizado de PR | Categorize por severidade, corrija sistematicamente, verifique CI |
| Antes de deploy critico | Revise adversarialmente: edge cases, falhas, vulnerabilidades, suposicoes nao testadas |
| Fim de sprint ou bug dificil | Extraia licoes do historico git: hotspots, padroes de bugs recorrentes |
