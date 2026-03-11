# Raptor2 Releases

Public releases for the Raptor2 CLI tool — local-first infrastructure management.

## Installation

Download the latest release for your platform:

### Linux
```bash
# AMD64
curl -L -o raptor2 https://github.com/Facets-cloud/raptor2-releases/releases/latest/download/raptor2-linux-amd64
chmod +x raptor2
mv raptor2 ~/.local/bin/

# ARM64
curl -L -o raptor2 https://github.com/Facets-cloud/raptor2-releases/releases/latest/download/raptor2-linux-arm64
chmod +x raptor2
mv raptor2 ~/.local/bin/
```

### macOS
```bash
# Intel
curl -L -o raptor2 https://github.com/Facets-cloud/raptor2-releases/releases/latest/download/raptor2-darwin-amd64
chmod +x raptor2
mv raptor2 ~/.local/bin/

# Apple Silicon
curl -L -o raptor2 https://github.com/Facets-cloud/raptor2-releases/releases/latest/download/raptor2-darwin-arm64
chmod +x raptor2
mv raptor2 ~/.local/bin/
```

> **Note:** Make sure `~/.local/bin` is in your `PATH`. Add `export PATH="$HOME/.local/bin:$PATH"` to your shell profile if needed.

## Getting Started

### Prerequisites

- **Cloud CLI** authenticated (`aws configure` / `gcloud auth` / `az login`)
- **Terraform** installed (>= 1.5)

### Quick Start

```bash
# Scaffold a new project
raptor2 init --name my-app

# Add a module source
raptor2 set module-source --name facets --type git \
  --url https://github.com/Facets-cloud/facets-v3-modules.git \
  --path modules --ref main

# Create an environment
raptor2 create environment -p my-app -e dev

# Add resources
raptor2 apply resource cloud_account/aws_provider/1.0 -p my-app -n default
raptor2 apply resource network/aws_network/1.0 -p my-app -n main-vpc \
  --input cloud_account=cloud_account/default

# Preview deployment
raptor2 apply environment -p my-app -e dev --plan

# Deploy
raptor2 apply environment -p my-app -e dev
```

### Usage

```bash
# View all available commands
raptor2 --help

# Check version
raptor2 --version

# List projects
raptor2 get projects

# List available modules
raptor2 get modules

# Describe a module (inputs, outputs, spec schema)
raptor2 describe module postgres/aws_rds/1.0

# List resources in a project
raptor2 get resources -p my-app
```

### Authentication (Enterprise)

For enterprise users with a Facets Control Plane:

```bash
# Login (opens browser for token)
raptor2 login

# Check current auth context
raptor2 whoami
```
