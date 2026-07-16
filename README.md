# skill-share-cli-mcp

# SkillShare Installation Guide

> **Latest Releases**
>
> * CLI: **v1.0.2**
> * MCP Server: **v1.0.1**
>
> These releases fix issues with standalone binaries on Linux, macOS, and Windows, and add automatic support for corporate TLS inspection proxies such as Zscaler and Netskope.
>
> If you installed an earlier version, we recommend reinstalling to receive these updates.

---

# Install

## SkillShare CLI (`skillshare`)

### Linux / macOS

```bash
curl -fsSL https://raw.githubusercontent.com/Aniket-think41/skillshare-cli/main/install.sh | bash
```

### Windows (PowerShell)

```powershell
irm https://raw.githubusercontent.com/Aniket-think41/skillshare-cli/main/install.ps1 | iex
```

### Direct Binary Installation (Without Install Script)

#### Linux (x86_64)

```bash
curl -fsSL https://github.com/Aniket-think41/skillshare-cli/releases/latest/download/skillshare-linux-amd64 -o skillshare
chmod +x skillshare
sudo mv skillshare /usr/local/bin/
```

#### macOS (Apple Silicon)

```bash
curl -fsSL https://github.com/Aniket-think41/skillshare-cli/releases/latest/download/skillshare-macos-arm64 -o skillshare
chmod +x skillshare
sudo mv skillshare /usr/local/bin/
```

#### Windows

1. Download `skillshare-windows-amd64.exe` from the latest GitHub release.
2. Rename it to `skillshare.exe`.
3. Add the executable's location to your system `PATH`.

### Verify Installation

```bash
skillshare --help
```

### Login

```bash
skillshare login
```

---

# MCP Server (`skillshare-mcp`)

### Linux / macOS

```bash
curl -fsSL https://raw.githubusercontent.com/Aniket-think41/skillshare-mcp/main/install.sh | bash
```

### Windows (PowerShell)

```powershell
irm https://raw.githubusercontent.com/Aniket-think41/skillshare-mcp/main/install.ps1 | iex
```

### Direct Binary Installation

Download the appropriate binary from the latest GitHub release:

* `skillshare-mcp-linux-amd64`
* `skillshare-mcp-macos-arm64`
* `skillshare-mcp-windows-amd64.exe`

### Verify Installation

```bash
skillshare-mcp --version
skillshare-mcp --help
```

---

# Add the MCP Server to Claude Code

```bash
claude mcp add skillshare -- skillshare-mcp
```

### Verify MCP Registration

```bash
claude mcp list
```

---

# Using Skills and Notes Without Installing

You do not need to copy a skill into `~/.claude/skills` to use it.

Instead, you can fetch the content on demand and provide it directly to your agent.

### CLI

Print the raw content without writing any files:

```bash
skillshare use <resource-id>
```

### MCP

Ask your agent to use a specific skill or note. The MCP server will call the `use_resource` tool, retrieve the content, and apply it directly within the current session.

Nothing is written to disk and nothing is copied into your organization.

Use `install` or `import` only when you want a persistent local copy.

---

# Corporate Networks & TLS Proxies

### Supported Proxies

* Zscaler
* Netskope
* Other TLS-inspection corporate proxies

Starting with:

* CLI **v1.0.2**
* MCP Server **v1.0.1**

Both tools use your operating system's certificate store for TLS validation, allowing them to work automatically in environments where HTTPS traffic is re-signed by a corporate root certificate.

No additional configuration is required.

### If You Still Encounter Certificate Errors

#### Option 1: Specify Your Corporate CA Bundle

```bash
export SSL_CERT_FILE=/path/to/corporate-root.pem
export REQUESTS_CA_BUNDLE=/path/to/corporate-root.pem
```

For the MCP server, add these environment variables to the `env` section of your Claude Code MCP configuration.

#### Option 2: Install System Certificate Support

For source or pip installations:

```bash
pip install pip-system-certs
```

Install it into the same Python environment as SkillShare.

### Force Legacy Certificate Behavior

To disable system trust stores and use the previous `certifi`-only behavior:

```bash
export SKILLSHARE_SYSTEM_TRUST=0
```

---

# Install From Source

**Requirements:** Python 3.10 or newer.

## CLI

```bash
pip install "git+https://github.com/Aniket-think41/skillshare-cli.git"
```

## MCP Server

```bash
pip install "git+https://github.com/Aniket-think41/skillshare-mcp.git"
```

---

# Quick Start

```bash
# Install CLI
curl -fsSL https://raw.githubusercontent.com/Aniket-think41/skillshare-cli/main/install.sh | bash

# Login
skillshare login

# Install MCP
curl -fsSL https://raw.githubusercontent.com/Aniket-think41/skillshare-mcp/main/install.sh | bash

# Register MCP with Claude Code
claude mcp add skillshare -- skillshare-mcp

# Verify
claude mcp list
```

