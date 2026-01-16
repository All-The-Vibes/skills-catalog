# Skills Catalog - Automated Setup for AI Agents

**Last Updated:** 2026-01-10
**Version:** 1.1

---

## 🤖 For AI Coding Agents

This file contains **complete setup instructions** for installing the Skills Catalog in any project. You (the AI agent) should execute these steps autonomously.

**Your goal:** Install and configure skills without requiring user intervention beyond answering a few questions.

---

## Step 0: Prerequisites Check

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

## Step 1: Detect Platform and Ask User

**Agent Instructions:** Determine which AI coding assistant is being used.

### Automatic Detection

Run these checks:

```bash
# Check for Claude Code indicators
if [ -d ".claude" ] || command -v claude &>/dev/null; then
  echo "PLATFORM=claude-code"
fi

# Check for GitHub Copilot indicators
if [ -d ".github" ] || ([ -f ".vscode/settings.json" ] && grep -q "github.copilot" .vscode/settings.json 2>/dev/null); then
  echo "PLATFORM=github-copilot"
fi

# Check for Cursor indicators
if [ -d ".cursor" ]; then
  echo "PLATFORM=cursor"
fi
```

### Ask User to Confirm

**Present the user with a question:**

"Which AI coding assistant are you using?"
- **Claude Code** (uses `.claude/skills/`)
- **GitHub Copilot** (uses `.github/skills/` or `.claude/skills/`)
- **Cursor** (uses `.claude/skills/`)
- **Other / Not Sure** (will use `.claude/skills/`)

**Record answer:** `[PLATFORM]`

---

## Step 2: Git Repository Setup

**Check if git is initialized:**

```bash
git status 2>/dev/null
```

### If NOT a git repository (GIT_REPO=false):

**Ask the user:**

"This directory is not a git repository. Would you like to initialize git?"
- **Yes, initialize new repo** → Run `git init`
- **No, skip git** → Continue without git (skills will still work)

### If IS a git repository:

**Ask the user:**

"Do you want to connect this repository to a remote?"
- **Create new remote on GitHub** → Help create repo with gh CLI
- **Connect to existing remote** → Ask for URL and add remote
- **No remote needed** → Continue with local repo only

#### If "Create new remote on GitHub":

```bash
# Check if gh CLI is available
if command -v gh &>/dev/null; then
  echo "GitHub CLI is available"

  # Ask user for details
  echo "What should the repository be named?"
  # [Get repo name from user]

  echo "Should it be public or private?"
  # [Get visibility from user]

  echo "Which organization/account? (or leave blank for personal)"
  # [Get org from user, optional]

  # Create the repository
  if [ -n "$ORG" ]; then
    gh repo create "$ORG/$REPO_NAME" --$VISIBILITY --source=. --remote=origin
  else
    gh repo create "$REPO_NAME" --$VISIBILITY --source=. --remote=origin
  fi
else
  echo "GitHub CLI not available. Please install gh CLI or add remote manually"
  echo "See: https://cli.github.com/"
fi
```

#### If "Connect to existing remote":

```bash
# Ask user for remote URL
echo "What is the remote repository URL?"
# [Get URL from user]

# Add remote
git remote add origin "$REMOTE_URL"

# Optionally pull if remote has content
echo "Does the remote have existing content you want to pull?"
# If yes: git pull origin main (or appropriate branch)
```

---

## Step 3: Determine Skills Directory

**Based on platform detected in Step 1:**

### For Claude Code:
- **Skills Directory:** `.claude/skills/`
- **Why:** Claude Code uses this standard location

**Set variable:**
```bash
SKILLS_CHOICE=".claude/skills"
```

### For GitHub Copilot:
**Ask the user:**

"GitHub Copilot supports both `.github/skills/` and `.claude/skills/` for agent skills. Which would you prefer?"
- **`.github/skills/`** (GitHub standard, good for GitHub-centric workflows)
- **`.claude/skills/`** (Cross-platform, works with Claude Code too)
- **Both** (maximum compatibility, skills will be copied to both locations)

**Record answer and set variable:**
```bash
# Set based on user's choice:
# ".claude/skills" or ".github/skills" or "both"
SKILLS_CHOICE="[user's choice]"
```

### For Cursor:
- **Skills Directory:** `.claude/skills/`
- **Why:** Cursor uses the Claude Code standard

**Set variable:**
```bash
SKILLS_CHOICE=".claude/skills"
```

### For Other:
- **Skills Directory:** `.claude/skills/`
- **Why:** Default cross-platform location

**Set variable:**
```bash
SKILLS_CHOICE=".claude/skills"
SKILLS_DIR="[determined above]"
```

---

## Step 4: Install bd (beads)

**Check if already installed:**

```bash
which bd && bd --version
```

**If not installed, install now:**

### macOS/Linux:

```bash
# Method 1: Direct installation script (recommended)
curl -fsSL https://raw.githubusercontent.com/steveyegge/beads/main/scripts/install.sh | bash


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
# macOS/Linux: Add to PATH
export PATH="$HOME/.cargo/bin:$PATH"

# Add permanently to shell profile
echo 'export PATH="$HOME/.cargo/bin:$PATH"' >> ~/.bashrc  # or ~/.zshrc
source ~/.bashrc  # or ~/.zshrc
```

---

## Step 5: Choose Skills to Install

**Agent Instructions:** Ask the user which skills they need.

**Use this decision tree:**

### Q1: "What type of project is this?"

- **Engineering/Software** → Core + Engineering skills
- **DevOps/Infrastructure** → Core + DevOps skills
- **Documentation/Writing** → Core + Documentation skills
- **Research/Evaluation** → Core + Research skills
- **All of the above** → Install everything

### Q2: "Do you use bd (beads) or Backlog MCP for task management?"

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

## Step 6: Check for Existing Skills

**Agent Instructions:** Before copying skills, check for conflicts.

```bash
# Check if skills directory exists
if [ -d "$SKILLS_DIR" ]; then
  echo "⚠️  Existing skills directory found at: $SKILLS_DIR"

  # List existing skills
  ls -la "$SKILLS_DIR"

  # Ask user for action
fi
```

**Ask the user:**

"Skills directory already exists. What would you like to do?"
- **Merge** — Keep existing, add new from catalog (only copy non-existent skills)
- **Replace** — Backup existing, install fresh
- **Skip** — Keep existing, abort installation

**Handle based on user choice.**

---

## Step 7: Download Skills from GitHub

**Agent Instructions:** Download selected skills from the catalog.

**Set base URL:**

```bash
BASE_URL="https://raw.githubusercontent.com/All-The-Vibes/skills-catalog/main"
```

### Method 1: Direct download with curl (recommended for selective install)

```bash
# Create directory structure
mkdir -p "$SKILLS_DIR/core"
mkdir -p "$SKILLS_DIR/engineering"
mkdir -p "$SKILLS_DIR/devops"
mkdir -p "$SKILLS_DIR/documentation"
mkdir -p "$SKILLS_DIR/research"

# Download core skills (always needed)
mkdir -p "$SKILLS_DIR/core/creating-skills"
curl -fsSL "$BASE_URL/.claude/skills/core/creating-skills/SKILL.md" \
  -o "$SKILLS_DIR/core/creating-skills/SKILL.md"

mkdir -p "$SKILLS_DIR/core/session-continuation"
curl -fsSL "$BASE_URL/.claude/skills/core/session-continuation/SKILL.md" \
  -o "$SKILLS_DIR/core/session-continuation/SKILL.md"

# Download based on user selection (Q2 from Step 5)
# If using bd (beads):
mkdir -p "$SKILLS_DIR/core/bd"
curl -fsSL "$BASE_URL/.claude/skills/core/bd/SKILL.md" \
  -o "$SKILLS_DIR/core/bd/SKILL.md"

mkdir -p "$SKILLS_DIR/core/git"
curl -fsSL "$BASE_URL/.claude/skills/core/git/SKILL.md" \
  -o "$SKILLS_DIR/core/git/SKILL.md"

mkdir -p "$SKILLS_DIR/core/subagent"
curl -fsSL "$BASE_URL/.claude/skills/core/subagent/SKILL.md" \
  -o "$SKILLS_DIR/core/subagent/SKILL.md"

# If using Backlog MCP:
mkdir -p "$SKILLS_DIR/core/backlog-workflow"
curl -fsSL "$BASE_URL/.claude/skills/core/backlog-workflow/SKILL.md" \
  -o "$SKILLS_DIR/core/backlog-workflow/SKILL.md"

mkdir -p "$SKILLS_DIR/core/git-hygiene"
curl -fsSL "$BASE_URL/.claude/skills/core/git-hygiene/SKILL.md" \
  -o "$SKILLS_DIR/core/git-hygiene/SKILL.md"

# Download based on user selection (Q1 from Step 5)
# Engineering skills:
mkdir -p "$SKILLS_DIR/engineering/refactoring"
curl -fsSL "$BASE_URL/.claude/skills/engineering/refactoring/SKILL.md" \
  -o "$SKILLS_DIR/engineering/refactoring/SKILL.md"

mkdir -p "$SKILLS_DIR/engineering/tdd"
curl -fsSL "$BASE_URL/.claude/skills/engineering/tdd/SKILL.md" \
  -o "$SKILLS_DIR/engineering/tdd/SKILL.md"

# ... Continue for other categories as selected
```

### Method 2: Clone full catalog (for "Install everything")

```bash
# Create temporary directory
TEMP_DIR=$(mktemp -d)

# Clone the catalog
git clone --depth 1 https://github.com/All-The-Vibes/skills-catalog.git "$TEMP_DIR"

# Copy all skills to destination
cp -r "$TEMP_DIR/.claude/skills/"* "$SKILLS_DIR/"

# Copy AGENTS.md
cp "$TEMP_DIR/AGENTS.md" ./AGENTS.md

# Cleanup
rm -rf "$TEMP_DIR"
```

### For GitHub Copilot with "Both" locations:

If user chose to install in both `.github/skills/` AND `.claude/skills/`:

```bash
# Install to .claude/skills first
SKILLS_DIR=".claude/skills"
[run downloads above]

# Copy to .github/skills
mkdir -p .github/skills
cp -r .claude/skills/* .github/skills/
```

---

## Step 8: Download AGENTS.md

```bash
curl -fsSL "$BASE_URL/AGENTS.md" -o AGENTS.md
```

**If AGENTS.md already exists:**

1. Backup existing: `mv AGENTS.md AGENTS.md.backup.$(date +%s)`
2. Download new version
3. Inform user: "Your old AGENTS.md is backed up as AGENTS.md.backup.[timestamp]"

### Transform Paths Based on Skills Directory Choice

**After downloading AGENTS.md, update paths based on user's choice in Step 3:**

```bash
# Transform paths based on user's skills directory choice
if [ "$SKILLS_CHOICE" = ".github/skills" ]; then
  # User chose ONLY .github/skills/
  # Replace all /.claude/skills/ paths with /.github/skills/
  sed -i 's|/.claude/skills/|/.github/skills/|g' AGENTS.md
  echo "✅ Updated AGENTS.md paths to use .github/skills/"
  
elif [ "$SKILLS_CHOICE" = "both" ]; then
  # User chose BOTH directories
  # Add a note at the beginning indicating both locations exist
  # Keep paths as /.claude/skills/ (the cross-platform default)
  sed -i '/^# Agent Instructions/a\
\
> **📍 Skills Location:** This project has skills installed in both `/.claude/skills/` AND `/.github/skills/` for maximum compatibility. Links below use `/.claude/skills/` but both locations contain identical skills.\
' AGENTS.md
  echo "✅ Added dual-location note to AGENTS.md"

fi
# If user chose .claude/skills/ → no changes needed, keep original paths
```

---

## Step 9: Initialize bd (if selected)

**If user chose bd in Step 5:**

```bash
cd [project-root]
bd init

# Answer prompts based on detected environment:
# - Project name: [current directory name]
# - Git integration: [yes if git repo exists]
```

**Configure git hooks:**

```bash
# Run bd doctor to check for issues
bd doctor

# Install recommended hooks if suggested
bd doctor --fix
```

**Note:** If bd is already initialized, you can skip this step.

---

## Step 10: Platform-Specific Configuration

### For Claude Code:

1. Verify skills are in `.claude/skills/`
2. **CRITICAL:** Inform user:
   > ⚠️ **Claude Code must restart to load new skills.**
   >
   > Please **quit and restart** Claude Code now:
   > - macOS: Command+Q then relaunch
   > - Windows/Linux: Close completely and relaunch
3. After user restarts: "Welcome back! Your skills are now active. Run `bd list` to see your tasks."

### For GitHub Copilot:

1. Verify skills are in chosen directory (`.github/skills/` or `.claude/skills/` or both)
2. **Important:** Inform user:
   > ✅ **Skills installed for GitHub Copilot!**
   >
   > GitHub Copilot will automatically load skills from `$SKILLS_DIR` directory.
   >
   > **Note:** Agent Skills require:
   > - GitHub Copilot Chat or Copilot CLI
   > - VS Code or GitHub.com (Skills are loaded when relevant)
   >
   > See: [GitHub Copilot Agent Skills Documentation](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills)
3. Recommend: "Reload VSCode window (Ctrl+Shift+P / Cmd+Shift+P → 'Developer: Reload Window')"

### For Cursor:

1. Verify skills are in `.claude/skills/`
2. Inform user:
   > ✅ **Skills installed for Cursor!**
   >
   > Restart Cursor to load new skills:
   > - Close and relaunch Cursor
3. After restart: "Your skills are now available in Cursor."

### For Other:

1. Verify skills are in `.claude/skills/`
2. Inform user: "Skills installed in `.claude/skills/`. Refer to AGENTS.md for usage instructions."
3. Recommend: "Restart your editor/agent to load skills"

---

## Step 11: Git Commit (if git repository)

**If git repository exists:**

```bash
# Stage skills and AGENTS.md
git add "$SKILLS_DIR" AGENTS.md .gitignore 2>/dev/null || true

# Check if there are changes to commit
if ! git diff --cached --quiet; then
  echo "Creating commit for skills installation..."

  git commit -m "Add Agent Skills from Skills Catalog

Installed agent skills for AI coding assistants.

Skills directory: $SKILLS_DIR
Platform: $PLATFORM

Skills installed:
- Core: creating-skills, session-continuation, etc.
- [List other categories based on user selection]

🤖 Generated with Skills Catalog
https://github.com/All-The-Vibes/skills-catalog"

  echo "✅ Changes committed to git"

  # If remote exists, ask about pushing
  if git remote | grep -q origin; then
    # Ask user
    echo "Push changes to remote?"
    # If yes: git push origin [current-branch]
  fi
fi
```

---

## Step 12: Verification

**Run verification checks:**

```bash
# 1. Check skills installed
echo "Checking skills..."
ls -la "$SKILLS_DIR"

# 2. Check bd working (if installed)
if command -v bd &>/dev/null; then
  echo "Checking bd..."
  bd --version
fi

# 3. Check AGENTS.md exists
echo "Checking AGENTS.md..."
[ -f "AGENTS.md" ] && echo "✅ AGENTS.md found" || echo "❌ AGENTS.md missing"

# 4. Check git status
if [ "$GIT_REPO" = "true" ]; then
  echo "Checking git..."
  git status
fi

# 5. Try creating a test task (if bd installed)
if command -v bd &>/dev/null; then
  echo "Testing bd functionality..."
  bd create "Test task - setup verification" || true
  bd list || true
fi
```

**Success criteria:**

- ✅ Skills directory exists with skills
- ✅ `AGENTS.md` exists
- ✅ `bd` command works (if installed)
- ✅ Platform-specific setup complete

**If all checks pass:** Installation successful! 🎉

---

## Step 13: Next Steps

**Inform user:**

✅ **Setup Complete!**

**Your skills are installed in:** `$SKILLS_DIR`

**Platform:** `$PLATFORM`

**Getting started:**

1. **Read AGENTS.md** to understand the workflow
2. **Create your first task:** `bd create "Your first task"` (if using bd)
3. **Review available skills:** `ls $SKILLS_DIR/*/`

**Workflow patterns:**

- **Tech Leads:** Use `technical-lead-role` skill, delegate tasks
- **Individual Contributors:** Use `subagent` skill, execute tasks directly
- **Everyone:** Use `bd` for backlog management (if installed), `git` for version control

**Next task ideas:**

- `bd create "Set up CI/CD pipeline"` → Use `ci-cd` skill
- `bd create "Write project README"` → Use `technical-writing` skill
- `bd create "Refactor X module"` → Use `refactoring` skill
- `bd create "Add tests for Y feature"` → Use `tdd` skill

---

## Troubleshooting

### Issue: `bd: command not found` after installation

**Solution:**

```bash
# macOS/Linux: Add to PATH
export PATH="$HOME/.cargo/bin:$PATH"

# Add permanently to shell profile:
echo 'export PATH="$HOME/.cargo/bin:$PATH"' >> ~/.bashrc  # or ~/.zshrc
source ~/.bashrc

# Verify
which bd
bd --version
```

### Issue: Skills not loading in editor

**Claude Code:**
- Verify skills in `.claude/skills/`
- Quit completely (Command+Q) and restart
- Try clearing cache: `rm -rf .claude/.cache`

**GitHub Copilot:**
- Verify skills in `.github/skills/` or `.claude/skills/`
- Reload VSCode: Cmd/Ctrl+Shift+P → "Developer: Reload Window"
- Check Copilot is enabled in settings
- See: [GitHub Copilot Agent Skills Docs](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills)

**Cursor:**
- Verify skills in `.claude/skills/`
- Restart Cursor completely
- Check AI features are enabled in settings

### Issue: Git remote setup failed

**Solution:**

```bash
# Manual remote setup
git remote add origin <your-remote-url>

# Or use GitHub CLI
gh repo create <name> --public --source=. --remote=origin

# Verify
git remote -v
```

### Issue: Permission denied downloading skills

**Solution:**

```bash
# Fix permissions
chmod -R u+w "$SKILLS_DIR"

# If GitHub rate limited, authenticate:
# Install GitHub CLI: https://cli.github.com/
gh auth login
```

---

## Reference

**Full Documentation:** https://github.com/All-The-Vibes/skills-catalog

**GitHub Copilot Agent Skills:** https://docs.github.com/en/copilot/concepts/agents/about-agent-skills

**Available Skills:**

- **Core:** bd, git, subagent, technical-lead-role, task-delegation, creating-skills, session-continuation, backlog-workflow, git-hygiene
- **Engineering:** refactoring, tdd, architecture-review, performance-optimization
- **DevOps:** ci-cd, deployment, infrastructure, monitoring
- **Documentation:** technical-writing, api-documentation, adr
- **Research:** technical-research, evaluation, proof-of-concept

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

**Sources:**
- [About Agent Skills - GitHub Docs](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills)
- [Use Agent Skills in VS Code](https://code.visualstudio.com/docs/copilot/customization/agent-skills)
- [GitHub Copilot Agent Skills Announcement](https://github.blog/changelog/2025-12-18-github-copilot-now-supports-agent-skills/)
