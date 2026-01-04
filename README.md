#  Purple Canary 🐦‍⬛

**A Pi-hole plugin for detecting Pegasus spyware and commercial surveillance tools**

Purple Canary transforms your Pi-hole into a network sensor that monitors DNS queries for known indicators of compromise (IoCs) associated with Pegasus spyware and other commercial surveillance tools. By deploying distributed sensors across civil society, we increase the operational costs for spyware vendors and reduce the window of opportunity for zero-day exploits.

## WiP, Status: Just initiated

4.1.2026: Structure and WBS created

## 🎯 Mission

Commercial spyware like NSO Group's Pegasus has been used to target journalists, human rights defenders, and activists worldwide. While reactive detection cannot prevent zero-day exploits, widespread deployment of network sensors serves multiple strategic purposes:

- **Economic pressure**: Forces attackers to rotate infrastructure more frequently, increasing operational costs
- **Rapid attribution**: Enables faster identification and documentation of new attack campaigns
- **Deterrence**: Makes surveillance operations more visible and risky, particularly against lower-priority targets
- **Community defense**: Creates a distributed early warning system for civil society organizations

## 🔍 What is Pegasus?

Pegasus is sophisticated spyware developed by NSO Group that can compromise iOS and Android devices through:

- **Zero-click exploits**: No user interaction required, exploiting vulnerabilities in iMessage, WhatsApp, Apple Music, and iOS Photos
- **Network injection**: Attacks via compromised mobile operators or rogue cell towers
- **Spear-phishing**: Malicious SMS messages with embedded links

Once installed, Pegasus provides complete device access including messages, calls, camera, microphone, and location data.

## 📊 Data Sources

Purple Canary integrates indicators of compromise from leading digital rights organizations:

- **Amnesty International's Security Lab**: Technical investigations and IoC lists from documented cases
- **Citizen Lab (University of Toronto)**: Research on targeted surveillance and NSO Group infrastructure
- **Community contributions**: Additional indicators from security researchers and civil society

All IoCs are automatically synced from trusted sources and updated regularly.

## ✨ Features

### Core Functionality
- 🔄 **Automatic IoC updates** from Amnesty International and Citizen Lab repositories
- 🔎 **Real-time DNS query monitoring** against known Pegasus/spyware domains
- 🚨 **Configurable alerts** via ntfy.sh, email, Telegram, or Slack
- 📝 **Forensic logging** with timestamps, affected devices, and IoC sources
- 🛡️ **Privacy-focused** - all monitoring happens locally, no data leaves your network

### Optional Features
- 📊 Web dashboard for visualization of detected queries
- 📤 Export functionality for forensic analysis (CSV/JSON)
- 🐳 Docker container support for easy deployment

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/yourusername/purple-canary.git
cd purple-canary

# Run the installer
sudo ./install.sh

# Configure alerts (optional)
sudo nano /etc/purple-canary/config.yml

# Start monitoring
sudo systemctl enable --now purple-canary
```


## 📋 Requirements

- Pi-hole v5.x or v6.x
- Debian/Ubuntu-based system (Raspberry Pi OS, DietPi, etc.)
- Python 3.8+ or Bash 4.0+
- Root/sudo access


## 🔔 Alert Configuration

Purple Canary supports multiple notification channels:

```yaml
alerts:
  enabled: true
  channels:
    - type: ntfy
      url: https://ntfy.sh/your-topic
    - type: email
      smtp_server: smtp.example.com
      recipient: security@example.org
```


## 🤝 Contributing

This is a community-driven project. We welcome contributions of all kinds:

- **IoC sources**: Know of additional threat intelligence feeds?
- **Code improvements**: Bug fixes, new features, optimizations
- **Documentation**: Translations, tutorials, case studies
- **Testing**: Report issues or test on different Pi-hole configurations

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## ⚠️ Limitations

**Important**: Purple Canary is a reactive detection system. It can only detect known IoCs that have been documented and published. It provides:

- ✅ Detection of historical and documented spyware infrastructure
- ✅ Attribution and documentation of attempted connections
- ✅ Community early warning when infrastructure is reused

It does **not** provide:

- ❌ Protection against new zero-day exploits
- ❌ Detection of unknown Command \& Control servers
- ❌ Prevention of device compromise
- ❌ Complete security against targeted surveillance

Think of Purple Canary as one layer in a defense-in-depth strategy, not a complete solution.

## 📚 Learn More

- [Amnesty International: Forensic Methodology Report](https://www.amnesty.org/en/latest/research/2021/07/forensic-methodology-report-how-to-catch-nso-groups-pegasus/)
- [Citizen Lab: NSO Group Research](https://citizenlab.ca/tag/nso-group/)
- [AmnestyTech IoC Repository](https://github.com/AmnestyTech/investigations)
- [Mobile Verification Toolkit](https://github.com/mvt-project/mvt)


## 📄 License

[Apache 2.0](LICENSE) or [GPL-3.0](LICENSE-GPL) - choose the license that works best for your use case.

## 🙏 Acknowledgments

- Amnesty International's Security Lab for forensic research and IoC publication
- Citizen Lab at the University of Toronto for surveillance research
- The Pi-hole community for building essential privacy infrastructure
- All journalists, activists, and human rights defenders who contributed to exposing commercial surveillance


## ⚖️ Ethical Use

This tool is designed to protect civil society from unlawful surveillance. Please use it responsibly and in compliance with applicable laws in your jurisdiction.


