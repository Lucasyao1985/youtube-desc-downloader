# YouTube 简介下载器
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

**YouTube 简介下载器是一个 [Claude Code](https://claude.ai) 技能，将 YouTube 视频的完整简介下载为本地 UTF-8 文本文件。**

## 功能特点

- 下载单个 YouTube 视频的完整简介
- 批量下载某个频道最近 N 期视频的简介
- 输出为 UTF-8 文本文件，包含视频标题、URL 和完整简介正文
- 需要 yt-dlp 和 Python 3

---

## 快速安装

```bash
git clone https://github.com/Lucasyao1985/youtube-desc-downloader.git
```

将文件夹放入 Claude Code skills 目录：
- **Windows:** `C:\Users\<你的用户名>\.claude\skills\`
- **macOS/Linux:** `~/.claude/skills/`

### 依赖安装

```bash
pip install yt-dlp
```

## 使用示例

向 Claude 发送以下指令：

```
请下载这个视频的简介：https://www.youtube.com/watch?v=xxx
```

或批量下载：

```
把这个频道最新的视频简介都下载下来
```

## 文件结构

```
youtube-desc-downloader/
├── SKILL.md           # 技能定义文件
├── README.md          # 英文文档
├── README.zh-CN.md    # 中文文档
├── scripts/           # 执行脚本
└── references/        # 参考资料
```

## 许可证

MIT — 见 [LICENSE](LICENSE)。

由 [opencode](https://github.com/anomalyco/opencode) 构建。