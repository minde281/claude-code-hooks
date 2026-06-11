# Installation

[⬅ Back to Main README](../README.md)

Works on **macOS, Linux, and Windows** from a single config. The hook command uses a
`python3 ... || python ...` fallback, so the correct Python interpreter is picked on
every platform automatically.

## Prerequisites

- **Python 3** — required for running the hook scripts
  - **macOS**: `brew install python3` (requires [Homebrew](https://brew.sh/)) · verify with `python3 --version`
  - **Linux**: `sudo apt install python3` (Ubuntu/Debian) or `sudo yum install python3` (RHEL/CentOS) · verify with `python3 --version`
  - **Windows**: download from [python.org](https://www.python.org/downloads/) or `winget install Python.Python.3` · verify with `python --version`
- **Audio player**
  - **macOS**: `afplay` (built-in, no install needed)
  - **Linux**: `paplay` from `pulseaudio-utils` (`sudo apt install pulseaudio-utils`)
  - **Windows**: `winsound` (built into Python)

All details are mentioned in [HOOKS-README.md](../.claude/hooks/HOOKS-README.md)

---

## Installation

### Step 1: Copy the hooks folder

Open a terminal in your project directory and run the commands for your platform.

**macOS / Linux (bash):**
```bash
mkdir -p .claude/hooks
git clone https://github.com/minde281/claude-code-hooks.git temp-hooks
cp -r temp-hooks/.claude/hooks/* .claude/hooks/
rm -rf temp-hooks
```

**Windows (PowerShell):**
```powershell
New-Item -ItemType Directory -Force -Path .claude\hooks
git clone https://github.com/minde281/claude-code-hooks.git temp-hooks
Copy-Item -Recurse -Force temp-hooks\.claude\hooks\* .claude\hooks\
Remove-Item -Recurse -Force temp-hooks
```

**Windows (Command Prompt):**
```cmd
if not exist .claude\hooks mkdir .claude\hooks
git clone https://github.com/minde281/claude-code-hooks.git temp-hooks
xcopy /E /I /Y temp-hooks\.claude\hooks\* .claude\hooks\
rmdir /S /Q temp-hooks
```

### Step 2: Copy settings.json keys into your existing Claude settings file

1. If you don't have a `.claude/settings.json` file in your project, create one.
2. Open [`install/settings.json`](settings.json) and copy the keys (`disableAllHooks` and `hooks`) into your `.claude/settings.json`.

> **One settings file for every platform.** Each hook runs
> `python3 .claude/hooks/scripts/hooks.py || python .claude/hooks/scripts/hooks.py`.
> On macOS/Linux `python3` runs directly. On Windows — where `python3` is often a
> non-functional Microsoft Store stub — it exits non-zero and the `python` fallback
> runs instead. No per-OS config needed.

### Step 3: Start Claude

Start Claude, you will hear "Claude session start" which is the sound played on startup.

```
claude
```

---

## Optional: Test Agent Hooks

To test the agent-specific hooks (PreToolUse, PostToolUse, Stop), copy the demo agent file.

**macOS / Linux (bash):**
```bash
mkdir -p .claude/agents
git clone https://github.com/minde281/claude-code-hooks.git temp-hooks
cp temp-hooks/.claude/agents/claude-code-hook-agent.md .claude/agents/
rm -rf temp-hooks
```

**Windows (PowerShell):**
```powershell
New-Item -ItemType Directory -Force -Path .claude\agents
git clone https://github.com/minde281/claude-code-hooks.git temp-hooks
Copy-Item temp-hooks\.claude\agents\claude-code-hook-agent.md .claude\agents\
Remove-Item -Recurse -Force temp-hooks
```

**Windows (Command Prompt):**
```cmd
if not exist .claude\agents mkdir .claude\agents
git clone https://github.com/minde281/claude-code-hooks.git temp-hooks
copy temp-hooks\.claude\agents\claude-code-hook-agent.md .claude\agents\
rmdir /S /Q temp-hooks
```

After copying, run the agent in Claude Code with:
```
/agents claude-code-hook-agent
```

This agent fetches the weather for Dubai and demonstrates the PreToolUse, PostToolUse, and Stop hooks in action.
