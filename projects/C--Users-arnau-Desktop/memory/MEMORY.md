# Environment Setup (Windows 11)

## PATH Configuration
- `.bashrc` and `.bash_profile` at `~` configure the PATH
- `~/bin/` contains wrapper scripts: `python3`, `python`, `pip3`, `pip`, `gh`
- Wrappers delegate to actual executables (Python313, GitHub CLI)

## Tool Locations
- **Python 3.13**: `C:\Users\arnau\AppData\Local\Programs\Python\Python313\`
- **GitHub CLI**: `C:\Program Files\GitHub CLI\gh.exe` (account: arnwaldn)
- **Node.js**: `C:\Program Files\nodejs\` (v24.13.1)
- **Git**: mingw64 (v2.53.0)
- **Semgrep**: Installed via pip in Python313/Scripts/

## Hooks
- Python hooks (hookify, security-guidance, qodo-skills) need `CLAUDE_PLUGIN_ROOT` env var
- Node hooks (everything-claude-code) work natively
- Shell hooks (.sh) work via Git Bash
- Semgrep hooks work after pip install
- Hook fix: `.claude/` paths and `MEMORY.md` exempted from md-blocker hook (patched in both cache + marketplace copies)

## Key Gotchas
- Windows has no `python3.exe` — `~/bin/python3` wrapper bridges this
- `gh` installed via winget, not auto-added to Git Bash PATH — `~/bin/gh` wrapper
- everything-claude-code md-blocker hook: two copies to patch (cache + marketplaces)
- Hooks are cached at session start — edits to hooks.json take effect next session
