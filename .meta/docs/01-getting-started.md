# Installation & Setup

Get ClaudeSpace running on your machine in under 5 minutes.

---

## System Requirements

Before installing, ensure your system meets these requirements:

| Requirement | Minimum | Recommended |
|-------------|---------|-------------|
| **Node.js** | ≥18.19.9 | Latest LTS |
| **RAM** | 4GB | 8GB |
| **Disk Space** | 500MB | 1GB |
| **Platform** | macOS, Windows, Linux | Any |

**Check your Node.js version:**
```bash
node --version
```

If you need to install or update Node.js, download it from [nodejs.org](https://nodejs.org/).

---

## Installation

### Option 1: Quick Install (Recommended)

Get ClaudeSpace running in 3 commands:

```bash
# Clone the repository
git clone https://github.com/FilipeBorges1993/ClaudeSpaceElectron.git
cd ClaudeSpaceElectron

# Install dependencies
npm install

# Run ClaudeSpace
npm run dev
```

**Expected output:**
```
  VITE v5.x.x  ready in xxx ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose

  Electron app started
```

✅ **Success:** ClaudeSpace opens automatically

---

### Option 2: Build from Source

For production builds or custom installations:

```bash
# Clone and install (same as Option 1)
git clone https://github.com/FilipeBorges1993/ClaudeSpaceElectron.git
cd ClaudeSpaceElectron
npm install

# Build for your platform
npm run build:mac      # macOS (Intel + ARM)
npm run build:win      # Windows (x64 + ARM)
npm run build:linux    # Linux AppImage
```

**Build output location:**
- macOS: `dist/mac/` (.dmg file)
- Windows: `dist/win/` (.exe installer)
- Linux: `dist/linux/` (.AppImage)

---

## First Launch

When you launch ClaudeSpace for the first time:

### 1. Welcome Screen

The app opens with a workspace selection dialog.

[Screenshot: Workspace selection dialog showing "Select Workspace Folder" button]

### 2. Select Workspace

A **workspace** is a folder where ClaudeSpace stores your projects.

**Choose or create a folder:**
```bash
# Example locations
~/Documents/ClaudeSpace-Workspace     # macOS/Linux
C:\Users\YourName\ClaudeSpace         # Windows
```

**Recommendation:** Create a dedicated folder for your agents.

### 3. Main Dashboard

After selecting a workspace, you'll see the main dashboard:

[Screenshot: ClaudeSpace main dashboard with "New Project" button and empty project list]

✅ **Checkpoint:** You're ready to create projects!

---

## Verify Installation

Run these commands to ensure everything is working correctly:

### Type Checking

```bash
# Check all TypeScript files
npm run typecheck

# Check specific areas
npm run typecheck:node    # Node/Electron code
npm run typecheck:web     # Vue/Renderer code
```

**Expected output:** `✓ No errors found`

### Linting

```bash
npm run lint
```

**Expected output:** `✓ No linting errors found`

### Code Formatting

```bash
npm run format
```

**Expected output:** `✓ All files formatted`

---

## Configuration

### Claude API Setup

ClaudeSpace requires Claude API access for agent testing.

**Two authentication methods:**

#### Method 1: CLI Authentication (Recommended)

```bash
# Install Claude CLI if not already installed
npm install -g @anthropic-ai/claude-cli

# Authenticate
claude auth login
```

**Benefits:**
- No API key management
- Automatic token refresh
- Secure credential storage

#### Method 2: API Key

1. Get API key from [console.anthropic.com](https://console.anthropic.com/)
2. In ClaudeSpace: Settings → Claude Configuration → API Key
3. Paste your key and click Save

[Screenshot: Settings panel showing API key input field]

**Note:** API keys are stored securely in your system's credential manager.

---

## Next Steps

Now that ClaudeSpace is installed, you're ready to build your first agent!

**Continue to:** [Your First Agent](02-quick-start.md) (10-minute tutorial)

**Or explore:**
- [Workspace Basics](03-workspace-basics.md) - Understand project organization
- [Node Types Reference](04-node-types/README.md) - Learn about all node types
- [Canvas Workflow](05-canvas-workflow.md) - Master the visual editor

---

## Troubleshooting

### Problem: `npm install` fails

**Error message:**
```
npm ERR! code ENOENT
npm ERR! syscall open
```

**Solution:**
1. Update Node.js to ≥18.19.9
2. Clear npm cache: `npm cache clean --force`
3. Try again: `npm install`

---

### Problem: App won't start

**Symptoms:**
- Electron window doesn't open
- Console shows errors

**Solutions:**

**Check Node.js version:**
```bash
node --version  # Must be ≥18.19.9
```

**Check for port conflicts:**
```bash
# Kill process using port 5173
lsof -ti:5173 | xargs kill
```

**Clear cache and rebuild:**
```bash
rm -rf node_modules dist
npm install
npm run dev
```

**Check logs:**
- macOS/Linux: `~/.claude/logs/`
- Windows: `%APPDATA%\.claude\logs\`

---

### Problem: Workspace won't load

**Symptoms:**
- Projects don't appear
- Workspace selection fails

**Solutions:**

**Verify workspace folder:**
- Folder must exist
- You must have write permissions
- Path should not contain special characters

**Create new workspace:**
1. Create empty folder: `mkdir ~/ClaudeSpace-New`
2. In app: Switch Workspace → Select new folder

**Reset workspace:**
1. Close ClaudeSpace
2. Delete workspace cache:
   - macOS/Linux: `rm -rf ~/.config/ClaudeSpace/`
   - Windows: Delete `%APPDATA%\ClaudeSpace\`
3. Restart app

---

### Problem: Claude API authentication fails

**Symptoms:**
- Chat doesn't respond
- "Authentication failed" error

**Solutions:**

**For CLI authentication:**
```bash
# Re-authenticate
claude auth logout
claude auth login
```

**For API key:**
1. Verify key is valid at [console.anthropic.com](https://console.anthropic.com/)
2. Check for typos in Settings → Claude Configuration
3. Try regenerating API key

**Test connection:**
```bash
# If using Claude CLI
claude models list
```

---

### Problem: Build fails on specific platform

**macOS specific:**
```bash
# Install Xcode Command Line Tools
xcode-select --install

# Accept license
sudo xcodebuild -license accept
```

**Windows specific:**
```bash
# Install Windows Build Tools
npm install --global windows-build-tools
```

**Linux specific:**
```bash
# Install dependencies (Debian/Ubuntu)
sudo apt-get install build-essential libx11-dev libxkbfile-dev

# Install dependencies (Fedora)
sudo dnf install @development-tools
```

---

### Still Having Issues?

**Get help:**
- [Report a bug](https://github.com/FilipeBorges1993/ClaudeSpaceElectron/issues)
- [Join Discord](https://discord.gg/2tr2S7yw)
- Check [existing issues](https://github.com/FilipeBorges1993/ClaudeSpaceElectron/issues) for solutions

**When reporting issues, include:**
- Node.js version (`node --version`)
- npm version (`npm --version`)
- Operating system and version
- Error messages (full text or screenshots)
- Steps to reproduce

---

## Development Commands

For developers working on ClaudeSpace:

```bash
# Development mode with hot reload
npm run dev

# Type checking
npm run typecheck           # All
npm run typecheck:node      # Main process
npm run typecheck:web       # Renderer process

# Code quality
npm run lint                # ESLint check
npm run lint:fix            # Auto-fix issues
npm run format              # Prettier format

# Build for production
npm run build:mac           # macOS
npm run build:win           # Windows
npm run build:linux         # Linux
npm run build:all           # All platforms

# Clean build artifacts
rm -rf dist node_modules
npm install
```

---

## System Architecture

Understanding how ClaudeSpace works under the hood:

```
┌─────────────────────────────────────┐
│    Electron Main Process (Node.js)  │
│  - IPC handlers (80+ handlers)      │
│  - Agent session management         │
│  - File I/O operations              │
│  - Claude SDK integration           │
└──────────────┬──────────────────────┘
               │ IPC Bridge
┌──────────────▼──────────────────────┐
│     Vue 3 Renderer (Frontend)        │
│  - NodeCanvas (Vue Flow)            │
│  - ChatPage (testing UI)            │
│  - Settings & configuration         │
│  - Pinia state management           │
└─────────────────────────────────────┘
```

**Key directories:**
```
src/
├── main/           # Electron main process (Node.js)
├── preload/        # Context bridge & IPC
└── renderer/       # Vue 3 application (UI)
```

---

## License

ClaudeSpace is open source software licensed under the MIT License.

**What this means:**
- ✅ Free to use for personal and commercial projects
- ✅ Modify and distribute
- ✅ Private use
- ⚠️ No warranty or liability

See [LICENSE](../../LICENSE) for full details.

---

<div align="center">

**Ready to build your first agent?**

[Continue to Quick Start →](02-quick-start.md)

</div>
