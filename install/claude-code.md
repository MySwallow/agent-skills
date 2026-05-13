# Installing superpowers-lite on Claude Code

You are an AI coding assistant running inside **Claude Code**. The user has
asked you to install superpowers-lite — 7 coding-methodology skills.

**Follow these steps strictly.** Do not skip steps. Do not improvise commands.
If any step fails, STOP and report the exact failure to the user.

---

## Step 1: Ask the user which language

Two skill sets ship in this repository:

- `skills/` — **Chinese (default)**
- `skills-en/` — English

Ask the user which one. If they don't specify, use `skills/`.
Let `SKILL_SRC` be the chosen directory name.

---

## Step 2: Download the repository

Run **exactly**:

```bash
curl -fsSL https://github.com/MySwallow/superpowers-lite/archive/refs/heads/main.tar.gz \
  | tar xz -C /tmp/
```

If `curl` or `tar` is missing, fall back to:

```bash
git clone --depth=1 https://github.com/MySwallow/superpowers-lite.git /tmp/superpowers-lite-main
```

Verify `/tmp/superpowers-lite-main/skills/` contains **7 directories**. If
not, STOP and report.

---

## Step 3: Install

Remove any previous superpowers-lite skill folders, then copy fresh. This
preserves any other personal skills the user has added under `~/.claude/skills/`.

```bash
mkdir -p ~/.claude/skills
for skill_dir in /tmp/superpowers-lite-main/$SKILL_SRC/*/; do
  rm -rf ~/.claude/skills/$(basename "$skill_dir")
done
cp -R /tmp/superpowers-lite-main/$SKILL_SRC/* ~/.claude/skills/
```

(Substitute `$SKILL_SRC` with the value from Step 1.)

---

## Step 4: Verify

List `~/.claude/skills/` and confirm **7 skill folders** are present, each
containing a `SKILL.md`. Print the folder names to the user.

If the count is not 7, STOP and report.

---

## Step 5: Report to the user

Tell the user, in plain language:

1. Language version installed (`skills` or `skills-en`)
2. Install path: `~/.claude/skills/`
3. **Restart Claude Code session** to load the new skills
4. Example trigger to confirm: ask "let's brainstorm a new feature" — the
   `brainstorming` skill should activate.

---

## Step 6: Cleanup

```bash
rm -rf /tmp/superpowers-lite-main
```

Skip cleanup if Step 3 or 4 failed — leave the temp dir for inspection.
