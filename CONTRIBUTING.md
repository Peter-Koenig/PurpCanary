# Contributing to Purple Canary

Thank you for your interest in Purple Canary! This project is in its early stages, and we're figuring things out as we go. Your contributions are welcome, and we'll keep the process simple and pragmatic.

## 🏗️ Project Status

Purple Canary is a **project in development**. Processes, conventions, and governance structures are still being established. Don't worry about getting everything perfect - we'll figure it out together.

## 🤝 How You Can Help

### 1. Code Contributions

We're building the core functionality from scratch. Here's what we need:

- **IoC integration scripts**: Fetching and parsing indicators from Amnesty International, Citizen Lab, and other sources
- **Query monitoring**: Python/Bash scripts to watch Pi-hole's FTL database for suspicious DNS queries
- **Alert systems**: Integration with ntfy.sh, email, Telegram, or other notification channels
- **Installation scripts**: Making deployment as simple as possible
- **Testing**: Trying Purple Canary on different Pi-hole versions and system configurations

**Getting started**: Just fork the repo, create a branch, and submit a PR. We'll review and discuss together.

### 2. Threat Intelligence

Know of additional IoC sources beyond Amnesty International and Citizen Lab?

- New spyware vendor domains or IP ranges
- Additional research publications with technical indicators
- Trusted threat intelligence feeds relevant to commercial surveillance tools

**Share it**: Open an issue with the source details and we'll evaluate integration.

### 3. Documentation

- **Translations**: Help make Purple Canary accessible in languages beyond English and German
- **Tutorials**: Write guides for specific Pi-hole setups (Docker, Proxmox LXC, DietPi, etc.)
- **Use cases**: Document how Purple Canary is deployed in NGOs, newsrooms, or research environments
- **Troubleshooting**: Help us build a knowledge base as issues arise

### 4. Testing & Bug Reports

Found a bug? Have an idea? Open an issue on GitHub:

- Describe what happened and what you expected
- Include your Pi-hole version and OS (e.g., "Pi-hole v5.18 on Raspberry Pi OS Bookworm")
- Share relevant logs if possible (redact sensitive information)
- Screenshots or terminal output are helpful

No need for formal bug report templates yet - just tell us what's going on.

### 5. Ideas & Feedback

This project exists to serve civil society organizations, journalists, and individuals concerned about surveillance. If you have ideas about:

- Additional features that would be useful
- Different deployment scenarios we should support
- Privacy or security considerations we haven't addressed
- Partnerships with organizations doing similar work

Open an issue or start a discussion. All input is valuable.

## 💻 Technical Guidelines

Since we're still establishing conventions, here are some loose guidelines:

### Code Style
- **Python**: Follow PEP 8 where reasonable, but readability > strict adherence
- **Bash**: Use shellcheck to catch common issues
- **Comments**: Explain *why*, not *what* - the code shows what it does

### Commits
- Write meaningful commit messages (a one-line summary is fine)
- No need for formal conventional commit format yet

### Dependencies
- Prefer standard library and tools already available on most Pi-hole systems
- Minimize external dependencies where possible
- Document any new dependencies clearly

### Privacy & Security
This is non-negotiable:

- **No telemetry**: Purple Canary does not phone home or collect usage data
- **Local-only processing**: All detection happens on the user's network
- **Secure defaults**: Logs should be readable only by root, alerts should use encrypted channels
- **Data minimization**: Only log what's necessary for detection and forensics

## 🔐 Security Issues

Found a security vulnerability? Please **do not** open a public issue.

For now, email the maintainer directly (we'll set up a proper disclosure process soon). Include:
- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Any suggested fixes

We'll work with you to address it responsibly.

## 📜 License

By contributing to Purple Canary, you agree that your contributions will be licensed under the same license as the project (Apache 2.0 or GPL-3.0, dual-licensed).

If you're submitting code you didn't write yourself, make sure you have the right to contribute it.

## 🌍 Community Guidelines

Keep it simple:

- **Be respectful**: We're all here to fight surveillance, not each other
- **Be patient**: Maintainers are volunteers with day jobs
- **Be constructive**: Criticism is welcome, but offer solutions when possible
- **Be inclusive**: Purple Canary is for everyone concerned about surveillance

## 📞 Getting in Touch

- **GitHub Issues**: For bugs, feature requests, and technical discussions
- **GitHub Discussions**: For questions, ideas, and general conversation (once enabled)
- **Email**: [coming soon - we need to set up a project email]

## 🙏 Thank You


