# WeChat / Douyin / Videohao Q-Video Skill

A public Codex Skill for turning long-form Chinese articles into polished vertical short videos.

中文一句话：这是一个把公众号文章、行业分析、产品解读、汽车评论等长文，稳定转换成竖版短视频的 Codex Skill。它不只是做幻灯片，而是把文章逻辑拆成“封面、图解、动画、字幕、配音、BGM、结尾、发布文案”的完整生产流程。

## What This Skill Does

This Skill helps Codex create a repeatable article-to-video workflow:

```text
Article
-> storyboard
-> narration
-> Q-comic images
-> animated explainer
-> synced captions
-> BGM mix
-> upload-grade vertical MP4
```

The default video structure is:

```text
Full 9:16 Image 2 cover
        ↓
Body video stack
        ↓
Full 9:16 Image 2 ending card
```

The body stack is:

```text
Compact topic bar
Current-article Q-comic infographic
Dark animated explainer board
Bottom narration-synced subtitles
```

The key idea is simple:

> The voiceover, image, middle explainer, and subtitles should explain the same idea at the same time.

That rule prevents the common AI-video problem where the audio says one thing, the image shows another, and the motion graphics are just decoration.

## Who It Is For

This Skill is useful for:

- WeChat public-account writers repurposing articles into short videos.
- Automotive commentators making daily market or product analysis videos.
- Product analysts explaining launches, pricing, strategy, or user pain points.
- AI content operators building article-to-video pipelines.
- Small teams that need repeatable daily vertical-video production.
- Solo creators who want consistent style without redesigning every episode.

It was tuned through automotive commentary videos, but the structure can be adapted to:

- AI tool tutorials,
- consumer electronics analysis,
- finance or business explainers,
- SaaS product updates,
- company newsletters,
- local service reports,
- educational micro-lessons,
- personal IP commentary.

## Problem It Solves

Long articles often fail when converted to short video because:

- the script is too long,
- the video becomes a boring PPT,
- captions do not match the voice,
- images are nice but do not explain the argument,
- animated panels are generic,
- the cover is just a screenshot,
- the ending feels unfinished,
- every episode has a different visual style.

This Skill turns the process into a stable production system:

1. Extract the article's core logic.
2. Split it into 5-6 short-video chapters.
3. Write a natural voiceover script.
4. Generate topic-specific Q-comic infographics.
5. Build a dark animated logic board for each chapter.
6. Sync captions with the spoken narration.
7. Add a standalone cover and ending card.
8. Loop and mix BGM under narration.
9. Render, inspect, and deliver an upload-grade MP4.

## Output Example Structure

A typical output project may look like this:

```text
assets/
  qcovers/
    topic-cover-image2.png
  qcards/
    segment-01.png
    segment-02.png
  qendings/
    topic-ending-image2.png
  audio/
    narration.wav
    bgm.m4a

data/
  storyboard.json
  audio-sync.json

renders/
  topic-final-upload.mp4
  qa-cover-frame.png
  qa-body-frame.png
  qa-ending-frame.png
```

The exact folder names can change. The production logic matters more than the file layout.

## Core Design Principles

### 1. Cover And Ending Are Real Posters

The cover and ending should be complete `9:16` Image 2 images.

Do not make them by:

- cropping horizontal cards,
- stitching screenshots,
- exporting HTML blocks,
- reusing a body frame.

They should work as standalone shareable poster images.

### 2. Multi-Platform By Default

The same video may be posted on WeChat Channels, Douyin, Xiaohongshu, Bilibili, TikTok-style feeds, or other platforms.

Therefore the image itself should not contain platform-specific wording unless the creator explicitly asks for a platform-specific variant.

Avoid text like:

- `视频号解读`
- `抖音专用`
- `小红书笔记`
- `快手`
- `B站`
- `TikTok`

Use neutral labels instead:

- `本期解读`
- `重点清单`
- `风险清单`
- `购车前先看`
- `一图看懂`

This is especially important because image generation models may accidentally add platform labels into corner badges or stickers. Always inspect the generated image before rendering.

### 3. Middle Explainer Is The Logic Layer

The middle board is not a subtitle and not a decorative dashboard.

It should show:

- chapter title,
- one summary sentence,
- 3 nodes or checkpoints,
- quick highlights that follow the narration.

The animation does not need word-perfect sync. It should be reasonably aligned with the voiceover and move fast enough for short-video pacing.

### 4. Bottom Subtitle Is The Spoken Line

The bottom subtitle strip should show the actual spoken narration clause.

Do not put a separate summary there. The summary belongs in the middle explainer.

### 5. BGM Must Continue

If the BGM file is shorter than the video, loop it. A common production bug is that BGM only plays for the first segment and disappears later. This Skill explicitly checks for that.

## How To Install

Clone this repository:

```bash
git clone https://github.com/hh19880814-bot/wechat-videohao-qvideo-skill.git
```

Copy or symlink the Skill into your Codex skills folder:

```bash
mkdir -p ~/.codex/skills/wechat-videohao-qvideo
cp SKILL.md ~/.codex/skills/wechat-videohao-qvideo/SKILL.md
```

Restart Codex or refresh the Skill list if needed.

## How To Call It

In Codex, you can say things like:

```text
Use wechat-videohao-qvideo to turn this WeChat article into a vertical short video.
```

```text
按照 wechat-videohao-qvideo 这个 skill，把这篇公众号文章做成 9:16 视频。
```

```text
用这个 skill 做一个汽车行业分析视频，封面、正文、结尾都要完整。
```

```text
继续按这个 Q-video workflow，做今天这篇文章的视频。
```

If your Codex environment supports Skill metadata, the Skill can also trigger when the task mentions:

- WeChat article to video,
- 公众号文章转视频,
- 视频号竖版视频,
- 抖音短视频,
- Q-comic infographic video,
- dark middle explainer,
- narration-synced captions.

## What You Need To Provide

At minimum:

- article text, Markdown, JSON, or a WeChat draft export;
- target topic or title;
- desired publishing platform if it is platform-specific.

Recommended:

- fixed creator voice reference,
- preferred BGM,
- previous accepted video sample,
- existing Q-comic article images,
- desired length.

If you do not have all of these, the Skill can still guide the workflow. It will ask for missing assets instead of silently switching to unrelated placeholders.

## Typical Workflow

### Step 1: Read And Structure The Article

Codex extracts:

- what happened,
- why it matters,
- the central contradiction,
- what users should pay attention to,
- the final judgment.

### Step 2: Create 5-6 Chapters

Each chapter gets:

- short title,
- one summary sentence,
- 3 small nodes,
- narration paragraph,
- subtitle clauses,
- image direction,
- middle explainer direction.

### Step 3: Generate Images

Use ChatGPT Image 2 / Image 2 for:

- full vertical cover,
- body Q-comic cards,
- full vertical ending card.

The style should be:

- Q-style hand-drawn infographic,
- stable creator character,
- readable Chinese text,
- visual metaphor,
- article-specific logic,
- no stale labels from old topics.

### Step 4: Generate Voiceover

Use a consistent creator voice when possible.

If using local voice cloning, generate audio first and derive scene timing from actual audio durations. Do not rely only on estimated word count.

### Step 5: Build The Body Video

Default layout:

```text
topic bar
Q-comic card
dark explainer
caption strip
```

Keep the stack in the mobile-safe center area. Leave breathing room above and below so platform UI does not cover the core content.

### Step 6: Mix BGM And Render

Recommended output:

- `1080x1920`
- H.264 video
- AAC audio
- about `10-12 Mbps` video bitrate for upload
- BGM volume around `0.10-0.12` under narration

### Step 7: QA

Before delivery, inspect:

- first frame,
- early body frame,
- middle body frame,
- late body frame,
- ending frame,
- audio track,
- BGM continuity,
- subtitle readability,
- platform-specific unwanted text.

## Example Prompt To Codex

```text
Use wechat-videohao-qvideo.

Article title:
德国公司想卖小米汽车？先看授权和风险

Article summary:
德国公司计划进口中国电动车，小米官方否认合作并启动法律程序。请把重点放在：海外热度、官方授权、非官方进口风险、售后质保、软件法规、本地服务体系。

Requirements:
- 9:16 vertical video
- Image 2 cover and ending
- Q-comic body cards
- dark middle explainer
- real narration subtitles at the bottom
- BGM should loop through the whole video
- do not put platform-specific words in the images
- deliver MP4, short title, description, and tags
```

## Final Delivery Checklist

A finished video package should include:

- final MP4,
- short title,
- video description,
- topic tags,
- optional standalone cover image,
- confirmation that BGM continues,
- confirmation that cover and ending contain no platform-specific text.

## Why This Matters

The biggest value of this Skill is not one template. It is the production discipline:

- article logic first,
- voice and visuals aligned,
- cover and ending treated as real assets,
- platform-safe image text,
- audio checked before delivery,
- upload version separated from preview version.

That discipline is what makes AI-assisted short-video production feel less random and more like a repeatable creator workflow.

## License

MIT. Use it, modify it, and adapt it to your own creator workflow.
