# Claude Instructions — Video Summarization Workspace

## Automated CLI Output

When summaries are generated via the CLI with `--output <dir>`, they are automatically written to `<dir>/<channel-slug>/<video-id>.{json,md}`. The channel name is extracted from the YouTube `ytInitialPlayerResponse.videoDetails.author` field; when no channel is known, files land in `<dir>/unknown/`.

Run:
```
summarize <youtube-url> --output notes/videos
```

This produces:
- `notes/videos/<channel-slug>/<videoId>.json` (raw payload)
- `notes/videos/<channel-slug>/<videoId>.md` (markdown with frontmatter + summary)

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
