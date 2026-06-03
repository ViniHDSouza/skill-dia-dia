# skill-dia-dia — Claude Code

**Skills de desenvolvimento agnosticas de stack**
Skills organizadas em buckets dentro de `skills/`. Instale todas ou escolha por bucket/skill.

> Instrucoes completas em `AGENTS.md`. Exemplos praticos em `GUIA-SKILLS.md`.

---

## Regras para Claude Code

1. Skills estao em `skills/<bucket>/<skill>/` — carregue o `SKILL.md` antes de gerar codigo.
2. As 5 skills de `guardrails/` sao transversais — aplicar SEMPRE.
3. Consulte `GUIA-SKILLS.md` para exemplos praticos em portugues.
4. Skills sao auto-contidas e nao dependem de fontes externas.
5. Nenhuma tarefa esta pronta sem evidencia — `verification-before-completion` sempre ativo.

---

## Skills Disponiveis

| Bucket | Skills |
|--------|--------|
| `guardrails/` | `no-workarounds`, `systematic-debugging`, `verification-before-completion`, `find-rules`, `writing-clearly-and-concisely` |
| `planning/` | `requirements-clarity`, `brainstorming`, `creating-spec`, `prompt-enhancement` |
| `implementation/` | `context7`, `executing-plans`, `devops-engineer`, `frontend-design` |
| `review/` | `fix-coderabbit-review`, `adversarial-review`, `lesson-learned` |

---

## Instalacao

```bash
# Todas as skills
npx skills add https://github.com/ViniHDSouza/skill-dia-dia

# Um bucket especifico
npx skills add ViniHDSouza/skill-dia-dia/skills/guardrails

# Uma skill especifica
npx skills add ViniHDSouza/skill-dia-dia/skills/planning --skill brainstorming
```

---

## Compatibilidade

| Ferramenta | Arquivo de instrucoes | Skills |
|------------|----------------------|--------|
| Claude Code | `CLAUDE.md` (este) | `skills/` |
| OpenCode | `AGENTS.md` | `skills/` |
| VSCode | `.vscode/settings.json` | `skills/` |
