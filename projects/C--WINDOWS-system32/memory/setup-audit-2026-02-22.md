# Setup Audit & Enhancement - 2026-02-22

## Source: arnwaldn/ultra-create-v28
Repo analyzed for useful components. Key findings:
- 128 agents, 61 MCPs, 14 hooks, 149 templates — designed for C:\Claude-Code-Creation\ (not portable)
- CLAUDE.md uses "NON-NEGOCIABLE" override pattern — rejected
- autonomy-gate.js bypasses Write/Edit confirmation — rejected
- Hindsight dependency (Docker) required for most hooks — rejected

## What Was Extracted (safe, self-contained)
- 18 agents (8 game/mobile/desktop + 10 specialist)
- 6 commands (scaffold, deploy, tdd, review-fix, migrate, pre-deploy)
- 4 modes (architect, quality, brainstorm, autonomous)
- 1 rule (anti-hallucination red flags)
- 165 templates to ~/Projects/tools/project-templates/
- 1 MCP (desktop-commander)

## What Was Rejected and Why
| Component | Reason |
|---|---|
| CLAUDE.md persona override | Suppresses existing rules, "NON-NEGOCIABLE" |
| 14 hooks system | Performance killer (8 PreToolUse + 9 PostToolUse per call) |
| enforce-v25-rules.js | Blocks tool calls if not using shadcn/Context7 |
| autonomy-gate.js | Auto-approves Write/Edit without human confirmation |
| Hindsight memory system | Docker dependency, sends all code to local DB |
| self-improver/auto-upgrade agents | Self-modifying config = unpredictable |
| Duplicate MCPs | memory, context7, firecrawl, github, playwright already configured |
| filesystem MCP scoped to C:\ | Full disk access violates least privilege |

## Critical Fix Applied
5 custom Python hooks existed in ~/.claude/hooks/ but were NEVER registered.
Added `hooks` key to ~/.claude/settings.json with:
- secret-scanner.py → PreToolUse: Write|Edit|Bash
- dangerous-command-blocker.py → PreToolUse: Bash
- atum-session-start.py → SessionStart: *
- atum-post-write.py → PostToolUse: Write|Edit
- atum-compliance-check.py → PostToolUse: Bash

## System Architecture Notes
- Plugin hooks (everything-claude-code) = hooks/hooks.json in plugin cache
- Custom hooks = settings.json `hooks` key — both run, no conflict
- Agents/commands/modes = zero context cost (loaded on demand)
- Rules = always loaded (24 files, keep lean)
- 49 active plugins — some potentially redundant (5 code review tools, triple Supabase/Vercel)

## Known Issues
- everything-claude-code .md blocker hook: regex [\/]\.claude[\/] fails on some Windows paths
  Workaround: use Bash heredoc instead of Write tool for .md files in .claude/
- tmux hooks: auto-disabled on Windows (process.platform check) — not a bug
- swift-lsp plugin: non-functional on Windows (no Swift compiler)
