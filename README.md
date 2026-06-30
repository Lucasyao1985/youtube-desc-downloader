# YouTube 简介下载器 (youtube-desc-downloader)

将 YouTube 视频的完整简介（描述）下载为本地 UTF-8 文本文件。

## 功能特性

- 下载单个 YouTube 视频简介
- 批量下载频道最新 N 期简介
- 输出 UTF-8 文本：包含视频标题、URL 和完整描述
- 需要 yt-dlp 和 Python 3

## 安装

```bash
git clone https://github.com/Lucasyao1985/youtube-desc-downloader.git
```

### 依赖

```bash
pip install yt-dlp
```

## 使用示例

```
下载这个视频的简介：https://www.youtube.com/watch?v=xxx

把这个频道最新的简介都下载下来
```

## Skill 文件结构

```
youtube-desc-downloader/
├── SKILL.md           # 主技能文件
├── README.md          # 项目说明
└── scripts/           # 执行脚本
```

## License

MIT
