# YouTube Description Downloader
<p align="center">
  <a href="https://github.com/Lucasyao1985/youtube-desc-downloader">GitHub</a> | <a href="SKILL.md">SKILL.md</a>
</p>
<p align="center">
  <a href="https://github.com/Lucasyao1985/youtube-desc-downloader"><img alt="Release version" src="https://img.shields.io/github/v/release/Lucasyao1985/youtube-desc-downloader?color=2da44e&label=Latest&style=for-the-badge" /></a>
  <a href="https://github.com/Lucasyao1985/youtube-desc-downloader/commits"><img alt="Last commit" src="https://img.shields.io/github/last-commit/Lucasyao1985/youtube-desc-downloader?color=0969da&label=Last%20commit&style=for-the-badge" /></a>
  <a href="README.zh-CN.md"><img alt="中文" src="https://img.shields.io/badge/中文-da3633?style=for-the-badge" /></a>
  <a href="LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-2da44e?style=for-the-badge" /></a>
</p>

---

**YouTube Description Downloader is a [Claude Code](https://claude.ai) skill that downloads YouTube video descriptions as local UTF-8 text files.** Supports single videos and batch channel downloads.

<table>
<tr><td><b>Single video download</b></td><td>Download the full description of any YouTube video as a UTF-8 text file.</td></tr>
<tr><td><b>Batch channel download</b></td><td>Download the latest N episode descriptions from any channel at once.</td></tr>
<tr><td><b>Rich output</b></td><td>Each file contains video title, URL, publish date, and full description text.</td></tr>
<tr><td><b>yt-dlp powered</b></td><td>Uses yt-dlp under the hood for reliable extraction.</td></tr>
</table>

---

## Quick Install

```bash
git clone https://github.com/Lucasyao1985/youtube-desc-downloader.git
```

Place the folder in your Claude Code skills directory:
- **Windows:** `C:\Users\<you>\.claude\skills\`
- **macOS/Linux:** `~/.claude/skills/`

### Dependencies

```bash
pip install yt-dlp
```

## Usage

Share a YouTube URL with Claude:

```
Download the description of this video: https://www.youtube.com/watch?v=xxx
```

Or for batch channel download:

```
Download descriptions of the latest 10 videos from this channel: https://www.youtube.com/@channel
```

The skill outputs individual text files with:
- **Video title** and **URL**
- **Publish date**
- **Full description text** (verbatim)

## How It Works

```
YouTube URL → [yt-dlp] → description text → UTF-8 file
```

The skill uses yt-dlp's `--write-info-json` and `--write-description` flags to extract metadata and description, then formats them into a clean text file.

## Project Structure

```
youtube-desc-downloader/
├── SKILL.md                 # Skill definition
├── README.md                # This file (English)
├── README.zh-CN.md          # Chinese documentation
├── scripts/
│   └── download-desc.sh     # Core download script
└── references/
```

## License

MIT — see [LICENSE](LICENSE).

Built with [opencode](https://github.com/anomalyco/opencode).