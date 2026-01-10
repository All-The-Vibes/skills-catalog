# Skills Catalog Setup Verification Checklist

**For AI Agents and Human Installers**

Use this checklist to verify that the Skills Catalog has been installed correctly.

---

## Quick Verification

Run these commands and check for success:

```bash
# 1. Check bd is installed
bd --version

# 2. Check skills directory exists
ls -la .claude/skills/

# 3. Check AGENTS.md exists
ls -la AGENTS.md

# 4. Test bd functionality
bd create "Verification test task"
bd list
# bd close [task-id]  # Close the test task after confirming it works
```

**All passing?** ✅ You're good to go!

**Something failed?** See detailed checks below.

---

## Detailed Verification

### 1. Prerequisites

#### ✅ Git Installed

```bash
git --version
```

**Expected:** `git version X.Y.Z`

**If failed:**
- Install git: https://git-scm.com/downloads
- Restart terminal after installation

---

#### ✅ curl or wget Installed

```bash
curl --version || wget --version
```

**Expected:** Version output from curl or wget

**If failed:**
- Install curl: `brew install curl` (macOS) or `apt-get install curl` (Linux)
- Or install wget: `brew install wget` (macOS) or `apt-get install wget` (Linux)

---

### 2. bd (beads) Installation

#### ✅ bd Command Available

```bash
which bd
```

**Expected:** `/path/to/.cargo/bin/bd` or similar

**If failed:**
- Install bd: `curl -fsSL https://raw.githubusercontent.com/ezrasingh/beads/main/install.sh | sh`
- Or: `cargo install beads-cli`

---

#### ✅ bd Version Check

```bash
bd --version
```

**Expected:** `beads-cli X.Y.Z`

**If failed:**
- Reinstall bd
- Check PATH includes `$HOME/.cargo/bin`

---

#### ✅ bd in PATH

```bash
echo $PATH | grep -q ".cargo/bin" && echo "✅ bd in PATH" || echo "❌ .cargo/bin not in PATH"
```

**Expected:** `✅ bd in PATH`

**If failed:**
```bash
export PATH="$HOME/.cargo/bin:$PATH"
# Add to ~/.bashrc or ~/.zshrc permanently:
echo 'export PATH="$HOME/.cargo/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

---

### 3. Project Initialization

#### ✅ bd Initialized in Project

```bash
[ -d "backlog" ] && echo "✅ bd initialized" || echo "❌ bd not initialized"
```

**Expected:** `✅ bd initialized`

**If failed:**
```bash
bd init
# Answer prompts: project name, MCP/CLI choice, git integration
```

---

#### ✅ Backlog Configuration Exists

```bash
ls -la backlog/.backlog-config.yaml
```

**Expected:** File exists

**If failed:**
- Run `bd init` to create configuration

---

#### ✅ Backlog File Exists

```bash
ls -la backlog/BACKLOG.md
```

**Expected:** File exists

**If failed:**
- Run `bd init` to create BACKLOG.md

---

### 4. Skills Installation

#### ✅ Skills Directory Exists

```bash
[ -d ".claude/skills" ] && echo "✅ Skills directory exists" || echo "❌ No skills directory"
```

**Expected:** `✅ Skills directory exists`

**If failed:**
```bash
mkdir -p .claude/skills
```

---

#### ✅ Core Skills Installed

```bash
ls -la .claude/skills/core/
```

**Expected:** Subdirectories for skills like:
- `bd/`
- `git/`
- `subagent/`
- `creating-skills/`
- `session-continuation/`
- `technical-lead-role/`
- `task-delegation/`

**If failed:**
- Download skills from catalog
- See [INSTALLATION_GUIDE.md](INSTALLATION_GUIDE.md)

---

#### ✅ Skills Have Valid SKILL.md Files

```bash
# Check a few skill files exist and have content
for skill in bd git subagent creating-skills; do
  if [ -f ".claude/skills/core/$skill/SKILL.md" ]; then
    echo "✅ $skill: SKILL.md exists"
  else
    echo "❌ $skill: SKILL.md missing"
  fi
done
```

**Expected:** All checked skills have SKILL.md

**If failed:**
- Re-download missing skills

---

#### ✅ Skills Have Valid Frontmatter

```bash
# Check creating-skills has proper YAML frontmatter
head -5 .claude/skills/core/creating-skills/SKILL.md
```

**Expected:** Should start with:
```yaml
---
name: creating-skills
description: ...
---
```

**If failed:**
- Skill file is malformed
- Re-download the skill

---

### 5. AGENTS.md Workflow File

#### ✅ AGENTS.md Exists

```bash
[ -f "AGENTS.md" ] && echo "✅ AGENTS.md exists" || echo "❌ AGENTS.md missing"
```

**Expected:** `✅ AGENTS.md exists`

**If failed:**
```bash
curl -fsSL https://raw.githubusercontent.com/All-The-Vibes/skills-catalog/main/AGENTS.md \
  -o AGENTS.md
```

---

#### ✅ AGENTS.md Has Content

```bash
wc -l AGENTS.md | awk '{print $1}' | (read lines; [ "$lines" -gt 50 ] && echo "✅ AGENTS.md has content" || echo "❌ AGENTS.md too short")
```

**Expected:** `✅ AGENTS.md has content`

**If failed:**
- Re-download AGENTS.md

---

### 6. bd Functionality

#### ✅ Can Create Tasks

```bash
bd create "Verification: Test task creation" > /dev/null && echo "✅ Task creation works"
```

**Expected:** `✅ Task creation works`

**If failed:**
- Check bd is initialized: `bd init`
- Check permissions on backlog/

---

#### ✅ Can List Tasks

```bash
bd list | grep -q "Verification" && echo "✅ Task listing works"
```

**Expected:** `✅ Task listing works`

**If failed:**
- Verify task was created
- Check backlog/BACKLOG.md exists

---

#### ✅ Can Close Tasks

```bash
# Get the task ID for the verification task
TASK_ID=$(bd list | grep "Verification" | awk '{print $1}')
if [ -n "$TASK_ID" ]; then
  bd close "$TASK_ID" > /dev/null && echo "✅ Task closing works"
else
  echo "❌ No verification task found to close"
fi
```

**Expected:** `✅ Task closing works`

**If failed:**
- Check bd commands are working
- Verify backlog/BACKLOG.md is writable

---

### 7. Git Integration

#### ✅ Git Repository Initialized

```bash
git status > /dev/null 2>&1 && echo "✅ Git repo initialized" || echo "❌ Not a git repo"
```

**Expected:** `✅ Git repo initialized`

**If failed (optional):**
```bash
git init
```

---

#### ✅ Git Can Track Skills

```bash
git add .claude/skills/ AGENTS.md > /dev/null 2>&1 && echo "✅ Git can track files"
```

**Expected:** `✅ Git can track files`

**If failed:**
- Check .gitignore doesn't exclude these files
- Check file permissions

---

### 8. Environment-Specific Checks

#### For Claude Code:

##### ✅ Claude Code Recognizes Skills Directory

```bash
[ -d ".claude" ] && echo "✅ Claude Code directory exists" || echo "❌ Not in Claude Code project"
```

**Expected:** `✅ Claude Code directory exists`

**Action required:**
- Restart Claude Code (Command+Q, relaunch)
- After restart, ask Claude: "What skills do you have?"

---

#### For GitHub Copilot / VSCode:

##### ✅ VSCode Settings Exist

```bash
[ -f ".vscode/settings.json" ] && echo "✅ VSCode settings exist" || echo "❌ No VSCode settings"
```

**Expected (if using VSCode):** `✅ VSCode settings exist`

**Action required:**
- Reload VSCode window
- Open Copilot Chat
- Ask: "What skills are available?"

---

#### For Cursor:

##### ✅ Cursor Directory Exists

```bash
[ -d ".cursor" ] && echo "✅ Cursor directory exists" || echo "❌ Not in Cursor project"
```

**Expected (if using Cursor):** `✅ Cursor directory exists`

**Action required:**
- Restart Cursor
- Open AI chat
- Ask: "What skills do you have access to?"

---

### 9. Agent Recognition (Manual Check)

**For AI Agents performing this verification:**

#### ✅ Agent Can See Skills

**Instruction:** List all skills you can access from `.claude/skills/`.

**Expected response:** Agent should list skills by category:
- Core: bd, git, subagent, technical-lead-role, task-delegation, creating-skills, session-continuation
- Engineering: refactoring, tdd
- DevOps: ci-cd
- Documentation: technical-writing
- Research: technical-research

**If failed:**
- Restart editor/agent
- Manually reference a skill: "Read .claude/skills/core/creating-skills/SKILL.md"

---

#### ✅ Agent Can Load AGENTS.md

**Instruction:** Read and summarize the workflow described in AGENTS.md.

**Expected response:** Agent should describe:
- Tech lead orchestration pattern
- Task delegation with Task tool
- Use of bd for backlog management
- Git hygiene practices

**If failed:**
- Verify AGENTS.md exists: `ls -la AGENTS.md`
- Manually load: "Read AGENTS.md and explain the workflow"

---

### 10. Integration Test

#### ✅ End-to-End Workflow Test

**Instructions for agent:**

1. Create a task: `bd create "Integration test: Write a hello world function"`
2. List tasks: `bd list` (confirm task appears)
3. Use a skill: "Use the creating-skills skill to understand the skill format"
4. Close task: `bd close [task-id]`
5. Verify task closed: `bd list` (confirm task no longer open)

**Expected:** All steps complete successfully

**If failed:** Review specific failures above

---

## Summary Checklist

**Prerequisites:**

- [ ] Git installed and working
- [ ] curl or wget available

**bd (beads):**

- [ ] bd installed
- [ ] bd in PATH
- [ ] bd initialized in project
- [ ] backlog/ directory exists
- [ ] Can create, list, and close tasks

**Skills:**

- [ ] .claude/skills/ directory exists
- [ ] Core skills installed
- [ ] Skills have valid SKILL.md files
- [ ] Skills have proper frontmatter

**Workflow:**

- [ ] AGENTS.md exists and has content
- [ ] Git repo initialized (optional but recommended)

**Environment:**

- [ ] Editor/agent restarted (Claude Code, VSCode, Cursor)
- [ ] Agent recognizes skills
- [ ] Agent can load AGENTS.md

**Integration:**

- [ ] End-to-end task workflow works

---

## Success!

**If all checks pass:** ✅ Setup is complete and verified!

**Next steps:**
1. Read AGENTS.md for workflow guidance
2. Create your first real task: `bd create "Your task here"`
3. Start using skills in your work

---

## Failed Checks?

**If any checks failed:**

1. Review the specific failure above
2. Follow the remediation steps
3. Re-run the verification
4. If still failing, see [INSTALLATION_GUIDE.md](INSTALLATION_GUIDE.md) troubleshooting

**Need help?**
- Open an issue: https://github.com/All-The-Vibes/skills-catalog/issues
- Check documentation: https://github.com/All-The-Vibes/skills-catalog

---

## Automated Verification Script

**Want to run all checks automatically?**

Save this as `verify-setup.sh`:

```bash
#!/bin/bash
# Skills Catalog Setup Verification Script

echo "🔍 Verifying Skills Catalog Setup..."
echo ""

# Prerequisites
echo "1️⃣ Prerequisites"
git --version > /dev/null 2>&1 && echo "  ✅ Git installed" || echo "  ❌ Git not found"
(curl --version > /dev/null 2>&1 || wget --version > /dev/null 2>&1) && echo "  ✅ curl/wget available" || echo "  ❌ curl/wget not found"
echo ""

# bd installation
echo "2️⃣ bd (beads)"
which bd > /dev/null 2>&1 && echo "  ✅ bd in PATH" || echo "  ❌ bd not in PATH"
bd --version > /dev/null 2>&1 && echo "  ✅ bd works" || echo "  ❌ bd not working"
[ -d "backlog" ] && echo "  ✅ bd initialized" || echo "  ❌ bd not initialized"
echo ""

# Skills
echo "3️⃣ Skills"
[ -d ".claude/skills" ] && echo "  ✅ Skills directory" || echo "  ❌ No skills directory"
[ -d ".claude/skills/core" ] && echo "  ✅ Core skills" || echo "  ❌ No core skills"
[ -f ".claude/skills/core/creating-skills/SKILL.md" ] && echo "  ✅ creating-skills" || echo "  ❌ creating-skills missing"
echo ""

# AGENTS.md
echo "4️⃣ Workflow"
[ -f "AGENTS.md" ] && echo "  ✅ AGENTS.md" || echo "  ❌ AGENTS.md missing"
echo ""

# bd functionality
echo "5️⃣ bd Functionality"
bd list > /dev/null 2>&1 && echo "  ✅ bd list works" || echo "  ❌ bd list failed"
echo ""

# Git
echo "6️⃣ Git"
git status > /dev/null 2>&1 && echo "  ✅ Git repo" || echo "  ⚠️  Not a git repo (optional)"
echo ""

echo "✅ Verification complete!"
echo ""
echo "Next: Read AGENTS.md and start creating tasks with 'bd create'"
```

**Run it:**

```bash
chmod +x verify-setup.sh
./verify-setup.sh
```

---

**Verification complete!** Your Skills Catalog is ready to use. 🎉
