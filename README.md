# Handoff

A Codex plugin that writes a compact, verifiable context handoff for a new AI session. It records the task goal, decisions, checks, Git anchor, open questions, and next steps while omitting secrets and personal data.

## Install from GitHub

```bash
codex plugin marketplace add l3263254135-dotcom/handoff
codex plugin add handoff@handoff
```

Start a new Codex task after installation and ask it to save a handoff for the current task. The skill writes a Markdown file under `_docs/handoff/` in the current working directory.

## Local development and publishing

The editable personal source is `~/plugins/handoff/`. The Codex cache is an installation artifact. After changing the source, run the shared publisher in the sibling `research-knowledge-onramp` checkout:

```bash
../research-knowledge-onramp/scripts/publish-project.sh handoff --dry-run
../research-knowledge-onramp/scripts/publish-project.sh handoff --message "docs: clarify handoff guidance"
```

The publisher validates the plugin, checks for private paths and credentials, syncs this repository, commits and pushes `main`, then reinstalls the personal plugin. For GitHub installations, refresh the Git marketplace with `codex plugin marketplace upgrade handoff` and reinstall the plugin to pick up updates.

Licensed under [MIT](LICENSE).
