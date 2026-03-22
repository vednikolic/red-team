# Red Team

An LLM skill that adversarially stress-tests any product artifact from multiple disciplinary perspectives. Give it a PRD, strategy doc, UX flow, business pitch, or just an idea, and it produces structured findings with severity ratings and actionable recommendations.

Unlike generic "find weaknesses" prompts, Red Team activates specialized domain agents (Engineering, UXR, PMM, Privacy, Legal, Ethics, Security, Finance, Data/Analytics, Design, Ops, Localization) based on what you feed it. Each agent attacks from its domain's perspective with specific, grounded findings.

## What It Does

**Always-on agents** (activated for every analysis):
- **Engineering** -- feasibility, scalability, dependencies, timeline risks
- **UXR** -- user mental models, edge case users, behavioral assumptions
- **PMM** -- differentiation, audience definition, go-to-market timing
- **Privacy** -- data minimization, consent, cross-border, retention
- **Legal** -- regulatory surface, IP, ToS conflicts, liability

**Conditional agents** (activated based on input signals):
- **Ethics / Trust and Safety** -- misuse vectors, vulnerable populations, feedback loops
- **Security** -- authentication, third-party risk, threat modeling
- **Finance / Biz** -- unit economics, cost models, pricing assumptions
- **Data / Analytics** -- metric validity, causal claims, experiment design
- **Design** -- visual hierarchy, journey integrity, missing states
- **Ops / Implementation** -- support load, monitoring, rollback plans
- **Localization** -- text expansion, RTL support, format assumptions

Each finding is rated BLOCKING / HIGH / MEDIUM / LOW with structured grounding.

## Quick Start

### With Claude Code

```bash
git clone https://github.com/vednikolic/red-team.git
cd red-team
claude
```

Then:

```
/red-team path/to/your-spec.md
/red-team path/to/your-spec.md --save
/red-team path/to/your-spec.md --agents privacy,legal,security
```

### With Any LLM

Copy the content of [`.claude/skills/red-team/SKILL.md`](.claude/skills/red-team/SKILL.md) and use it as a system prompt or custom instruction. Then provide your document or idea as the user message.

For deeper analysis, also include [`references/agents.md`](references/agents.md) as additional context. This file contains detailed attack vector playbooks for each domain agent.

The skill file is self-contained. It works with any LLM that can follow structured instructions.

### With Other AI Coding Tools

| Tool | Install |
|------|---------|
| ChatGPT | Paste `SKILL.md` content into a Custom GPT's instructions or a project's custom instructions |
| Cursor | Copy `SKILL.md` content into `.cursor/rules/red-team.md` |
| Windsurf | Copy `SKILL.md` content into `.windsurfrules` |
| Cline / Roo | Add `SKILL.md` path to your custom instructions |
| Gemini CLI | Copy `SKILL.md` into `.gemini/instructions/red-team.md` |

## Output Format

```
Detected input type: [type]
Active agents: [list]

[AGENT] | [SEVERITY] | [ADDRESSABLE or NOTE]
Attack: [specific assumption or claim being challenged]
Grounding: [why this is a real risk, referencing the input]
Worst case: [what happens if unaddressed]
Confidence: [HIGH/MEDIUM/LOW + what would raise it]

...

## Severity Summary
BLOCKING: [count]
HIGH: [count]
MEDIUM/LOW: [count]

## Overall Confidence Score
[HIGH/MEDIUM/LOW with explanation]
```

## Project Structure

```
red-team/
├── .claude/skills/red-team/
│   └── SKILL.md              # The skill (auto-discovered by Claude Code)
├── references/
│   └── agents.md             # Deep attack vector playbooks per domain
├── CLAUDE.md                 # Project context for Claude Code
├── README.md                 # This file
└── sync.sh                   # Workspace sync utility
```

## Pairing with Steelman

Red Team finds the weaknesses. [Steelman](https://github.com/vednikolic/steelman) strengthens them. Run red-team first, then pass the output to steelman:

```
/steelman path/to/spec.md --from-red-team
```

This is optional. Both skills work independently.

## Syncing with a Workspace

If you use this skill inside a larger monorepo alongside other skills:

```bash
./sync.sh pull   # Pull latest from workspace
./sync.sh push   # Push changes back to workspace
```

Set `WORKSPACE_ROOT` if your workspace is not at `~/claude`.

## Author

Ved Nikolic ([vednikolic](https://github.com/vednikolic)) -- ved@vednikolic.com

## License

MIT
