# yt-digest-skill

A Claude Code skill that digests YouTube videos into summaries and key takeaways using Google NotebookLM. Get the essential content without watching.

## What It Does

Give it a YouTube URL, and it will:
1. Process the video through NotebookLM
2. Display a structured summary and key takeaways
3. Answer follow-up questions about specific sections
4. Optionally clean up the NotebookLM notebook when done

## Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code)
- [notebooklm-py](https://github.com/teng-lin/notebooklm-py):
  ```bash
  pip install "notebooklm-py[browser]"
  playwright install chromium
  notebooklm login
  ```

## Installation

### User-level (available everywhere)

```bash
# Clone the repo
git clone https://github.com/IvanKusturic/yt-digest-skill.git

# Copy the skill to your user-level skills directory
mkdir -p ~/.claude/skills
cp -r yt-digest-skill/.claude/skills/yt-digest ~/.claude/skills/yt-digest
```

### Project-level (single project only)

```bash
# From your project root
git clone https://github.com/IvanKusturic/yt-digest-skill.git /tmp/yt-digest-skill
mkdir -p .claude/skills
cp -r /tmp/yt-digest-skill/.claude/skills/yt-digest .claude/skills/yt-digest
rm -rf /tmp/yt-digest-skill
```

## Usage

```
/yt-digest https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

Or use natural language:
- "Summarize this video: https://..."
- "What's this YouTube video about? https://..."
- "Digest this video for me: https://..."

## License

Apache 2.0
