# Skills Catalog - Automated Setup for AI Agents

**Last Updated:** 2026-01-09
**Version:** 1.0

---

## 🤖 For AI Coding Agents

This file contains **complete setup instructions** for installing the Skills Catalog in any project. You (the AI agent) should execute these steps autonomously.

**Your goal:** Install and configure skills without requiring user intervention beyond answering a few questions.

---

## Prerequisites Check

**Step 0: Verify Environment**

Run these commands and record results:

```bash
# Check git
git --version

# Check curl or wget
curl --version || wget --version

# Check current directory
pwd

# Check if git repo
git status 2>/dev/null && echo "GIT_REPO=true" || echo "GIT_REPO=false"
```

**If git not found:** Tell user to install git first.
**If curl/wget not found:** Use alternative download method.

---

## Step 1: Detect Environment

**Agent Instructions:** Run the following checks to determine your environment:

1. Check if `.claude/` directory exists → Claude Code
2. Check for `.vscode/` with GitHub Copilot → VSCode + Copilot
3. Check for Cursor-specific files → Cursor
4. Otherwise → Generic environment

**Commands to run:**

```bash
# Detect Claude Code
[ -d ".claude" ] && echo "CLAUDE_CODE" || echo "OTHER"

# Detect GitHub Copilot
[ -f ".vscode/settings.json" ] && grep -q "github.copilot" .vscode/settings.json 2>/dev/null && echo "COPILOT"

# Detect Cursor
[ -d ".cursor" ] && echo "CURSOR"
```

**Record your environment:** `[DETECTED_ENV]`

---

## Step 2: Install bd (beads)

**Check if already installed:**

```bash
which bd && bd --version
```

**If not installed, install now:**

### macOS/Linux:

```bash
# Method 1: Direct installation script
curl -fsSL https://raw.githubusercontent.com/ezrasingh/beads/main/install.sh | sh

# Method 2: Using Cargo (if Rust installed)
cargo install beads-cli
```

### Windows:

```bash
# If Rust/Cargo installed:
cargo install beads-cli

# Otherwise, download binary from:
# https://github.com/ezrasingh/beads/releases
```

**Verify installation:**

```bash
bd --version
# Should output: beads-cli X.Y.Z
```

**If bd not in PATH:**

```bash
# Add to PATH (macOS/Linux)
export PATH="$HOME/.cargo/bin:$PATH"

# Add to PATH (Windows)
# Add %USERPROFILE%\.cargo\bin to PATH environment variable
```

---

## Step 3: Choose Skills to Install

**Agent Instructions:** Ask the user which skills they need.

**Use this decision tree:**

### Q1: "What type of project is this?"

- **Engineering/Software** → Core + Engineering skills
- **DevOps/Infrastructure** → Core + DevOps skills
- **Documentation/Writing** → Core + Documentation skills
- **Research/Evaluation** → Core + Research skills
- **All of the above** → Install everything

### Q2: "Do you use bd (beads) or Backlog MCP?"

- **bd (beads)** → Install `bd` + `git` + `subagent` skills
- **Backlog MCP** → Install `backlog-workflow` + `git-hygiene` + `subagent` skills
- **Not sure** → Default to bd (easier setup)

### Q3: "Are you a tech lead or individual contributor?"

- **Tech lead** → Install `technical-lead-role` + `task-delegation`
- **Individual** → Skip these, focus on execution skills

**Based on answers, install:**

- **Always:** `creating-skills`, `session-continuation`
- **Conditional:** Based on Q1-Q3 above

---

## Step 4: Check for Existing Skills

**Agent Instructions:** Before copying skills, check for conflicts.

```bash
# Check if .claude/skills/ exists
if [ -d ".claude/skills" ]; then
  echo "⚠️  Existing skills directory found."

  # List existing skills
  ls -la .claude/skills/

  # Ask user for preferred action
fi
```

**Options:**

1. **Merge** — Keep existing, add new from catalog (only copy non-existent skills)
2. **Replace** — Backup existing to `.claude/skills.backup.$(date +%s)/`, install fresh
3. **Skip** — Keep existing, abort installation

**Handle based on user choice.**

---

## Step 5: Download Skills from GitHub

**Agent Instructions:** Download selected skills from GitHub.

**Set base URL:**

```bash
BASE_URL="https://raw.githubusercontent.com/All-The-Vibes/skills-catalog/main"
```

**Method 1: Direct download with curl (recommended for selective install):**

```bash
# Create directory structure
mkdir -p .claude/skills/core
mkdir -p .claude/skills/engineering
mkdir -p .claude/skills/devops
mkdir -p .claude/skills/documentation
mkdir -p .claude/skills/research

# Download core skills (always needed)
curl -fsSL "$BASE_URL/.claude/skills/core/creating-skills/SKILL.md" \
  -o .claude/skills/core/creating-skills/SKILL.md

curl -fsSL "$BASE_URL/.claude/skills/core/session-continuation/SKILL.md" \
  -o .claude/skills/core/session-continuation/SKILL.md

# Download based on user selection (Q1-Q3)
# Example: Engineering skills
curl -fsSL "$BASE_URL/.claude/skills/engineering/refactoring/SKILL.md" \
  -o .claude/skills/engineering/refactoring/SKILL.md

curl -fsSL "$BASE_URL/.claude/skills/engineering/tdd/SKILL.md" \
  -o .claude/skills/engineering/tdd/SKILL.md
```

**Method 2: Git sparse-checkout (recommended for full install):**

```bash
# Initialize sparse checkout
git init
git remote add skills-catalog https://github.com/All-The-Vibes/skills-catalog.git
git config core.sparseCheckout true

# Specify what to download
echo ".claude/skills/" >> .git/info/sparse-checkout
echo "AGENTS.md" >> .git/info/sparse-checkout

# Pull only specified files
git pull skills-catalog main
```

---

## Step 6: Download AGENTS.md

```bash
curl -fsSL "$BASE_URL/AGENTS.md" -o AGENTS.md
```

**If AGENTS.md already exists:**

1. Backup existing: `mv AGENTS.md AGENTS.md.backup.$(date +%s)`
2. Download new version
3. Inform user: "Your old AGENTS.md is backed up as AGENTS.md.backup.[timestamp]"

---

## Step 7: Initialize bd

```bash
cd [project-root]
bd init

# Answer prompts based on detected environment:
# - Project name: [current directory name]
# - Git integration: [yes if GIT_REPO=true]
# - MCP or CLI: [based on user choice in Step 3]
```

**Note:** If bd is already initialized, you can skip this step.

---

## Step 8: Configure Git Hooks (Optional but Recommended)

```bash
# Run bd doctor to check for issues
bd doctor

# Install recommended hooks if suggested
bd doctor --fix
```

---

## Step 9: Environment-Specific Configuration

### If Claude Code (DETECTED_ENV=CLAUDE_CODE):

1. Verify skills are in `.claude/skills/`
2. **CRITICAL:** Inform user:
   > ⚠️ **Claude Code must restart to load new skills.**
   >
   > Please restart Claude Code now (Command+Q and relaunch on macOS, or close and relaunch on other platforms).
3. After user restarts: "Welcome back! Your skills are now active. Run `bd list` to see tasks."

### If GitHub Copilot/VSCode (DETECTED_ENV=COPILOT):

1. Verify skills are in `.claude/skills/`
2. Check if `.vscode/settings.json` exists, create if not:
   ```json
   {
     "github.copilot.enable": {
       "*": true
     }
   }
   ```
3. Recommend: "Reload VSCode window (Ctrl+Shift+P / Cmd+Shift+P → 'Reload Window')"

### If Cursor (DETECTED_ENV=CURSOR):

1. Verify skills are in `.claude/skills/`
2. Open Cursor settings (Cmd+, / Ctrl+,)
3. Verify "Agent Skills" or "AI Features" are enabled
4. Recommend: "Restart Cursor to load new skills"

### If Other (DETECTED_ENV=OTHER):

1. Verify skills are in `.claude/skills/`
2. Inform user: "Skills installed. Refer to AGENTS.md for usage instructions."
3. Recommend: "Restart your editor/agent to load skills"

---

## Step 10: Verification

**Run verification checks:**

```bash
# 1. Check skills installed
echo "Checking skills..."
ls -la .claude/skills/

# 2. Check bd working
echo "Checking bd..."
bd --version

# 3. Check AGENTS.md exists
echo "Checking AGENTS.md..."
[ -f "AGENTS.md" ] && echo "✅ AGENTS.md found" || echo "❌ AGENTS.md missing"

# 4. Check git status
echo "Checking git..."
git status

# 5. Try creating a test task
echo "Testing bd functionality..."
bd create "Test task - setup verification"
bd list
# Note the task ID, then close it:
# bd close [task-id]
```

**Success criteria:**

- ✅ `.claude/skills/` exists with skills
- ✅ `AGENTS.md` exists
- ✅ `bd` command works
- ✅ `bd list` shows tasks (including test task)
- ✅ `bd create` and `bd close` work

**If all checks pass:** Installation successful! 🎉

---

## Step 11: Next Steps

**Inform user:**

✅ **Setup Complete!**

**Getting started:**

1. **Read AGENTS.md** to understand the workflow
2. **Create your first real task:** `bd create "Your first task"`
3. **Review available skills:** `ls .claude/skills/*/`

**Workflow patterns:**

- **Tech Leads:** Use `technical-lead-role` skill, delegate tasks with Task tool
- **Individual Contributors:** Use `subagent` skill, execute tasks directly
- **Everyone:** Use `bd` for backlog management, `git` for version control

**Next task ideas:**

- `bd create "Set up CI/CD pipeline"` → Use `ci-cd` skill
- `bd create "Write project README"` → Use `technical-writing` skill
- `bd create "Refactor X module"` → Use `refactoring` skill
- `bd create "Add tests for Y feature"` → Use `tdd` skill

---

## Troubleshooting

### Issue: `bd: command not found` after installation

**Cause:** bd not in PATH

**Solution:**

```bash
# macOS/Linux: Add to PATH
export PATH="$HOME/.cargo/bin:$PATH"

# Add permanently to shell profile:
echo 'export PATH="$HOME/.cargo/bin:$PATH"' >> ~/.bashrc  # or ~/.zshrc
source ~/.bashrc  # or ~/.zshrc

# Verify
which bd
bd --version
```

**Windows:**

1. Add `%USERPROFILE%\.cargo\bin` to PATH environment variable
2. Restart terminal
3. Verify: `bd --version`

---

### Issue: Claude Code doesn't see skills after installation

**Cause:** Claude Code needs restart to load skills

**Solution:**

1. Verify skills exist: `ls -la .claude/skills/`
2. Quit Claude Code completely (Command+Q on macOS, not just close window)
3. Relaunch Claude Code
4. Check Skills panel in Claude interface
5. If still not visible, try: `rm -rf .claude/.cache` then restart again

---

### Issue: Git conflicts during skills download

**Cause:** Local changes conflict with incoming files

**Solution:**

```bash
# Stash local changes
git stash

# Retry download steps
[retry Step 5]

# Restore local changes
git stash pop

# Resolve any conflicts manually
```

---

### Issue: Skills not activating when requested

**Cause:** Malformed SKILL.md or missing frontmatter

**Solution:**

1. Check SKILL.md files have proper frontmatter:
   ```yaml
   ---
   name: skill-name
   description: Clear description of what this skill does
   ---
   ```

2. Ensure file is readable: `cat .claude/skills/core/[skill-name]/SKILL.md`

3. Restart editor/agent

4. Manually reference skill in task: "Use the [skill-name] skill to..."

---

### Issue: bd init fails with "already initialized"

**Cause:** bd is already initialized in this project

**Solution:**

This is expected if bd was previously set up. You can:

- Continue with installation (skip Step 7)
- Check existing setup: `bd list`
- Or reinitialize: `rm -rf .beads/ && bd init`

---

### Issue: Permission denied when downloading skills

**Cause:** Insufficient permissions or GitHub rate limiting

**Solution:**

```bash
# Check directory permissions
ls -la .claude/

# Fix permissions if needed
chmod -R u+w .claude/

# If GitHub rate limited, wait or use authenticated requests:
curl -H "Authorization: token YOUR_GITHUB_TOKEN_IF_NEEDED" \
  -fsSL "$BASE_URL/.claude/skills/core/creating-skills/SKILL.md" \
  -o .claude/skills/core/creating-skills/SKILL.md
```

---

## Reference

**Full Documentation:** https://github.com/All-The-Vibes/skills-catalog/blob/main/README.md

**Available Skills:**

- **Core:** bd, git, subagent, technical-lead-role, task-delegation, creating-skills, session-continuation
- **Engineering:** refactoring, tdd
- **DevOps:** ci-cd
- **Documentation:** technical-writing
- **Research:** technical-research

**Need more skills?**

- Check the repo for newly added skills
- Create your own using the `creating-skills` skill
- Submit a pull request to add skills to the catalog

---

## Support

**Issues?** https://github.com/All-The-Vibes/skills-catalog/issues

**Questions?** Read AGENTS.md or create an issue on GitHub.

**Contributing?** Pull requests welcome! Use the `creating-skills` skill to ensure consistency.

---

**Congratulations!** The Skills Catalog is now installed and ready to use. 🎉

**Remember:** Always refer to AGENTS.md for workflow guidance and best practices.
