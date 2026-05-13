# Installing superpowers-lite

Pick the install URL for **your platform** and paste it into your AI:

| Platform | Tell your AI: "Please install superpowers-lite. Follow:" |
|---|---|
| Claude Code | <https://raw.githubusercontent.com/MySwallow/superpowers-lite/main/install/claude-code.md> |
| opencode | <https://raw.githubusercontent.com/MySwallow/superpowers-lite/main/install/opencode.md> |
| Codex CLI | <https://raw.githubusercontent.com/MySwallow/superpowers-lite/main/install/codex.md> |
| Gemini CLI | <https://raw.githubusercontent.com/MySwallow/superpowers-lite/main/install/gemini-cli.md> |
| Cursor / Windsurf / Cline | <https://raw.githubusercontent.com/MySwallow/superpowers-lite/main/install/cursor.md> |

Each per-platform installer is self-contained: it tells the AI to ask
about language preference, download the repo, install to that platform's
correct global directory, verify, and report back.

**Re-running an installer upgrades cleanly** — it removes the 7 known
skill folders before copying fresh, so stale files from older versions
don't pile up. Any other skills you've added by hand to the same directory
are preserved.

---

## Native one-liner alternatives

For platforms with built-in plugin systems, you can skip the AI installer
and use the native command directly.

### Gemini CLI

```bash
gemini extensions install https://github.com/MySwallow/superpowers-lite
```

---

## Manual install (no AI, no plugin manager)

If you'd rather install everything by hand:

### Claude Code

```bash
git clone https://github.com/MySwallow/superpowers-lite.git
cd superpowers-lite
./scripts/install-claude-code.sh           # Chinese (default)
./scripts/install-claude-code.sh --lang en # English
```

### Any other platform

1. Clone the repo: `git clone https://github.com/MySwallow/superpowers-lite.git`
2. Copy `skills/` (or `skills-en/`) into your platform's skill directory.
   Common locations:
   - opencode: `~/.config/opencode/skills/`
   - Codex: `~/.codex/skills/`
   - Cursor / Windsurf / Cline: copy `templates/cursor-rules.md` into your
     project's rules directory
3. Verify by asking the AI to brainstorm or debug something — it should
   announce the relevant skill.

---

## Troubleshooting

If install fails, file an issue with the platform, the command run, and
the error output: <https://github.com/MySwallow/superpowers-lite/issues>
