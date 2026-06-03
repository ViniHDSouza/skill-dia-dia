# skill-dia-dia

[![skills.sh](https://skills.sh/b/ViniHDSouza/skill-dia-dia)](https://skills.sh/ViniHDSouza/skill-dia-dia)

A curated collection of **16 agent skills** for everyday software development — covering guardrails, planning, prompt engineering, implementation workflows, frontend design, code review, and continuous learning. Stack-agnostic skills that enhance an agent's ability to write better code, debug systematically, and deliver with evidence.

## Installation

### Quick install (recommended)

Install all skills into your agent skills directory with the [`skills`](https://www.npmjs.com/package/skills) CLI:

```bash
npx skills add https://github.com/ViniHDSouza/skill-dia-dia
```

### Install a single bucket

Use the `owner/repo/<subpath>` shorthand to install only one bucket:

```bash
# Only guardrail skills
npx skills add ViniHDSouza/skill-dia-dia/skills/guardrails

# Only planning skills
npx skills add ViniHDSouza/skill-dia-dia/skills/planning

# Only implementation skills
npx skills add ViniHDSouza/skill-dia-dia/skills/implementation

# Only review skills
npx skills add ViniHDSouza/skill-dia-dia/skills/review
```

You can also pin a specific skill with `--skill`:

```bash
npx skills add ViniHDSouza/skill-dia-dia/skills/guardrails --skill systematic-debugging
```

### Manual install

Copy or symlink the skills you need into your Claude Code configuration:

```bash
# Copy a single skill
cp -r skills/guardrails/no-workarounds ~/.claude/skills/no-workarounds

# Or symlink an entire bucket
ln -s $(pwd)/skills/guardrails ~/.claude/skills/guardrails
```

## Usage

Skills are automatically picked up by Claude Code when placed in the `~/.claude/skills/` directory. The agent matches tasks to relevant skills based on the `description` field in each `SKILL.md` frontmatter.

### Quick start by workflow

| When you need to... | Install these skills |
|---|---|
| **Enforce code discipline** | `no-workarounds` + `systematic-debugging` + `verification-before-completion` |
| **Understand a new codebase** | `find-rules` |
| **Clarify vague requirements** | `requirements-clarity` |
| **Explore approaches before coding** | `brainstorming` |
| **Document a technical decision** | `creating-spec` |
| **Transform vague prompts into structured ones** | `prompt-enhancement` |
| **Fetch up-to-date library docs** | `context7` |
| **Execute a multi-step plan** | `executing-plans` |
| **Set up Docker/CI/CD/K8s** | `devops-engineer` |
| **Build distinctive frontend UIs** | `frontend-design` |
| **Process automated PR feedback** | `fix-coderabbit-review` |
| **Challenge code before deploy** | `adversarial-review` |
| **Learn from recent changes** | `lesson-learned` |
| **Write clear text** | `writing-clearly-and-concisely` |

### Compatibility

| Agent | Instructions | Skills |
|---|---|---|
| **Claude Code** | `CLAUDE.md` | `skills/` |
| **OpenCode** | `AGENTS.md` | `skills/` |
| **VS Code** | `.vscode/settings.json` | `skills/` (via AI extensions) |

## Skill Catalog

### Guardrails — Sempre Ativos

Skills transversais de qualidade e disciplina. Aplicar a qualquer tarefa.

- **[Sem Gambiarras](./skills/guardrails/no-workarounds)** — Root cause fixes only, no workarounds
- **[Debug Sistemático](./skills/guardrails/systematic-debugging)** — 4-phase debugging: observe, instrument, isolate, fix
- **[Verificar Antes de Concluir](./skills/guardrails/verification-before-completion)** — Evidence before assertions
- **[Descobrir Regras](./skills/guardrails/find-rules)** — Discover project conventions before writing code
- **[Escrita Clara e Concisa](./skills/guardrails/writing-clearly-and-concisely)** — Strunk's rules for clear writing

### Planning — Antes de Codar

Clareza de requisitos, brainstorming e especificações técnicas.

- **[Clareza de Requisitos](./skills/planning/requirements-clarity)** — Clarify ambiguous requirements through dialogue
- **[Brainstorming](./skills/planning/brainstorming)** — Explore approaches and trade-offs before committing
- **[Criar Spec Técnica](./skills/planning/creating-spec)** — Generate structured technical specifications
- **[Aprimorar Prompts](./skills/planning/prompt-enhancement)** — Transform vague prompts into structured XML/Markdown

### Implementation — Durante a Implementação

Docs atualizados, execução em batches, infraestrutura e design frontend.

- **[Docs Atualizados (Context7)](./skills/implementation/context7)** — Fetch current library docs via Context7 CLI
- **[Executar Planos](./skills/implementation/executing-plans)** — Execute plans in batches with review checkpoints
- **[Engenheiro DevOps](./skills/implementation/devops-engineer)** — Docker, CI/CD, Kubernetes, Terraform
- **[Design Frontend](./skills/implementation/frontend-design)** — Distinctive, production-grade frontend interfaces

### Review & Learning — Após a Implementação

Feedback de PR, revisão adversarial e lições de engenharia.

- **[Corrigir Review de PR](./skills/review/fix-coderabbit-review)** — Process CodeRabbit/SonarQube PR feedback systematically
- **[Revisão Adversarial](./skills/review/adversarial-review)** — Find edge cases, vulnerabilities, and wrong assumptions
- **[Lições Aprendidas](./skills/review/lesson-learned)** — Extract engineering lessons from git history

## Quando usar cada skill de Planning?

As 4 skills do bucket `planning/` resolvem problemas diferentes. A tabela abaixo ajuda a escolher:

| | `brainstorming` | `creating-spec` | `prompt-enhancement` |
|---|---|---|---|
| **O que faz** | Diálogo colaborativo para explorar ideias, abordagens e trade-offs antes de se comprometer | Spec técnica completa: arquitetura, APIs, migração, testes, ordem de implementação | Transforma um prompt vago em prompt estruturado com XML (task, role, requirements, workflow) |
| **Entrada** | Ideia ou decisão a tomar ("preciso de X, como faço?") | Decisão já tomada que precisa ser documentada em detalhe | Prompt mal escrito que vai ser passado para outro agente executar |
| **Saída** | Design doc curto + recomendação de abordagem | Documento de spec completo (problema, design, APIs, migração, testes) | Prompt estruturado com blocos XML (`<task>`, `<role>`, `<requirements>`, `<critical>`) |
| **Interação** | Alta — pergunta ao usuário uma coisa por vez, propõe 2-3 opções | Média — explora o código, faz 2-4 perguntas de decisão, depois escreve | Baixa — analisa o prompt de entrada e reestrutura automaticamente |
| **Quando usar** | Antes de decidir como implementar (feature nova, escolha de arquitetura, buy vs build) | Depois de decidir, para documentar a decisão com profundidade (SDK, módulo, centralização) | Quando você tem um pedido vago e precisa preparar um prompt claro para o agente executar |
| **Quando NAO usar** | Tarefa simples sem ambiguidade (bugfix, rename, config change) | Mudanças pequenas que não precisam de spec formal | Prompt que já está bem estruturado com contexto, requisitos e restrições claras |

### Fluxo típico combinando as 3

```
1. prompt-enhancement  →  Estrutura o pedido vago do PO em prompt claro
2. brainstorming       →  Explora abordagens e escolhe a melhor
3. creating-spec       →  Documenta a decisão em spec técnica completa
4. executing-plans     →  Implementa em batches seguindo a spec
```

Nem sempre as 3 são necessárias. Use apenas o que faz sentido:

- **Pedido simples e claro** → pule direto para `executing-plans`
- **Pedido vago mas sem decisão de arquitetura** → `prompt-enhancement` + `executing-plans`
- **Decisão de arquitetura** → `brainstorming` + `creating-spec`
- **Pedido vago com decisão complexa** → as 3 em sequência

## Structure

```
skills/
  guardrails/<skill-name>/       # Always-on quality & discipline skills
  planning/<skill-name>/         # Pre-implementation skills
  implementation/<skill-name>/   # During implementation skills
  review/<skill-name>/           # Review & learning skills

skills/<bucket>/<skill-name>/
  SKILL.md              # Main skill definition (required)
  references/           # Deep-dive reference material
  elements-of-style/    # Writing guidelines (writing skill)
  scripts/              # Automation scripts
  agents/               # Agent configurations
```

## Contributing

To add a new skill:

1. Create a directory under the appropriate bucket with a lowercase, hyphenated name
2. Add a `SKILL.md` with proper frontmatter (`name`, `displayName`, and `description` fields)
3. Include reference material, examples, and templates as needed

## License

MIT
