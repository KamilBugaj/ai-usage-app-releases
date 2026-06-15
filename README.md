# KB.AI.Usage

A system-tray app that tracks your AI tool usage locally. No telemetry, no cloud.
Monitors tokens, costs, and rate limits for: Anthropic API, Claude.ai, OpenAI API, ChatGPT, GitHub Copilot.

![AI Usage app window showing Claude.ai and usage tiles](./docs/screenshots/app-preview.png)

## Download

Go to [Releases](../../releases/latest) and grab the file for your platform:

| Platform      | File                                | Notes                  |
|---------------|-------------------------------------|------------------------|
| Windows       | `KB.AI.Usage-Setup.exe`             | Installer              |
| Windows       | `KB.AI.Usage-win-x64.zip`           | Portable (zip)         |
| macOS (M1+)   | `KB.AI.Usage-osx-arm64.zip`         | Apple Silicon          |
| macOS (Intel) | `KB.AI.Usage-osx-x64.zip`           | Intel                  |
| Linux         | `KB.AI.Usage-linux-x64.tar.gz`      | x64                    |

## Installation

### Windows

**Installer**: run `KB.AI.Usage-Setup.exe`.

SmartScreen may block it (the app is not code-signed):
click **More info** → **Run anyway**.

**Portable**: unzip and run `AiUsage.App.exe`.

### macOS

Unzip the archive. Before first launch, remove the quarantine flag (Gatekeeper
blocks unsigned apps):

```bash
xattr -dr com.apple.quarantine KB.AI.Usage.app
```

Alternatively: right-click the `.app` → Open → Open.

### Linux

```bash
tar xzf KB.AI.Usage-linux-x64.tar.gz
chmod +x AiUsage.App
./AiUsage.App
```

Requires a tray library: `libappindicator3-1`
(Ubuntu/Debian: `sudo apt install libappindicator3-1`).

## First launch

The app appears in the system tray. Click the icon → Open to see the usage tiles.

Edit the config file and fill in your API keys / session tokens:
- **Windows**: `%APPDATA%\AiUsage\config.json`
- **macOS/Linux**: `~/.config/AiUsage/config.json`

See [config.example.json](https://github.com/KamilBugaj/ai-usage-app-releases/blob/main/config.example.json)
for the full list of fields.

### Where to find your keys and tokens

**Anthropic API** (`anthropicApiKey`):
https://console.anthropic.com/account/keys

**OpenAI API** (`openAiApiKey`):
https://platform.openai.com/api-keys — requires an owner/admin key.

**Claude.ai** (`sessionKey`, `organizationId`):
1. Open claude.ai in your browser and log in.
2. DevTools (F12) → Application → Cookies → find `sessionKey`.
3. DevTools → Network → any request to api.claude.ai → look for the `X-Org-Id` header
   or an `/organizations/<id>/` segment in the URL.

**ChatGPT** (`sessionToken`):
1. Open chatgpt.com and log in.
2. DevTools → Application → Cookies → `__Secure-next-auth.session-token`.

**GitHub Copilot**: auto-detected from VS Code logs — no configuration needed.

## Reporting issues

Open an [issue](../../issues) in this repo.
