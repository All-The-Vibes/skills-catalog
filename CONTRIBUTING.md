# Contributing to Skills Catalog

Thank you for your interest in contributing to the Skills Catalog! This document provides guidelines for contributing to this project.

## 🎯 How to Contribute

### Reporting Issues

Found a bug or have a suggestion? Please open an issue on GitHub:

1. Check if the issue already exists
2. If not, create a new issue with:
   - Clear, descriptive title
   - Detailed description of the issue/suggestion
   - Steps to reproduce (for bugs)
   - Expected vs actual behavior
   - Your environment (AI agent type, OS, etc.)

### Contributing Skills

We welcome new skills and improvements to existing ones!

#### Creating a New Skill

1. **Read the Guidelines**
   - Read `.claude/skills/core/creating-skills/SKILL.md`
   - Follow the [Agent Skills Standard](https://agentskills.io)

2. **Fork and Clone**
   ```bash
   git clone https://github.com/All-The-Vibes/skills-catalog.git
   cd skills-catalog
   ```

3. **Create a Branch**
   ```bash
   git checkout -b skill/your-skill-name
   ```

4. **Create Your Skill**
   - Place in appropriate category (`core/`, `engineering/`, `devops/`, `documentation/`, `research/`)
   - Use YAML frontmatter (name and description)
   - Include clear examples
   - Follow the structure of existing skills

5. **Test Your Skill**
   - Test with real AI agents (Claude Code, Cursor, GitHub Copilot)
   - Verify it works as expected
   - Ensure no syntax errors

6. **Submit Pull Request**
   - Push your branch
   - Create a pull request with:
     - Clear title and description
     - Explanation of the skill's purpose
     - Examples of usage
     - Test results

#### Improving Existing Skills

1. **Fork and Clone** (same as above)

2. **Create a Branch**
   ```bash
   git checkout -b improve/skill-name
   ```

3. **Make Your Changes**
   - Maintain consistent formatting
   - Keep the existing structure
   - Add examples where helpful
   - Fix typos or clarify confusing sections

4. **Test Your Changes**
   - Verify the skill still works correctly
   - Test with AI agents if possible

5. **Submit Pull Request**

### Code Style

#### For Skills (Markdown)

- Use clear, concise language
- Include practical examples
- Use code blocks with syntax highlighting
- Structure sections logically
- Keep line length reasonable (80-120 chars when possible)

#### For Documentation

- Write for clarity
- Use headings appropriately (H1 for title, H2 for sections, etc.)
- Include examples
- Link to related documentation
- Keep it up to date

### Commit Messages

Follow conventional commit format:

```
type(scope): brief description

Longer description if needed

Examples:
- feat(skills): add database-design skill
- fix(git-hygiene): correct merge conflict example
- docs(readme): update installation instructions
- refactor(ci-cd): reorganize deployment section
```

**Types:**
- `feat`: New feature or skill
- `fix`: Bug fix
- `docs`: Documentation changes
- `refactor`: Code restructuring (no functional changes)
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

### Pull Request Process

1. **Ensure CI Passes**
   - All checks must pass
   - No merge conflicts

2. **Request Review**
   - Tag relevant maintainers
   - Respond to feedback promptly

3. **Address Feedback**
   - Make requested changes
   - Push additional commits
   - Re-request review

4. **Merge**
   - Maintainers will merge when approved
   - Your contribution will be credited

## 🏗️ Development Setup

### Prerequisites

- Git
- A text editor
- (Optional) AI coding assistant for testing

### Local Setup

```bash
# Clone the repository
git clone https://github.com/All-The-Vibes/skills-catalog.git
cd skills-catalog

# Install bd (for testing backlog features)
curl -fsSL https://raw.githubusercontent.com/ezrasingh/beads/main/install.sh | sh

# Test with your AI agent
# Open the project in your editor and test skills
```

## 📋 Skill Quality Checklist

Before submitting a skill, ensure:

- [ ] YAML frontmatter present (name and description)
- [ ] Clear "When to Use" section
- [ ] Practical examples included
- [ ] Code blocks properly formatted
- [ ] No typos or grammar errors
- [ ] Tested with at least one AI agent
- [ ] Follows existing skill structure
- [ ] No PII or sensitive information
- [ ] Appropriate category placement
- [ ] Links to related skills (if applicable)

## 🤝 Community Guidelines

### Be Respectful

- Be kind and respectful to all contributors
- Provide constructive feedback
- Welcome newcomers
- Assume good intentions

### Be Collaborative

- Discuss major changes in issues first
- Share knowledge and help others
- Give credit where due
- Work together towards quality

### Be Professional

- Keep discussions on-topic
- Avoid inflammatory language
- Focus on the work, not the person
- Accept decisions gracefully

## 📜 License

By contributing, you agree that your contributions will be licensed under the MIT License.

## ❓ Questions?

- **General Questions**: Open a discussion on GitHub
- **Bug Reports**: Open an issue
- **Security Issues**: See [SECURITY.md](SECURITY.md)

## 🙏 Thank You!

Your contributions make this project better for everyone. Thank you for taking the time to contribute!

---

**Maintained by:** All The Vibes
**License:** MIT
**Questions?** Open an issue or discussion on GitHub
