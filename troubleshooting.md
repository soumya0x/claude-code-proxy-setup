# Troubleshooting

Real errors. Real fixes.

---

## `401 Unauthorized`

**Cause:** Wrong key, or `settings.json` not being picked up.

**Fix:**
```bash
cat ~/.claude/settings.json   # confirm file exists and key is correct
echo $ANTHROPIC_API_KEY       # if this prints something, it's overriding your config
unset ANTHROPIC_API_KEY       # clear it for current session
```

---

## Claude Code using my real Anthropic key instead of proxy

**Cause:** `ANTHROPIC_API_KEY` is exported in `~/.zshrc` or `~/.bash_profile`.

**Fix:**
```bash
grep "ANTHROPIC_API_KEY" ~/.zshrc
```

If found — remove or comment it out. Restart terminal. Re-test.

---

## `settings.json` is being ignored

**Cause:** File is in the wrong location or malformed JSON.

**Fix:**
```bash
# Confirm location
ls ~/.claude/settings.json

# Validate JSON
cat ~/.claude/settings.json | python3 -m json.tool
```

Fix any JSON syntax errors (trailing commas, missing quotes, etc.)

---

## Plugin install fails

**Cause:** npm permissions or Node version mismatch.

**Fix:**
```bash
node -v       # should be 18+
npm -v

# If permission error:
sudo npm install -g @anthropic-ai/claude-code
```

---

## Claude Desktop stopped working after this setup

**Cause:** You may have modified the wrong config file.

Claude Desktop uses:
```
~/Library/Application Support/Claude/claude_desktop_config.json
```

Claude Code uses:
```
~/.claude/settings.json
```

They are separate. Do not mix them.

---

## Still broken?

Open an issue with:
1. Your OS + version
2. Output of `cat ~/.claude/settings.json`
3. Output of `echo $ANTHROPIC_API_KEY`
4. The exact error message
