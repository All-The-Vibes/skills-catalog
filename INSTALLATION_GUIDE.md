# Skills Catalog Installation Guide

**For Human Users**

This guide walks you through installing the Skills Catalog in your project, either manually or with AI agent assistance.

---

## Table of Contents

1. [Quick Start (AI Agent)](#quick-start-ai-agent)
2. [Manual Installation](#manual-installation)
3. [Environment-Specific Setup](#environment-specific-setup)
4. [Verification](#verification)
5. [Next Steps](#next-steps)
6. [Troubleshooting](#troubleshooting)

---

## Quick Start (AI Agent)

The fastest way to install is to let your AI coding agent do it for you.

### For Claude Code Users:

1. Open Claude Code in your project directory
2. Send this message to Claude:

   ```
   Read and execute the instructions at:
   https://raw.githubusercontent.com/All-The-Vibes/skills-catalog/main/AGENT_START.md
   ```

3. Claude will:
   - Detect your environment
   - Install bd (beads) if needed
   - Ask which skills you need
   - Download and configure everything
   - Tell you when to restart Claude Code

4. Restart Claude Code when prompted
5. Done! Run `bd list` to get started

### For GitHub Copilot / VSCode Users:

1. Open GitHub Copilot Chat in your project
2. Send this message:

   ```
   Read and execute the instructions at:
   https://raw.githubusercontent.com/All-The-Vibes/skills-catalog/main/AGENT_START.md
   ```

3. Follow the agent's prompts
4. Reload VSCode window when complete

---

## Manual Installation

Prefer to install manually? Follow these steps.

### Prerequisites

- **Git** — Version control system
- **curl or wget** — File download tools
- **Terminal/Command Prompt** — Command-line access

**Check if you have these:**

```bash
git --version
curl --version || wget --version
```

---

### Step 1: Install bd (beads)

bd is a task management CLI that powers the Skills Catalog workflow.

**macOS / Linux:**

```bash
# Using the installation script (recommended)
curl -fsSL https://raw.githubusercontent.com/ezrasingh/beads/main/install.sh | sh

# OR using Cargo (if you have Rust installed)
cargo install beads-cli
```

**Windows:**

```powershell
# Using Cargo (if you have Rust installed)
cargo install beads-cli

# OR download binary from:
# https://github.com/ezrasingh/beads/releases
```

**Verify installation:**

```bash
bd --version
# Should show: beads-cli X.Y.Z
```

**If bd is not found:**

Add it to your PATH:

```bash
# macOS/Linux - Add to ~/.bashrc or ~/.zshrc
export PATH="$HOME/.cargo/bin:$PATH"

# Windows - Add to System Environment Variables
# %USERPROFILE%\.cargo\bin
```

---

### Step 2: Initialize bd in Your Project

Navigate to your project directory and initialize bd:

```bash
cd /path/to/your/project
bd init
```

**Answer the prompts:**

- **Project name:** (Enter your project name or press Enter for directory name)
- **MCP or CLI:** Choose based on your preference
  - **MCP** — Recommended for Claude Code, Cursor, Gemini
  - **CLI** — Works with all tools
- **Git integration:** Yes (if using git)

This creates a `backlog/` directory with `BACKLOG.md` for task tracking.

---

### Step 3: Create Skills Directory

Create the directory where skills will live:

```bash
mkdir -p .claude/skills
```

**Note:** The `.claude/skills/` directory is the standard location for agent skills, regardless of which agent you use (Claude, Copilot, Cursor, etc.).

---

### Step 4: Download Skills

You can download individual skills or the entire catalog.

#### Option A: Download Entire Catalog (Recommended)

```bash
# Clone the repository into a temporary location
git clone https://github.com/All-The-Vibes/skills-catalog.git /tmp/skills-catalog

# Copy skills to your project
cp -r /tmp/skills-catalog/.claude/skills/* .claude/skills/

# Copy AGENTS.md workflow guide
cp /tmp/skills-catalog/AGENTS.md AGENTS.md

# Clean up
rm -rf /tmp/skills-catalog
```

#### Option B: Download Specific Skills

If you only need certain skills:

```bash
# Set base URL
BASE_URL="https://raw.githubusercontent.com/All-The-Vibes/skills-catalog/main"

# Download core skills (recommended for everyone)
mkdir -p .claude/skills/core/creating-skills
curl -fsSL "$BASE_URL/.claude/skills/core/creating-skills/SKILL.md" \
  -o .claude/skills/core/creating-skills/SKILL.md

mkdir -p .claude/skills/core/session-continuation
curl -fsSL "$BASE_URL/.claude/skills/core/session-continuation/SKILL.md" \
  -o .claude/skills/core/session-continuation/SKILL.md

# Download AGENTS.md
curl -fsSL "$BASE_URL/AGENTS.md" -o AGENTS.md
```

**Available skill categories:**

- **core/** — Fundamental skills (bd, git, subagent, technical-lead-role, task-delegation, etc.)
- **engineering/** — Software development (refactoring, tdd)
- **devops/** — Infrastructure and deployment (ci-cd)
- **documentation/** — Writing and documentation (technical-writing)
- **research/** — Investigation and analysis (technical-research)

See [SKILL_SELECTOR.md](SKILL_SELECTOR.md) for help choosing which skills you need.

---

### Step 5: Verify Installation

Check that everything is installed correctly:

```bash
# 1. Check skills directory
ls -la .claude/skills/

# 2. Check bd is working
bd --version

# 3. Check AGENTS.md exists
ls -la AGENTS.md

# 4. Create a test task
bd create "Test task - installation verification"

# 5. List tasks
bd list

# 6. Close the test task
bd close [task-id]
```

**Success indicators:**

- ✅ `.claude/skills/` contains skill subdirectories
- ✅ `AGENTS.md` exists in project root
- ✅ `bd` commands work
- ✅ `bd list` shows tasks

---

## Environment-Specific Setup

Additional steps depending on your AI coding environment.

### Claude Code

**Location:** `.claude/skills/` ✅ (already correct)

**After installation:**

1. **Restart Claude Code** — Skills are loaded at startup
   - macOS: Command+Q, then relaunch
   - Windows/Linux: Close completely, then relaunch

2. **Verify in Claude:**
   - Start a new conversation
   - Type: "What skills do you have?"
   - Claude should list the installed skills

3. **Start using:**
   - Read AGENTS.md for workflow guidance
   - Run `bd list` to see your backlog
   - Try: "Use the technical-writing skill to write a README"

---

### GitHub Copilot (VSCode)

**Location:** `.claude/skills/` ✅ (already correct)

**After installation:**

1. **Reload VSCode:**
   - Cmd+Shift+P / Ctrl+Shift+P → "Developer: Reload Window"

2. **Open Copilot Chat:**
   - Click Copilot icon in sidebar
   - Or press Ctrl+Shift+I / Cmd+Shift+I

3. **Verify skills:**
   - Type: "What skills are available?"
   - Copilot should recognize installed skills

4. **Start using:**
   - Reference skills by name: "Use the refactoring skill"
   - Follow AGENTS.md for workflow patterns

---

### Cursor

**Location:** `.claude/skills/` ✅ (already correct)

**After installation:**

1. **Restart Cursor** or reload window

2. **Check settings:**
   - Open Settings (Cmd+, / Ctrl+,)
   - Search for "Agent Skills" or "AI Features"
   - Ensure enabled

3. **Verify:**
   - Open Cursor chat
   - Ask: "What skills do you have access to?"

4. **Start using:**
   - Reference skills in chat: "Use the tdd skill"
   - Follow AGENTS.md patterns

---

### Other Editors / Generic Setup

**Location:** `.claude/skills/` ✅ (standard location)

**After installation:**

1. Check if your editor/agent supports Agent Skills format
2. Consult your tool's documentation for loading skills
3. If unsupported, you can still reference skills manually:
   - Read `AGENTS.md` for workflow patterns
   - Open `.claude/skills/[category]/[skill-name]/SKILL.md` as needed
   - Follow skill instructions manually

---

## Verification

After installation, verify everything works:

### Test 1: bd Functionality

```bash
# Create a test task
bd create "Test: Verify skills catalog setup"

# List tasks (should show the new task)
bd list

# Close the task
bd close [task-id-from-list]
```

### Test 2: Skills Access (with your AI agent)

Ask your agent:

```
What skills do you have available? Please list them by category.
```

Expected response should include skills from `.claude/skills/`.

### Test 3: AGENTS.md Workflow

Ask your agent:

```
Read AGENTS.md and explain the workflow for managing tasks.
```

Expected response should summarize the tech lead / task delegation pattern.

---

## Next Steps

**Congratulations! You're ready to start using the Skills Catalog.**

### Getting Started

1. **Read AGENTS.md** — Understand the workflow
   ```bash
   cat AGENTS.md
   ```

2. **Create your first task:**
   ```bash
   bd create "Write project README"
   ```

3. **Use skills in your work:**
   - Tell your agent: "Use the technical-writing skill to create a README"
   - Or: "Use the refactoring skill to clean up the auth module"

4. **Review your backlog:**
   ```bash
   bd list
   ```

### Recommended First Tasks

- **Documentation:** `bd create "Write comprehensive README"` → Use `technical-writing` skill
- **Code Quality:** `bd create "Set up CI/CD pipeline"` → Use `ci-cd` skill
- **Refactoring:** `bd create "Refactor legacy module X"` → Use `refactoring` skill
- **Testing:** `bd create "Add tests for feature Y"` → Use `tdd` skill

---

## Troubleshooting

### Problem: `bd: command not found`

**Solution:**

1. Verify bd is installed:
   ```bash
   cargo install beads-cli
   ```

2. Add to PATH:
   ```bash
   export PATH="$HOME/.cargo/bin:$PATH"
   ```

3. Reload shell:
   ```bash
   source ~/.bashrc  # or ~/.zshrc
   ```

---

### Problem: Agent doesn't see skills

**Claude Code:**

1. Check skills location: `ls -la .claude/skills/`
2. Restart Claude Code completely (Command+Q, relaunch)
3. Clear cache if needed: `rm -rf .claude/.cache`

**GitHub Copilot:**

1. Check skills location: `ls -la .claude/skills/`
2. Reload VSCode window: Cmd+Shift+P → "Developer: Reload Window"
3. Check Copilot is enabled in settings

**Cursor:**

1. Check skills location: `ls -la .claude/skills/`
2. Restart Cursor
3. Verify Agent Skills enabled in settings

---

### Problem: Skills exist but don't activate

**Check skill format:**

```bash
# View a skill file
cat .claude/skills/core/creating-skills/SKILL.md
```

**Ensure proper frontmatter:**

```yaml
---
name: skill-name
description: Clear description here
---
```

If frontmatter is missing or malformed, the skill won't load.

---

### Problem: AGENTS.md missing

**Download it:**

```bash
curl -fsSL https://raw.githubusercontent.com/All-The-Vibes/skills-catalog/main/AGENTS.md \
  -o AGENTS.md
```

---

### Problem: Git conflicts during installation

**If you have local changes:**

```bash
# Stash changes
git stash

# Retry installation
[repeat installation steps]

# Restore changes
git stash pop
```

---

### Need More Help?

- **Read AGENT_START.md** for detailed agent automation steps
- **Read SKILL_SELECTOR.md** to choose the right skills
- **Open an issue:** https://github.com/All-The-Vibes/skills-catalog/issues
- **Check documentation:** https://github.com/All-The-Vibes/skills-catalog

---

## Summary

**Installation checklist:**

- ✅ Installed bd (beads)
- ✅ Initialized bd in project (`bd init`)
- ✅ Created `.claude/skills/` directory
- ✅ Downloaded skills from catalog
- ✅ Downloaded AGENTS.md
- ✅ Restarted editor/agent
- ✅ Verified bd commands work
- ✅ Verified agent sees skills
- ✅ Read AGENTS.md workflow guide

**You're ready to go!** Start creating tasks and using skills to supercharge your development workflow.
