# macOS Setup (Apple Silicon)

> Tested on: MacBook Air M5 · macOS Tahoe · zsh · Python 3.14

---

## Step 1 — Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

Verify:

```bash
claude --version
```

---

## Step 2 — Get a proxy key

Go to [cc.freemodel.dev](https://cc.freemodel.dev) and grab your API key.

---

## Step 3 — Write the config

```bash
mkdir -p ~/.claude
nano ~/.claude/settings.json
```

Paste:

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://cc.freemodel.dev/api",
    "ANTHROPIC_API_KEY": "YOUR_PROXY_KEY_HERE"
  }
}
```

Save: `Ctrl+O` → Enter → `Ctrl+X`

---

## Step 4 — Handle the Claude Desktop conflict

Claude Desktop stores its own API key. On Mac, check:

```bash
echo $ANTHROPIC_API_KEY
cat ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

If `ANTHROPIC_API_KEY` is set globally in your env, it overrides `settings.json`.

Fix: Do not export `ANTHROPIC_API_KEY` in `~/.zshrc`.  
Let `settings.json` handle it exclusively for Claude Code.

---

## Step 5 — Test

```bash
claude "respond with: proxy is working"
```

Done.
