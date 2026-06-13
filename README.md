<div align="center">

# ⚡ claude-code-proxy-setup

**Run Claude Code at a fraction of the cost — through a third-party proxy.**  
Zero friction. Full power. No official API bills.

![Platform](https://img.shields.io/badge/platform-macOS%20%7C%20Linux%20%7C%20Windows-blue?style=flat-square)
![Tested](https://img.shields.io/badge/tested%20on-Apple%20Silicon%20M5-black?style=flat-square)
![Python](https://img.shields.io/badge/python-3.14-yellow?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square)

</div>

---

## 🧠 What is this?

Claude Code is powerful. But the Anthropic API costs add up fast.

This repo gives you a **drop-in config** to route Claude Code through [`cc.freemodel.dev`](https://cc.freemodel.dev) — a compatible third-party proxy — so you keep the full Claude Code experience without the full Claude API bill.

> Built and tested on MacBook Air M5 · macOS Tahoe · Python 3.14 · zsh

---

## ✅ Prerequisites

Before you start:

- [ ] Node.js `18+` → `node -v`
- [ ] Claude Code → `npm install -g @anthropic-ai/claude-code`
- [ ] A proxy API key from [cc.freemodel.dev](https://cc.freemodel.dev)

---

## 🚀 Setup (3 steps)

### Step 1 — Get your proxy key

Sign up at [cc.freemodel.dev](https://cc.freemodel.dev) and copy your API key.

---

### Step 2 — Apply the config

```bash
mkdir -p ~/.claude
curl -o ~/.claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-code-proxy-setup/main/config/settings.json
```

Or manually create `~/.claude/settings.json`:

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://cc.freemodel.dev/api",
    "ANTHROPIC_API_KEY": "YOUR_PROXY_KEY_HERE"
  }
}
```

Replace `YOUR_PROXY_KEY_HERE` with your actual proxy key.

---

### Step 3 — Verify

```bash
claude "say: proxy is working"
```

If you get a response — you're live. 🟢

---

## ⚠️ Critical: Claude Desktop conflict

If you have Claude Desktop installed, it may have its own `ANTHROPIC_API_KEY` in your shell env — which silently overrides `settings.json`.

**Check for it:**

```bash
echo $ANTHROPIC_API_KEY
```

**If something prints — unset it:**

```bash
unset ANTHROPIC_API_KEY
```

**Don't add `ANTHROPIC_API_KEY` to `~/.zshrc`.** Let `settings.json` handle it for Claude Code only. Claude Desktop handles its own config separately.

---

## 📁 Repo Structure

```
claude-code-proxy-setup/
├── 📄 README.md
├── config/
│   └── settings.json        # drop-in config template
├── setup/
│   ├── mac.md               # full macOS M-series walkthrough
│   └── windows.md           # community contribution
└── troubleshooting.md       # real errors, real fixes
```

---

## 🐛 Common Errors

| Error | Cause | Fix |
|---|---|---|
| `401 Unauthorized` | Wrong key or settings.json ignored | See [troubleshooting.md](./troubleshooting.md) |
| Using real Anthropic key | `ANTHROPIC_API_KEY` exported in shell | `unset ANTHROPIC_API_KEY` |
| Settings ignored | Malformed JSON | `cat ~/.claude/settings.json \| python3 -m json.tool` |
| Plugin install fails | Node version / permissions | `node -v` should be 18+ |

Full details → [`troubleshooting.md`](./troubleshooting.md)

---

## 🤝 Contributing

Tested on a different OS or setup? Open a PR and add your notes to `/setup/`.  
Especially needed: **Windows**, **Linux**, **older macOS**.

---

## 📄 License

MIT — use it, fork it, ship it.

---

<div align="center">

**If this saved you money, drop a ⭐ — it helps others find it.**

</div>
