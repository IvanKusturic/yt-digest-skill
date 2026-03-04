---
name: yt-digest
description: Digest a YouTube video into a summary and key takeaways using NotebookLM. Use when user provides a YouTube URL to summarize, or asks to digest/summarize a video.
---

# YouTube Video Digest

Digest YouTube videos into structured summaries and key takeaways using Google NotebookLM. No need to watch — get the essential content directly in the CLI.

## Trigger

- `/yt-digest <YouTube URL>`
- Natural language: "summarize this video", "digest this YouTube video", "what's this video about"

## Workflow

### Phase 1: Setup Verification

1. Check that `notebooklm-py` is installed:
   ```bash
   notebooklm status
   ```
2. If not installed, tell the user:
   ```
   Install notebooklm-py first:
     pip install "notebooklm-py[browser]"
     playwright install chromium
     notebooklm login
   ```
3. If not authenticated, run `notebooklm login` and wait for the user to complete browser auth.

### Phase 2: Process Video

1. Create a notebook for this video:
   ```bash
   notebooklm create "YT Digest: <video title or URL slug>"
   ```
2. Capture the notebook ID from the output.
3. Set it as active:
   ```bash
   notebooklm use <notebook_id>
   ```
4. Add the YouTube URL as a source:
   ```bash
   notebooklm source add "<youtube_url>"
   ```
5. Wait for the source to be processed. Check with:
   ```bash
   notebooklm source list
   ```
   Retry every 10 seconds until the source status shows as ready. If it fails after 2 minutes, inform the user.

### Phase 3: Generate and Display Digest

1. Query for the summary:
   ```bash
   notebooklm ask "Provide a comprehensive summary of this video in 2-3 paragraphs. Cover the main topic, key arguments, and conclusions."
   ```
2. Query for key takeaways:
   ```bash
   notebooklm ask "List the key takeaways from this video, grouped by topic. Use bullet points. Be specific and actionable."
   ```
3. Display the results in this format:

```
# <Video Title>

**Source:** <YouTube URL>

## Summary

<summary from NotebookLM>

## Key Takeaways

<key takeaways from NotebookLM, grouped by topic>
```

### Phase 4: Follow-Up

After displaying the digest, tell the user:

> "You can ask me for more details about any section — I'll query NotebookLM for deeper information. When you're done, let me know and I'll offer to clean up the notebook."

When the user asks about a specific topic or section:
```bash
notebooklm ask "<user's specific question>"
```

Display the response directly in the conversation.

### Phase 5: Cleanup

When the user indicates they're done (or explicitly asks to clean up), ask:

> "Would you like me to delete the NotebookLM notebook created for this video?"

- If **yes**: run `notebooklm delete <notebook_id>` and confirm deletion.
- If **no**: inform the user the notebook remains available in their NotebookLM account and provide the notebook ID for future reference.

## Important Notes

- Always use the CLI commands documented in `references/notebooklm-commands.md`
- Do NOT save files — all output stays in the CLI conversation
- If a NotebookLM command fails, show the error to the user and suggest next steps
- Keep the notebook active throughout the conversation for follow-up queries
