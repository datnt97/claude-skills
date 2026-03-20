# Claude Code Skills

A personal collection of agent skills for Claude Code, extending capabilities across planning, development, and tooling.

## Setup

Clone this repo into your Claude Code skills directory:

```bash
git clone https://github.com/datnt97/claude-skills.git ~/.claude/skills
```

To update skills to the latest version:

```bash
cd ~/.claude/skills && git pull
```

Claude Code automatically loads all skills from `~/.claude/skills` on startup — no further configuration needed.

## How Skills Work

Skills extend what Claude can do. Each skill has a `SKILL.md` with instructions that Claude follows when invoked.

**Invoking a skill:**
- **Directly**: type `/skill-name` in Claude Code
- **Automatically**: Claude loads it when your message matches the skill's `description`

**Scope priority** (higher wins when names conflict):

| Location   | Path                                     | Applies to          |
| :--------- | :--------------------------------------- | :------------------ |
| Personal   | `~/.claude/skills/<skill-name>/SKILL.md` | All your projects   |
| Project    | `.claude/skills/<skill-name>/SKILL.md`   | This project only   |

**Key frontmatter fields in `SKILL.md`:**

| Field                      | Description                                                                  |
| :------------------------- | :--------------------------------------------------------------------------- |
| `name`                     | Becomes the `/slash-command`. Defaults to directory name if omitted.         |
| `description`              | Tells Claude when to auto-invoke. Omit to disable automatic triggering.      |
| `disable-model-invocation` | Set `true` to allow only manual `/name` invocation (e.g. deploy, commit).   |
| `allowed-tools`            | Tools Claude can use without asking permission when this skill is active.    |
| `context: fork`            | Run the skill in an isolated subagent (no access to conversation history).   |

## Skills

### Planning & Design

- **write-a-prd** — Create a PRD through user interview, codebase exploration, and module design. Saved to `/ai-docs/prd/[feature-name].md`.

- **prd-to-plan** — Turn a PRD into a multi-phase implementation plan using tracer-bullet vertical slices. Saved to `./ai-docs/plans/`.

- **grill-me** — Get relentlessly interviewed about a plan or design until every branch of the decision tree is resolved.

### Development

- **tdd** — Test-driven development with a red-green-refactor loop. Builds features or fixes bugs one vertical slice at a time.

- **write-a-skill** — Create new agent skills with proper structure, progressive disclosure, and bundled resources.

### Code Understanding

- **explain-code** — Explains code with visual diagrams and analogies. Includes everyday analogies, ASCII diagrams, step-by-step walkthroughs, and common gotchas.

### Tooling & Safety

- **git-guardrails-claude-code** — Set up Claude Code hooks to block dangerous git commands (`push`, `reset --hard`, `clean -f`, `branch -D`, `checkout .`) before they execute.

## Structure

Each skill lives in its own directory:

```
skill-name/
├── SKILL.md        # Main instructions (required)
├── REFERENCE.md    # Detailed docs (if needed)
└── scripts/        # Utility scripts (if needed)
```

The `skills/` subdirectory contains the upstream community skills collection.

## Adding Skills

To add a new skill, use the `write-a-skill` skill or create a directory with a `SKILL.md` file following the template in `write-a-skill/SKILL.md`.
