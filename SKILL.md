---
name: youtube-desc-downloader
description: Download YouTube video descriptions to local text files. Use when user shares a YouTube URL and asks to "download description", "save description", "下载简介", "下载描述", or wants to batch-download descriptions from a YouTube channel. Supports single video and batch channel download (latest N episodes).
metadata:
  author: Lucas
  version: 1.0.0
  input: YouTube URL + optional save path + optional count
  output: UTF-8 text files with video title, URL, and full description
compatibility: Requires yt-dlp and Python 3 installed and available in PATH.
---

# YouTube 视频简介下载器

将 YouTube 视频的完整简介（描述）下载为本地 UTF-8 文本文件。

## 使用方式

用户提供 YouTube 链接时自动触发，下载视频简介到指定路径。

**示例触发语句：**
- "下载这个视频的简介 https://www.youtube.com/watch?v=xxx"
- "把 https://www.youtube.com/watch?v=xxx 的描述保存下来"
- "Download description from https://www.youtube.com/watch?v=xxx"
- "下载 https://www.youtube.com/@channel/videos 最新50期的简介"
- "把这个频道最新的简介都下载下来"
- 用户直接粘贴 YouTube URL 并提到"简介"、"描述"、"description"

## 工作流程

### 单个视频下载

#### Step 1: 解析 URL
从用户输入中提取 YouTube 视频 ID。

支持格式：
- `https://www.youtube.com/watch?v={videoId}`
- `https://youtu.be/{videoId}`
- `https://www.youtube.com/watch?v={videoId}&t=2s`（忽略多余参数）

#### Step 2: 获取视频信息和简介

**关键：不要直接使用 `yt-dlp --print description`**，该命令在 Windows 上输出中文乱码。

正确方法：使用 Python 调用 `yt-dlp --dump-json`，解析 JSON 获取描述，用 UTF-8 编码写入文件。

```bash
python -c "
import subprocess, json, sys
sys.stdout.reconfigure(encoding='utf-8')
result = subprocess.run(
    ['yt-dlp', '--skip-download', '--dump-json', 'VIDEO_URL'],
    capture_output=True, timeout=30
)
data = json.loads(result.stdout)
desc = data.get('description', '')
title = data.get('title', 'unknown')
print(f'Title: {title}')
print(f'Description length: {len(desc)} chars')
print('---')
print(desc)
"
```

#### Step 3: 确定保存路径和文件名
- 如果用户指定了路径，使用该路径
- 如果用户指定了文件名，使用该文件名
- 默认文件名：`{视频标题}.txt`（清理非法字符后）
- 默认路径：当前工作目录

#### Step 4: 写入文件

```bash
python -c "
import subprocess, json, os, re, sys
sys.stdout.reconfigure(encoding='utf-8')

result = subprocess.run(
    ['yt-dlp', '--skip-download', '--dump-json', 'VIDEO_URL'],
    capture_output=True, timeout=30
)
data = json.loads(result.stdout)
desc = data.get('description', '')
title = data.get('title', 'unknown')
video_id = data.get('id', '')

# Clean filename
clean = re.sub(r'[\\\\/:*?\"<>|]', '', title).strip()
clean = clean[:80]
filepath = os.path.join('SAVE_DIR', f'{clean}.txt')

with open(filepath, 'w', encoding='utf-8') as f:
    f.write(f'Title: {title}\n')
    f.write(f'URL: https://www.youtube.com/watch?v={video_id}\n')
    f.write(f'---\n\n')
    f.write(desc)

print(f'Saved: {filepath} ({len(desc)} chars)')
"
```

### 批量下载频道简介（最新 N 期）

#### Step 1: 获取频道视频列表

```bash
yt-dlp --flat-playlist --print "%(id)s|||%(title)s" "CHANNEL_URL" --playlist-items 1:N 2>/dev/null
```

其中 `CHANNEL_URL` 格式为 `https://www.youtube.com/@{channel}/videos`，`N` 为用户指定的数量。

#### Step 2: 用 Python 批量下载

```bash
python -c "
import subprocess, json, os, re, sys
sys.stdout.reconfigure(encoding='utf-8')

# 从 Step 1 获取的列表中解析
videos = [
    ('videoId1', 'Title 1'),
    ('videoId2', 'Title 2'),
    # ... 更多视频
]

outdir = 'SAVE_DIR'
os.makedirs(outdir, exist_ok=True)

for i, (vid_id, title) in enumerate(videos):
    clean = re.sub(r'[\\\\/:*?\"<>|]', '', title).strip()
    filepath = os.path.join(outdir, f'{clean}.txt')
    
    try:
        r = subprocess.run(
            ['yt-dlp', '--skip-download', '--dump-json', f'https://www.youtube.com/watch?v={vid_id}'],
            capture_output=True, timeout=30
        )
        data = json.loads(r.stdout)
        desc = data.get('description', '')
        real_title = data.get('title', title)
        
        with open(filepath, 'w', encoding='utf-8') as f:
            f.write(f'Title: {real_title}\n')
            f.write(f'URL: https://www.youtube.com/watch?v={vid_id}\n')
            f.write(f'---\n\n')
            f.write(desc)
        
        print(f'[{i+1}/{len(videos)}] {clean}.txt ({len(desc)} chars)')
    except Exception as e:
        print(f'[{i+1}/{len(videos)}] FAILED: {vid_id} - {e}')

print('Done!')
"
```

#### 注意事项
- 批量下载时，每次 `yt-dlp --dump-json` 调用需要约 2-3 秒，50 个视频约需 2-3 分钟
- 如果用户没有指定数量，默认下载最新 20 期
- 输出目录默认为当前工作目录

## 文件格式

每个下载的文本文件格式如下：

```
Title: 视频标题
URL: https://www.youtube.com/watch?v=videoId
---

[视频完整简介内容，包含时间戳、链接等]
```

## 常见问题

### 问题：yt-dlp 输出中文乱码
**原因：** Windows 终端默认编码为 GBK，yt-dlp 输出 UTF-8 中文时显示为乱码。
**解决：** 不要直接使用 `yt-dlp --print description`。改用 `yt-dlp --dump-json` 配合 Python 的 `json.loads()` 解析，再用 `open(..., encoding='utf-8')` 写入文件。

### 问题：WebFetch 无法获取 YouTube 简介
**原因：** YouTube 简介通过 JavaScript 动态加载，WebFetch 只能获取静态 HTML。
**解决：** 始终使用 yt-dlp 工具。

### 问题：文件名包含非法字符
**原因：** 视频标题可能包含 Windows 文件名不允许的字符（`/ \ : * ? " < > |`）。
**解决：** 使用正则 `re.sub(r'[\\\\/:*?\"<>|]', '', title)` 清理文件名。

### 问题：Python 命令中编码报错
**原因：** Python 默认编码可能不是 UTF-8。
**解决：** 在脚本开头添加 `sys.stdout.reconfigure(encoding='utf-8')`。
