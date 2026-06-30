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

**YouTube 简介下载器是一个 [Claude Code](https://claude.ai) 技能，将 YouTube 视频的完整简介下载为本地 UTF-8 文本文件。** 支持单个视频和批量频道下载。

<table>
<tr><td><b>单个视频下载</b></td><td>将任意 YouTube 视频的完整简介保存为 UTF-8 文本文件。</td></tr>
<tr><td><b>批量频道下载</b></td><td>一键下载某个频道最近 N 期视频的简介。</td></tr>
<tr><td><b>丰富输出</b></td><td>每个文件包含视频标题、URL、发布日期和完整简介正文。</td></tr>
<tr><td><b>基于 yt-dlp</b></td><td>底层使用 yt-dlp 实现稳定可靠的数据提取。</td></tr>
</table>

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

## 使用方法

向 Claude 分享 YouTube 链接：

```
请下载这个视频的简介：https://www.youtube.com/watch?v=xxx
```

或者批量下载频道简介：

```
请下载这个频道最新 10 个视频的简介：https://www.youtube.com/@channel
```

## 项目结构

```
youtube-desc-downloader/
├── SKILL.md                 # 技能定义文件
├── README.md                # 英文文档
├── README.zh-CN.md          # 中文文档
├── scripts/
│   └── download-desc.sh     # 核心下载脚本
└── references/
```

## 许可证

MIT — 见 [LICENSE](LICENSE)。

由 [opencode](https://github.com/anomalyco/opencode) 构建。