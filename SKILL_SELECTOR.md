# Skill Selector Guide

**Choose the Right Skills for Your Project**

This guide helps you decide which skills to install from the catalog based on your role, project type, and workflow needs.

---

## Quick Recommendation

**Not sure what to install?** Start with these:

### Essentials (Everyone)

- **creating-skills** — Learn to create new skills
- **session-continuation** — Maintain context across sessions
- **bd** — Task management with beads CLI
- **git** — Version control hygiene
- **subagent** — Delegate complex tasks

### Add based on role:

- **Tech Leads:** + `technical-lead-role`, `task-delegation`
- **Engineers:** + `refactoring`, `tdd`
- **DevOps:** + `ci-cd`
- **Documentation Writers:** + `technical-writing`
- **Researchers:** + `technical-research`

---

## Decision Tree

Follow this decision tree to select skills:

### Question 1: What is your primary role?

#### A. Tech Lead / Engineering Manager

**You orchestrate work across teams and delegate tasks.**

**Install these:**

| Skill | Category | Purpose |
|-------|----------|---------|
| `technical-lead-role` | core | Guides orchestration and delegation patterns |
| `task-delegation` | core | How to effectively delegate to agents/humans |
| `bd` | core | Manage backlog and track work |
| `git` | core | Version control hygiene for multi-agent work |
| `subagent` | core | Spawn specialized agents for complex tasks |
| `creating-skills` | core | Create custom skills for your team |
| `session-continuation` | core | Maintain context across sessions |

**Optional additions:**

- If you review code: + `refactoring`
- If you plan infrastructure: + `ci-cd`
- If you write RFCs/ADRs: + `technical-writing`

---

#### B. Software Engineer / Individual Contributor

**You write code, fix bugs, and implement features.**

**Install these:**

| Skill | Category | Purpose |
|-------|----------|---------|
| `bd` | core | Manage your tasks |
| `git` | core | Version control best practices |
| `subagent` | core | Delegate complex subtasks |
| `creating-skills` | core | Create project-specific skills |
| `session-continuation` | core | Maintain context across sessions |
| `refactoring` | engineering | Safe code restructuring |
| `tdd` | engineering | Test-driven development |

**Optional additions:**

- If you work on CI/CD: + `ci-cd` (devops)
- If you write docs: + `technical-writing` (documentation)
- If you do research: + `technical-research` (research)

---

#### C. DevOps Engineer / SRE

**You manage infrastructure, deployments, and operational concerns.**

**Install these:**

| Skill | Category | Purpose |
|-------|----------|---------|
| `bd` | core | Manage infrastructure tasks |
| `git` | core | Version control for IaC |
| `subagent` | core | Delegate complex ops tasks |
| `creating-skills` | core | Create ops-specific skills |
| `session-continuation` | core | Maintain context |
| `ci-cd` | devops | Continuous integration/deployment patterns |

**Optional additions:**

- If you write runbooks: + `technical-writing` (documentation)
- If you refactor IaC: + `refactoring` (engineering)
- If you evaluate tools: + `technical-research` (research)

---

#### D. Technical Writer / Documentation Specialist

**You create documentation, guides, and educational content.**

**Install these:**

| Skill | Category | Purpose |
|-------|----------|---------|
| `bd` | core | Manage documentation tasks |
| `git` | core | Version control for docs |
| `subagent` | core | Delegate research/writing subtasks |
| `creating-skills` | core | Create writing-specific skills |
| `session-continuation` | core | Maintain context |
| `technical-writing` | documentation | Documentation best practices |

**Optional additions:**

- If you research topics: + `technical-research` (research)
- If you document code: + `refactoring` (to understand code structure)

---

#### E. Researcher / Analyst

**You investigate technologies, evaluate options, and produce reports.**

**Install these:**

| Skill | Category | Purpose |
|-------|----------|---------|
| `bd` | core | Manage research tasks |
| `git` | core | Version control for research artifacts |
| `subagent` | core | Delegate research subtasks |
| `creating-skills` | core | Create research-specific skills |
| `session-continuation` | core | Maintain context |
| `technical-research` | research | Systematic research methodology |

**Optional additions:**

- If you write reports: + `technical-writing` (documentation)
- If you prototype: + `tdd`, `refactoring` (engineering)

---

### Question 2: What type of project is this?

#### New Project / Greenfield

**Starting from scratch.**

**Recommended:**

- Core skills (bd, git, subagent, creating-skills, session-continuation)
- `tdd` — Build with tests from day one
- `ci-cd` — Set up automation early
- `technical-writing` — Document as you go

**Why:** Establish good practices from the start.

---

#### Legacy Project / Brownfield

**Working with existing code that needs improvement.**

**Recommended:**

- Core skills (bd, git, subagent, creating-skills, session-continuation)
- `refactoring` — Safely improve existing code
- `tdd` — Add tests to legacy code
- `technical-research` — Understand existing architecture

**Why:** Focus on understanding and improving existing systems.

---

#### Infrastructure / Platform Project

**Building or maintaining infrastructure, tooling, or platforms.**

**Recommended:**

- Core skills (bd, git, subagent, creating-skills, session-continuation)
- `ci-cd` — Automate deployments
- `technical-writing` — Document systems and runbooks

**Why:** Infrastructure needs automation and clear documentation.

---

#### Documentation Project

**Creating or updating documentation, guides, or knowledge bases.**

**Recommended:**

- Core skills (bd, git, subagent, creating-skills, session-continuation)
- `technical-writing` — Documentation best practices
- `technical-research` — Gather and verify information

**Why:** Focus on writing quality and research thoroughness.

---

### Question 3: Team size and workflow

#### Solo Developer

**You work alone or mostly independently.**

**Recommended:**

- Core skills: bd, git, subagent, creating-skills, session-continuation
- Role-specific: Based on your role (Q1)

**Skip:**

- `technical-lead-role` (you don't need orchestration)
- `task-delegation` (you don't delegate to others)

---

#### Small Team (2-5 people)

**You collaborate closely with a small group.**

**Recommended:**

- Core skills: bd, git, subagent, creating-skills, session-continuation
- Role-specific: Based on your role (Q1)
- If you coordinate: + `technical-lead-role`, `task-delegation`

**Why:** Coordination helps but isn't as critical as large teams.

---

#### Large Team (6+ people)

**You work in a larger, more structured team.**

**Recommended:**

- Core skills: bd, git, subagent, creating-skills, session-continuation
- Role-specific: Based on your role (Q1)
- For leads: + `technical-lead-role`, `task-delegation` (essential!)
- For everyone: + `technical-writing` (documentation is critical at scale)

**Why:** Coordination, documentation, and process matter more at scale.

---

## Skill Categories Reference

### Core Skills

**Purpose:** Fundamental capabilities needed by most users.

| Skill | When to Use |
|-------|-------------|
| `bd` | Task management with beads CLI |
| `git` | Version control operations |
| `subagent` | Delegate complex subtasks to specialized agents |
| `technical-lead-role` | Orchestrate multi-agent workflows (leads only) |
| `task-delegation` | Effectively delegate to agents/humans (leads only) |
| `creating-skills` | Author new skills |
| `session-continuation` | Maintain context across sessions |

---

### Engineering Skills

**Purpose:** Software development and code quality.

| Skill | When to Use |
|-------|-------------|
| `refactoring` | Safe code restructuring and improvement |
| `tdd` | Test-driven development practices |

**Planned:**

- `code-review` — Code review best practices
- `debugging` — Systematic debugging methodology

---

### DevOps Skills

**Purpose:** Infrastructure, deployment, and operations.

| Skill | When to Use |
|-------|-------------|
| `ci-cd` | Continuous integration and deployment |

**Planned:**

- `deployment` — Deployment strategies and patterns
- `infrastructure` — Infrastructure as Code best practices
- `monitoring` — Observability and monitoring

---

### Documentation Skills

**Purpose:** Writing and knowledge management.

| Skill | When to Use |
|-------|-------------|
| `technical-writing` | Documentation, guides, and technical content |

**Planned:**

- `api-documentation` — API docs with OpenAPI/Swagger
- `adr` — Architecture Decision Records

---

### Research Skills

**Purpose:** Investigation, analysis, and evaluation.

| Skill | When to Use |
|-------|-------------|
| `technical-research` | Systematic technical research |

**Planned:**

- `evaluation` — Compare and evaluate alternatives
- `proof-of-concept` — Build and test POCs

---

## Installation Commands

Once you've decided which skills you need, install them:

### Option 1: Let an Agent Install (Recommended)

Tell your AI agent:

```
Read and execute https://raw.githubusercontent.com/All-The-Vibes/skills-catalog/main/AGENT_START.md
```

The agent will ask which skills you need based on this guide.

---

### Option 2: Manual Installation

**Download entire catalog:**

```bash
git clone https://github.com/All-The-Vibes/skills-catalog.git /tmp/skills-catalog
cp -r /tmp/skills-catalog/.claude/skills/* .claude/skills/
cp /tmp/skills-catalog/AGENTS.md AGENTS.md
rm -rf /tmp/skills-catalog
```

**Download specific skills:**

```bash
BASE_URL="https://raw.githubusercontent.com/All-The-Vibes/skills-catalog/main"

# Core skills
mkdir -p .claude/skills/core/bd
curl -fsSL "$BASE_URL/.claude/skills/core/bd/SKILL.md" \
  -o .claude/skills/core/bd/SKILL.md

# Repeat for each skill you need...
```

See [INSTALLATION_GUIDE.md](INSTALLATION_GUIDE.md) for detailed manual installation steps.

---

## Customization

**Don't see a skill you need?**

1. **Check the backlog** — It might be planned
   - See `backlog/BACKLOG.md` or `bd list` in the repo

2. **Create your own** — Use the `creating-skills` skill
   - Install `creating-skills`
   - Tell your agent: "Use the creating-skills skill to create a [your-skill-name] skill"

3. **Contribute back** — Share with the community
   - Submit a pull request to the skills-catalog repo
   - Others will benefit from your work!

---

## Examples

### Example 1: Solo Full-Stack Engineer

**Profile:** Building a new web app alone

**Install:**

- Core: bd, git, subagent, creating-skills, session-continuation
- Engineering: refactoring, tdd
- DevOps: ci-cd
- Documentation: technical-writing

**Why:** Covers full-stack development, testing, deployment, and documentation.

---

### Example 2: Tech Lead on 10-Person Team

**Profile:** Leading a team building a platform

**Install:**

- Core: technical-lead-role, task-delegation, bd, git, subagent, creating-skills, session-continuation
- Engineering: refactoring (for code reviews)
- DevOps: ci-cd (for platform deployment)
- Documentation: technical-writing (for RFCs, ADRs)

**Why:** Focus on coordination, delegation, and communication at scale.

---

### Example 3: DevOps Engineer Managing Infrastructure

**Profile:** Managing Kubernetes clusters and CI/CD pipelines

**Install:**

- Core: bd, git, subagent, creating-skills, session-continuation
- DevOps: ci-cd
- Documentation: technical-writing (for runbooks)
- Research: technical-research (for evaluating tools)

**Why:** Focus on infrastructure automation and operational documentation.

---

### Example 4: Technical Writer on Documentation Team

**Profile:** Writing API documentation and user guides

**Install:**

- Core: bd, git, subagent, creating-skills, session-continuation
- Documentation: technical-writing
- Research: technical-research (for understanding features)

**Why:** Focus on writing quality and research thoroughness.

---

## Summary

**Choosing skills:**

1. **Start with core skills** (everyone needs these)
2. **Add role-specific skills** (based on your primary role)
3. **Consider project type** (new vs legacy, infrastructure, etc.)
4. **Factor in team size** (coordination matters at scale)
5. **Install and iterate** (you can always add more later)

**Not sure?** Install everything! You can always ignore skills you don't need.

**Need help?** See:

- [AGENT_START.md](AGENT_START.md) — Automated installation
- [INSTALLATION_GUIDE.md](INSTALLATION_GUIDE.md) — Manual installation
- [AGENTS.md](AGENTS.md) — Workflow patterns
- [Creating an issue](https://github.com/All-The-Vibes/skills-catalog/issues) — Ask questions

---

**Ready to install?** Head to [INSTALLATION_GUIDE.md](INSTALLATION_GUIDE.md) or use [AGENT_START.md](AGENT_START.md) for automated setup.
