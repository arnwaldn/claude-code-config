# Claude Code Memory - Arnaud's Dev Environment

## User
- **Name**: Arnaud
- **Email**: arnaud.porcel@gmail.com
- **Language**: French
- **HuggingFace**: Arnwald84

## System
- **PC**: AMD Ryzen 7 5700U, 15 GB RAM, Windows 11 Home
- **Shell**: bash (MINGW64/Git Bash)
- **Workspace**: `C:\Users\arnau\Projects\` (web, mobile, api, desktop, fullstack, tools, learning)

## Claude Code Setup (updated 2026-02-22)

### Commands (9) — `~/.claude/commands/`
atum-audit, deploy, feature-analyzer, migrate, pre-deploy, review-fix, scaffold, tdd, ultra-think

### Agents (24) — `~/.claude/agents/`
- **Generalist**: architect-reviewer, codebase-pattern-finder, critical-thinking, database-optimizer, error-detective, technical-debt-manager
- **Game dev**: game-architect, phaser-expert, threejs-game-expert, unity-expert, godot-expert
- **Mobile/Desktop**: flutter-dart-expert, expo-expert, tauri-expert
- **Specialist**: accessibility-auditor, api-designer, auto-test-generator, ci-cd-engineer, data-engineer, documentation-generator, graphql-expert, migration-expert, performance-optimizer, windows-scripting-expert

### Modes (4) — `~/.claude/modes/`
architect, autonomous, brainstorm, quality

### Rules (24 files) — `~/.claude/rules/`
- common/ (9): agents, anti-hallucination, coding-style, git-workflow, hooks, patterns, performance, security, testing
- typescript/ (5), python/ (5), golang/ (5)

### Hooks (18 active total)
- **Custom (5)** — `~/.claude/hooks/` registered in `settings.json`:
  - secret-scanner.py (PreToolUse: Write|Edit|Bash) — BLOCKS secrets
  - dangerous-command-blocker.py (PreToolUse: Bash) — BLOCKS destructive cmds
  - atum-session-start.py (SessionStart) — ATUM project detection
  - atum-post-write.py (PostToolUse: Write|Edit) — ATUM file tracking
  - atum-compliance-check.py (PostToolUse: Bash) — ATUM compliance on git commit
- **Plugin (13)** — everything-claude-code hooks.json:
  - tmux reminder, git push reminder, .md blocker, suggest-compact, pre-compact, session-start, PR URL logger, auto-format, typecheck, console.log warn, check console.log, session-end, evaluate-session

### Plugins (49 active, 3 disabled)
- Disabled: code-simplifier, context7, explanatory-output-style
- See `~/.claude/settings.json` for full list

### MCP Servers (29 total)
- **Local (17)**: github, firecrawl, supabase, memory, sequential-thinking, vercel, railway, cloudflare-docs, cloudflare-workers-builds, cloudflare-workers-bindings, cloudflare-observability, clickhouse, context7, magic, filesystem, gmail, desktop-commander
- **Remote via claude.ai (12)**: Canva, Cloudflare, Figma, Gamma, Hugging Face, Invideo, Make, Notion, Supabase, Vercel, Windsor.ai, Zapier

### Templates & References — `~/Projects/tools/project-templates/`
- **INDEX.md** — MASTER CATALOG. Read this before scaffolding any project.
- **164 scaffold templates**: AI agents (42), RAG (21), teams (16), memory/chat (13), web apps (21), games (5), MCP (5), voice (3), ML (4), mobile (4), desktop (3), devtools (7), devops (5), learning (3), specialized (7)
- **9 reference files**: clone-wars (200 app clones), codrops (400 demos), rapidapi (45 API categories), awesome-llm-apps (120+ AI projects), glama-mcp (17K servers), website-templates (150+ HTML5), gitignore (262 templates), profile-readme (244 styles), roadmap-sh (80+ roadmaps)
- **Workflow**: Always read INDEX.md first → find matching template/reference → scaffold from match or scratch

## Installed Dev Stack (2026-02-19)
- **Languages**: Node v24, Python 3.13, Go 1.26, Rust, .NET 9, Java 21, Deno, PHP 8.4, Ruby 3.3, Flutter/Dart
- **JS/TS**: TypeScript 5.9, Vite 7.3, Next.js 16.1, Angular 21.1, Vue CLI 5, NestJS 11, Nuxt 3.33, Tailwind 4.2
- **Python**: Django 6.0, Flask 3.1, FastAPI 0.129, pytest 9.0, black, ruff, mypy
- **DB**: SQLite native, PostgreSQL/Redis/MongoDB/MySQL via Docker
- **Testing**: Jest 30, Vitest 4.0, Playwright 1.58, pytest + pytest-cov

## Key Learnings
- Hooks in `~/.claude/hooks/` are NOT auto-discovered — must register in `settings.json` under `hooks` key
- Plugin hooks (everything-claude-code) are separate via their own `hooks/hooks.json` — no conflict with settings.json hooks
- `.claude.json` is actively watched by Claude Code — use `node -e` atomic writes to avoid edit conflicts
- Agents/commands/modes have ZERO context cost when not invoked; only rules are always loaded
- HTTP MCPs (vercel, cloudflare) use SSE — curl tests show false negatives
- Everything-claude-code `.md` blocker hook has Windows path regex issues — use Bash for .md writes in .claude/

## Preferences
- Output style: Learning mode
- winget = primary package manager
- Git: user.name Arnaud, user.email arnaud.porcel@gmail.com, SSH ed25519
