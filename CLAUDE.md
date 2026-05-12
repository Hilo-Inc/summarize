# Claude Instructions — Video Summarization Workspace

## CLI Commands

The CLI binary is `summarize` (also aliased as `summarizer`). During development, run via `pnpm s <args>` or `tsx src/cli.ts <args>`.

### Basic usage

```bash
# Summarize a YouTube video with default settings
summarize https://www.youtube.com/watch?v=VIDEO_ID

# Summarize a web page
summarize https://example.com/article

# Summarize stdin (text or binary)
cat transcript.txt | summarize -

# Summarize a local file
summarize ./path/to/file.pdf
```

### Saving to the notes folder

The `--output` / `-o` flag writes `<outputDir>/<channel-slug>/<videoId>.{json,md}` — channel is auto-extracted from YouTube HTML. If no channel is known, files land in `<outputDir>/unknown/`.

```bash
# Save to notes/videos/<channel>/<videoId>.{json,md}
summarize https://www.youtube.com/watch?v=VIDEO_ID -o notes/videos

# Long-form summary saved to notes
summarize https://www.youtube.com/watch?v=VIDEO_ID --length xxl -o notes/videos
```

### Length presets

| Flag | Meaning |
|------|---------|
| `--length s` or `--length short` | Short summary |
| `--length m` or `--length medium` | Medium |
| `--length l` or `--length long` | Long |
| `--length xl` | Extra long (default) |
| `--length xxl` | Maximum |
| `--length 20k` | ~20,000 character cap |

### Model selection

```bash
# Use Claude Sonnet 4.6 via Anthropic
summarize <url> --model anthropic/claude-sonnet-4-6 -o notes/videos

# Use OpenAI
summarize <url> --model openai/gpt-5-mini -o notes/videos

# Force Claude CLI (agent mode, no API key needed if Claude Code is installed)
summarize <url> --cli claude -o notes/videos

# Let it auto-pick based on available API keys
summarize <url> --model auto -o notes/videos
```

### Transcript source control (YouTube)

```bash
# Try captions first, fall back to yt-dlp + whisper (default)
summarize <url> --youtube auto

# Force yt-dlp audio download + whisper transcription
summarize <url> --youtube yt-dlp

# Only use web captions; skip auto-generated
summarize <url> --youtube no-auto

# Use Apify transcript API (requires APIFY_TOKEN)
summarize <url> --youtube apify
```

### Useful flags

| Flag | Purpose |
|------|---------|
| `-o, --output <dir>` | Save `.json` + `.md` into `<dir>/<channel>/<videoId>.*` |
| `--json` | Emit full JSON payload (prompt, metrics, extraction) to stdout |
| `--extract` | Print raw extracted text/transcript only, skip LLM |
| `--timestamps` | Include timestamps in transcripts |
| `--language en` | Force output language (default: auto-match source) |
| `--timeout 5m` | Content fetch + LLM timeout (`30s`, `2m`, `5000ms`) |
| `--verbose` | Print progress to stderr |
| `--metrics detailed` | Show token counts, costs, timing breakdown |
| `--no-cache` | Bypass LLM summary cache |
| `--slides` | Extract slide screenshots from videos (requires ffmpeg) |
| `--prompt "..."` | Override the summary instruction prefix |
| `--prompt-file prompt.md` | Read prompt override from a file |

### Slides mode

```bash
# Extract slides + summary
summarize <youtube-url> --slides

# Slides with OCR (requires tesseract)
summarize <youtube-url> --slides --slides-ocr

# Slides-only mode, save images to ./slides/
summarize slides <youtube-url>
```

### Cache & maintenance

```bash
summarize --cache-stats     # Show cache size/hit stats
summarize --clear-cache     # Delete cache DB and exit
```

### Typical summarization workflow for this project

```bash
# 1. Summarize and save
summarize https://www.youtube.com/watch?v=VIDEO_ID \
  --length xxl \
  --model anthropic/claude-sonnet-4-6 \
  -o notes/videos

# 2. Output lands at:
#    notes/videos/<channel-slug>/<videoId>.json
#    notes/videos/<channel-slug>/<videoId>.md

# 3. Update notes/README.md index with the new entry
```

## Every Time a Video Is Summarized

When the user provides a transcript or video URL to summarize, follow these steps:

### 1. Produce the Summary

Format the summary in clean GitHub-flavored markdown:

- **Title** as an H2 heading
- **Sections** as H3 headings derived from the content's natural structure
- **Key data points** in tables where applicable
- **Important quotes** in blockquotes
- Use bullet points for lists; avoid walls of prose
- No fluff, no filler — only the most important points

### 2. Save the Video Summary

Save to `notes/videos/<channel-slug>/<video-id>.md` using this template:

```markdown
---
title: <video title>
channel: <YouTube channel name>
channel_url: <channel URL if known>
source: <video URL or filename>
date: <YYYY-MM-DD>
topic: <one-line topic tag>
---

## <Title>

<formatted summary content>
```

- Use the YouTube channel name as the folder slug (lowercase, hyphens, e.g., `optionsplay`, `max-fisher`, `kurzgesagt`)
- Use the YouTube video ID as the filename (e.g., `kZbMABuzn9U.md`)
- For local transcript files with no known channel, use `notes/videos/unknown/<filename-stem>.md`
- Create the channel folder if it doesn't exist

### 3. Save the Chat Discussion

If the user discusses the video content in depth (follow-up questions, analysis, debate), save the conversation to `notes/chats/<channel-slug>/<video-id>-chat.md` using this template:

```markdown
---
video: <notes/videos/filename.md>
date: <YYYY-MM-DD>
---

## Discussion: <Title>

### <Topic of exchange>

**User:** <question or point>

**Claude:** <response summary>

---
```

Only save chat entries that contain substantive analysis or insight beyond the summary itself.

### 4. Update the Index

Maintain `notes/README.md` as a running index of all saved summaries and chats:

```markdown
## Video Summaries

| Date | Title | File | Topic |
|------|-------|------|-------|
| YYYY-MM-DD | Title | [link](videos/file.md) | topic |

## Chat Discussions

| Date | Video | File |
|------|-------|------|
| YYYY-MM-DD | Title | [link](chats/file.md) |
```

---

## Folder Structure

```
notes/
  README.md                        ← index of all summaries and chats
  videos/
    <channel-slug>/                ← one folder per YouTube channel
      <video-id>.md                ← one file per video
    unknown/                       ← for transcripts with no known channel
  chats/
    <channel-slug>/                ← mirrors videos/ structure
      <video-id>-chat.md
summaries/                         ← raw JSON output from the summarize CLI (gitignored)
```

---

## Summary Quality Standards

- Lead with **what matters most**, not what comes first in the video
- If the video is a product demo or tutorial, focus on the **workflow and key capabilities**, not the sales pitch
- If the video is analysis or commentary, preserve the **argument structure** and key evidence
- Flag **sponsored segments** — summarize them briefly but mark clearly
- For transcripts with `(speaking in foreign language)` markers, note that portions were not transcribed
