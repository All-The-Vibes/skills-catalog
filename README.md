# Skills Catalog

**Supercharge your AI coding workflow with standardized agent skills**

A comprehensive collection of reusable Agent Skills for Claude Code, GitHub Copilot, Cursor, and other AI coding assistants. Install once, use everywhere.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Agent Skills Standard](https://img.shields.io/badge/Agent%20Skills-Standard-blue)](https://agentskills.io)

---

## ✨ What Is This?

The **Skills Catalog** is a curated collection of **Agent Skills** that teach AI coding assistants how to:

- 📋 Manage backlogs and tasks systematically
- 🔄 Follow git hygiene and version control best practices
- 🏗️ Refactor code safely and effectively
- ✅ Implement test-driven development (TDD)
- 🚀 Set up CI/CD pipelines
- 📝 Write excellent technical documentation
- 🔬 Conduct systematic technical research
- 👔 Orchestrate multi-agent workflows (tech leads)

**Key Features:**

- ✅ **Automated Setup** — AI agents install everything autonomously
- ✅ **Works Everywhere** — Claude Code, GitHub Copilot, Cursor, and more
- ✅ **Open Standard** — Based on [Agent Skills](https://agentskills.io)
- ✅ **Production Ready** — Battle-tested across multiple real projects
- ✅ **Extensible** — Create custom skills for your team

---

## 🚀 Quick Start

### Option 1: AI Agent Installation (Recommended)

**Let your AI agent install everything automatically:**

#### For Claude Code:

```plaintext
Read and execute: https://raw.githubusercontent.com/All-The-Vibes/skills-catalog/main/AGENT_START.md
```

#### For GitHub Copilot / VSCode:

```plaintext
Read and execute: https://raw.githubusercontent.com/All-The-Vibes/skills-catalog/main/AGENT_START.md
```

#### For Cursor:

```plaintext
Read and execute: https://raw.githubusercontent.com/All-The-Vibes/skills-catalog/main/AGENT_START.md
```

**That's it!** The agent will:
- ✅ Detect your environment
- ✅ Install bd (beads) for task management
- ✅ Ask which skills you need
- ✅ Download and configure everything
- ✅ Verify the installation

---

### Option 2: Manual Installation

**Prefer to install manually?** See [INSTALLATION_GUIDE.md](INSTALLATION_GUIDE.md) for detailed step-by-step instructions.

**Quick manual install:**

```bash
# 1. Install bd (beads)
curl -fsSL https://raw.githubusercontent.com/ezrasingh/beads/main/install.sh | sh

# 2. Initialize bd in your project
cd /path/to/your/project
bd init

# 3. Download skills
git clone https://github.com/All-The-Vibes/skills-catalog.git /tmp/skills-catalog
cp -r /tmp/skills-catalog/.claude/skills .claude/
cp /tmp/skills-catalog/AGENTS.md AGENTS.md
rm -rf /tmp/skills-catalog

# 4. Restart your editor/agent
```

---

## 📚 What's Included

### Core Skills (Essential)

Located in `.claude/skills/core/`:

| Skill | Purpose |
|-------|---------|
| **bd** | Task management with beads CLI |
| **git** | Version control hygiene for multi-agent work |
| **subagent** | Delegate complex tasks to specialized agents |
| **technical-lead-role** | Orchestrate multi-agent workflows (for tech leads) |
| **task-delegation** | Effective work delegation patterns |
| **creating-skills** | Learn to author new agent skills |
| **session-continuation** | Maintain context across sessions |

### Engineering Skills

Located in `.claude/skills/engineering/`:

| Skill | Purpose |
|-------|---------|
| **refactoring** | Safe code restructuring with systematic methodology |
| **tdd** | Test-Driven Development practices and patterns |

### DevOps Skills

Located in `.claude/skills/devops/`:

| Skill | Purpose |
|-------|---------|
| **ci-cd** | Continuous Integration/Deployment best practices |

### Documentation Skills

Located in `.claude/skills/documentation/`:

| Skill | Purpose |
|-------|---------|
| **technical-writing** | Write clear, effective technical documentation |

### Research Skills

Located in `.claude/skills/research/`:

| Skill | Purpose |
|-------|---------|
| **technical-research** | Systematic technical investigation and analysis |

**Not sure which skills you need?** See [SKILL_SELECTOR.md](SKILL_SELECTOR.md) for guidance.

---

## 🎯 How It Works

Skills are markdown files that teach AI agents specialized capabilities:

1. **Agent reads AGENTS.md** — Understands the workflow
2. **Skills activate automatically** — Based on task type and role
3. **Agent follows skill guidance** — Step-by-step instructions
4. **Work gets done right** — Following best practices

### Example Usage

**Create a task:**
```bash
bd create "Refactor authentication module"
```

**Tell your agent:**
```plaintext
Use the refactoring skill to safely refactor the auth module
```

**Agent executes following the skill:**
- ✅ Analyzes current code structure
- ✅ Identifies refactoring opportunities
- ✅ Makes changes incrementally with tests
- ✅ Verifies functionality preserved
- ✅ Commits with clear messages

---

## 📖 Documentation

| Document | Purpose |
|----------|---------|
| [AGENT_START.md](AGENT_START.md) | Automated setup for AI agents |
| [INSTALLATION_GUIDE.md](INSTALLATION_GUIDE.md) | Manual installation instructions |
| [SKILL_SELECTOR.md](SKILL_SELECTOR.md) | Choose the right skills for your needs |
| [VERIFICATION_CHECKLIST.md](VERIFICATION_CHECKLIST.md) | Verify your installation |
| [AGENTS.md](AGENTS.md) | Workflow patterns and best practices |

---

## 🎓 Learn More

### For Users

- **Getting Started:** Use automated setup with your AI agent
- **Choosing Skills:** Read [SKILL_SELECTOR.md](SKILL_SELECTOR.md)
- **Understanding Workflows:** Read [AGENTS.md](AGENTS.md)

### For Contributors

- **Creating Skills:** See `.claude/skills/core/creating-skills/SKILL.md`
- **Contributing:** Submit PRs with new or improved skills
- **Standards:** Follow the [Agent Skills open standard](https://agentskills.io)

## 🏗️ Project Structure

```
skills-catalog/
├── README.md                           # You are here
├── AGENT_START.md                      # Automated setup for AI agents
├── INSTALLATION_GUIDE.md               # Manual installation guide
├── SKILL_SELECTOR.md                   # Help choosing skills
├── VERIFICATION_CHECKLIST.md           # Verify installation
├── AGENTS.md                           # Workflow patterns
├── .gitignore                          # Git ignore rules
└── .claude/
    └── skills/
        ├── core/                       # Essential skills
        │   ├── bd/
        │   ├── git/
        │   ├── subagent/
        │   ├── technical-lead-role/
        │   ├── task-delegation/
        │   ├── creating-skills/
        │   └── session-continuation/
        ├── engineering/                # Software development
        │   ├── refactoring/
        │   └── tdd/
        ├── devops/                     # Infrastructure & deployment
        │   └── ci-cd/
        ├── documentation/              # Writing & docs
        │   └── technical-writing/
        └── research/                   # Investigation & analysis
            └── technical-research/
```

---

## Core Principles

The skills in this catalog follow these principles:

### 1. Be Declarative
- State intent before acting
- Track all work in backlog
- No silent work

### 2. Be Current
- Always pull before reading/editing
- Make decisions on current state
- When in doubt, pull

### 3. Be Focused
- One issue, one task
- Stay in scope
- Finish before starting new work

### 4. Be Transparent
- Update issue status
- Commit frequently
- Report blockers immediately

### 5. Be Complete
- Push commits before stopping
- Sync backlog
- Never leave work stranded

### 6. Respect User Time
- Test before presenting
- Fix obvious issues
- Verify it works

### 7. Ruthless Simplicity
- Every line must justify its existence
- No stubs or placeholders
- Build working code or don't build it

---

## 🛠️ Customization

### Creating New Skills

Use the `creating-skills` skill as your guide:

```bash
# Read the creating-skills skill
cat .claude/skills/core/creating-skills/SKILL.md

# Or ask your agent
"Use the creating-skills skill to create a new [skill-name] skill"
```

**All skills follow the [Agent Skills open standard](https://agentskills.io)**

### Modifying Existing Skills

Skills are markdown files — edit them to fit your workflow:

```bash
# Edit any skill
vim .claude/skills/core/git/SKILL.md

# Commit changes
git add .claude/skills/core/git/SKILL.md
git commit -m "docs: customize git skill for our workflow"
```

### Removing Unneeded Skills

Simply delete skill directories you don't use:

```bash
# Remove skills not relevant to your project
rm -rf .claude/skills/research  # If not doing research work
```

---

## 💡 Use Cases

### For Solo Developers

- ✅ Task management with bd
- ✅ Git best practices
- ✅ Refactoring guidance
- ✅ TDD support
- ✅ CI/CD setup

### For Tech Leads

- ✅ Multi-agent orchestration
- ✅ Task delegation patterns
- ✅ Team workflow coordination
- ✅ Code review guidance
- ✅ Documentation standards

### For Teams

- ✅ Shared skill library
- ✅ Consistent practices
- ✅ Onboarding new members
- ✅ Cross-project reuse
- ✅ Custom skill creation

---

## 🤝 Contributing

We welcome contributions!

### Adding New Skills

1. Use the `creating-skills` skill to create your skill
2. Place it in the appropriate category
3. Follow the [Agent Skills standard](https://agentskills.io)
4. Test with real AI agents
5. Submit a pull request

### Improving Existing Skills

1. Edit the `SKILL.md` file
2. Keep the format consistent
3. Add examples and clarity
4. Test your changes
5. Submit a pull request

### Reporting Issues

Found a problem? [Open an issue](https://github.com/All-The-Vibes/skills-catalog/issues) with:
- Skill name
- Issue description
- Expected vs actual behavior
- Steps to reproduce

---

## 📜 License

MIT License — Use freely in your projects.

See [LICENSE](LICENSE) for details.

---

## 🙏 Acknowledgments

This catalog consolidates and standardizes skills developed and refined across multiple production projects, adapted into a general-purpose, standardized format for any software development workflow.

## ❓ FAQ

**Q: How do skills activate?**
A: Automatically based on your role (tech lead vs individual contributor) and task description. Skills can also be explicitly referenced.

**Q: Can I use this with GitHub Copilot / Cursor / other agents?**
A: Yes! Skills are standard markdown files readable by any AI coding assistant.

**Q: Do I need to install all skills?**
A: No. Use [SKILL_SELECTOR.md](SKILL_SELECTOR.md) to choose what you need, or install everything and ignore what you don't use.

**Q: Can I modify skills for my team?**
A: Absolutely! Skills are designed to be customized. Edit the SKILL.md files to fit your workflow.

**Q: How do I create custom skills?**
A: Use the `creating-skills` skill as your guide. It teaches the standard format and best practices.

**Q: What's the difference between bd and Backlog MCP?**
A: Both manage backlogs. bd is a standalone CLI tool, Backlog MCP is an MCP server that integrates with editors. Choose based on your preference.

---

## 🚀 Get Started Now

**For AI-driven setup:**
```plaintext
Read and execute: https://raw.githubusercontent.com/All-The-Vibes/skills-catalog/main/AGENT_START.md
```

**For manual setup:**
See [INSTALLATION_GUIDE.md](INSTALLATION_GUIDE.md)

**Need help choosing skills?**
See [SKILL_SELECTOR.md](SKILL_SELECTOR.md)

---

**Last Updated:** 2026-01-09
**Version:** 1.0
**License:** MIT
