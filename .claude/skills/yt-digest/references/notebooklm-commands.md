# NotebookLM CLI Reference (for yt-digest skill)

## Prerequisites

Install: `pip install "notebooklm-py[browser]"` then `playwright install chromium`
Auth: `notebooklm login`

## Commands Used by This Skill

### Check auth status
```
notebooklm status
```
Returns current auth state and active notebook context. Use `--json` for machine-readable output.

### Create a notebook
```
notebooklm create "<title>"
```
Creates a new notebook. Returns the notebook ID.

### Set active notebook
```
notebooklm use <notebook_id>
```
Sets the active notebook for subsequent commands. Supports partial ID matching.

### Add a YouTube source
```
notebooklm source add "<youtube_url>"
```
Adds a YouTube video as a source to the active notebook. The source will be processed asynchronously.

### List sources
```
notebooklm source list
```
Shows all sources in the active notebook with their processing status.

### Query the notebook
```
notebooklm ask "<question>"
```
Ask a question about the notebook sources. Options:
- `--json` — returns structured response with references
- `--save-as-note` — saves response as a note in the notebook

### Delete a notebook
```
notebooklm delete -n <notebook_id> -y
```
Permanently removes a notebook and all its sources. Use `-n` to specify the notebook ID (supports partial IDs) and `-y` to skip confirmation.

### List all notebooks
```
notebooklm list
```
Shows all notebooks with their IDs.

## JSON Output
Most commands support `--json` for structured output.
