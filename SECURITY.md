# Security Policy

## Supported Versions

We currently support the following versions of Skills Catalog:

| Version | Supported          |
| ------- | ------------------ |
| 1.x     | :white_check_mark: |

## Reporting a Vulnerability

The Skills Catalog project takes security seriously. If you discover a security vulnerability, please follow these steps:

### Where to Report

**DO NOT** create a public GitHub issue for security vulnerabilities.

Instead, please report security issues by:

1. **Email:** Send details to the project maintainers at the organization level
2. **GitHub Security Advisory:** Use GitHub's private vulnerability reporting feature at https://github.com/All-The-Vibes/skills-catalog/security/advisories/new

### What to Include

When reporting a vulnerability, please include:

- A description of the vulnerability
- Steps to reproduce the issue
- Potential impact of the vulnerability
- Any suggested fixes or mitigations (optional)
- Your contact information for follow-up

### Response Timeline

- **Initial Response:** Within 48 hours of report submission
- **Status Update:** Within 7 days with assessment and timeline
- **Resolution:** Varies based on severity and complexity

### Security Considerations for Skills

Since this project contains AI agent skills that execute commands and manipulate files, please be especially vigilant about:

1. **Command Injection:** Skills that construct shell commands from user input
2. **Path Traversal:** Skills that handle file paths
3. **Credential Exposure:** Skills that might inadvertently log or expose secrets
4. **Malicious Prompts:** Skills that could be exploited through crafted prompts
5. **Privilege Escalation:** Skills that execute with elevated permissions

## Security Best Practices for Users

When using Skills Catalog:

1. **Review Skills:** Always review skill content before using them
2. **Limit Permissions:** Run AI agents with minimal required permissions
3. **Protect Secrets:** Never commit API keys, passwords, or tokens
4. **Verify Downloads:** Ensure skills are downloaded from official sources
5. **Keep Updated:** Regularly pull latest versions for security patches

## Known Security Considerations

### .beads/ Directory

The `.beads/` directory contains local state and is excluded from version control. This directory may contain:
- Local database files
- Issue/task metadata
- Daemon process information

Ensure `.beads/` remains in `.gitignore` to prevent accidental exposure of local data.

### Skill Execution

Skills contain instructions that AI agents execute. While we review all skills in the catalog:
- AI agents execute commands with your user permissions
- Skills may create, modify, or delete files
- Skills may execute shell commands
- Always review skill content before first use

### Git Operations

Skills may perform git operations including:
- Committing changes
- Pushing to remote repositories
- Creating branches
- Merging code

Ensure you understand what operations a skill performs before using it in production repositories.

## Disclosure Policy

When a security issue is resolved:

1. We will publish a security advisory on GitHub
2. We will credit the reporter (unless they prefer to remain anonymous)
3. We will document the vulnerability and fix in release notes
4. We will notify users through appropriate channels

## Questions?

For non-security related issues, please use GitHub Issues.

For security concerns, please follow the reporting process above.

---

**Last Updated:** 2026-01-10
**Maintained by:** All The Vibes
