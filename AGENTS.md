# AGENTS.md

> Skills de desenvolvimento agnósticas de stack. Fonte: [pedronauck/skills](https://github.com/pedronauck/skills)

## Guardrails (sempre ativos)

Estas skills se aplicam continuamente — nunca as ignore.

- **no-workarounds** — Toda correção deve atacar a causa raiz. Nada de try/catch engolindo exceções, flags booleanas para pular caminhos quebrados ou patches `// TODO: fix later`.
- **systematic-debugging** — Investigar antes de corrigir. Quatro fases: observar → instrumentar → isolar → corrigir. Nenhuma proposta de fix até a causa raiz ser identificada. Se 3+ fixes falharem, questionar a arquitetura.
- **verification-before-completion** — Executar os comandos de verificação do projeto e confirmar a saída antes de marcar qualquer tarefa como concluída. Nenhuma tarefa está pronta sem evidência.
- **find-rules** — Na primeira interação com qualquer codebase, descobrir as convenções existentes (linters, `.editorconfig`, `CONTRIBUTING.md`, guidelines arquiteturais) antes de escrever código.
- **writing-clearly-and-concisely** — Aplicar as regras de Strunk a toda escrita: eliminar voz passiva, remover palavras redundantes, manter frases curtas.

## Roteamento de Skills

### Antes de escrever código

| Sinal | Skill | Finalidade |
|---|---|---|
| Requisitos vagos ou ambíguos | `requirements-clarity` | Diálogo estruturado para revelar complexidade oculta, contradições e edge cases faltantes |
| Nova feature ou decisão arquitetural | `brainstorming` | Explorar abordagens, restrições e trade-offs antes de se comprometer com uma direção |
| Necessidade de documentar decisão técnica | `creating-spec` | Gerar spec estruturada: contexto, solução, API surface, plano de migração, riscos |

### Durante a implementação

| Sinal | Skill | Finalidade |
|---|---|---|
| Precisa de docs atualizados de qualquer lib ou API | `context7` | Buscar documentação atualizada, referências de API e exemplos de código via Context7 CLI |
| Plano de implementação com múltiplas etapas | `executing-plans` | Executar em lotes com checkpoints de revisão entre cada batch |
| Docker, CI/CD, Kubernetes, Terraform | `devops-engineer` | Gerar Dockerfiles, pipelines, manifests e templates de IaC |

### Durante o review

| Sinal | Skill | Finalidade |
|---|---|---|
| Feedback automatizado de PR (CodeRabbit, SonarQube) | `fix-coderabbit-review` | Categorizar por severidade, aplicar correções sistematicamente, verificar que o CI passa |
| Mudanças críticas antes de merge/deploy | `adversarial-review` | Desafio adversarial: encontrar edge cases não cobertos, suposições incorretas, vulnerabilidades |

### Após a conclusão

| Sinal | Skill | Finalidade |
|---|---|---|
| Final de sprint, post-mortem ou bug difícil resolvido | `lesson-learned` | Extrair lições de engenharia do histórico git e mudanças recentes |

## Referência das Skills Instaladas

### .agents/skills/

```
.agents/skills/adversarial-review/SKILL.md
.agents/skills/brainstorming/SKILL.md
.agents/skills/context7/SKILL.md
.agents/skills/creating-spec/SKILL.md
.agents/skills/devops-engineer/SKILL.md
.agents/skills/executing-plans/SKILL.md
.agents/skills/find-rules/SKILL.md
.agents/skills/fix-coderabbit-review/SKILL.md
.agents/skills/lesson-learned/SKILL.md
.agents/skills/no-workarounds/SKILL.md
.agents/skills/requirements-clarity/SKILL.md
.agents/skills/systematic-debugging/SKILL.md
.agents/skills/verification-before-completion/SKILL.md
.agents/skills/writing-clearly-and-concisely/SKILL.md
```

### .claude/skills/

```
.claude/skills/adversarial-review/SKILL.md
.claude/skills/brainstorming/SKILL.md
.claude/skills/context7/SKILL.md
.claude/skills/creating-spec/SKILL.md
.claude/skills/devops-engineer/SKILL.md
.claude/skills/executing-plans/SKILL.md
.claude/skills/find-rules/SKILL.md
.claude/skills/fix-coderabbit-review/SKILL.md
.claude/skills/lesson-learned/SKILL.md
.claude/skills/no-workarounds/SKILL.md
.claude/skills/requirements-clarity/SKILL.md
.claude/skills/systematic-debugging/SKILL.md
.claude/skills/verification-before-completion/SKILL.md
.claude/skills/writing-clearly-and-concisely/SKILL.md
```