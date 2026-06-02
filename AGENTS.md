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

```
skills/mine/no-workarounds/SKILL.md
skills/mine/fix-coderabbit-review/SKILL.md
skills/curated/systematic-debugging/SKILL.md
skills/curated/verification-before-completion/SKILL.md
skills/curated/brainstorming/SKILL.md
skills/curated/context7/SKILL.md
skills/curated/lesson-learned/SKILL.md
skills/community/find-rules/SKILL.md
skills/community/requirements-clarity/SKILL.md
skills/community/creating-spec/SKILL.md
skills/community/executing-plans/SKILL.md
skills/community/devops-engineer/SKILL.md
skills/community/adversarial-review/SKILL.md
skills/marketing/writing-clearly-and-concisely/SKILL.md
```