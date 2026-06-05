---
name: wechat-videohao-qvideo
description: Use this when turning a WeChat public-account article / 公众号文章 into a vertical 视频号/抖音 short video: full Image2 Q-comic cover, current-article Q-comic logic cards, dark-tech animated explainer, synced bottom captions, local cloned narration, fixed low-volume BGM, and full Image2 ending card. Default to vertical; make landscape only when explicitly requested.
---

# WeChat 视频号 Q-Video Skill

Use this Skill when the user asks to turn a公众号文章、汽车行业文章、每日公众号成稿、视频号样片、抖音竖版视频 into the accepted vertical article-video format.

The default output is a vertical `1080x1920` video for 视频号/抖音:

`完整 Image2 封面 -> 正文内容栈 -> 完整 Image2 结尾卡`

正文内容栈:

`顶部主题栏 -> 当前文章 Q版公众号图解 -> 中间深色科技讲解动画 -> 底部同步字幕`

## Non-Negotiable Rules

- Default to vertical video. Only make landscape when the user explicitly asks for横版.
- Source must be the current article JSON/draft, not a generic article and not yesterday's topic.
- Use only title, digest, summary, body paragraphs, and current-article generated image assets.
- Do not reuse old article images from other topics.
- Do not use stitched/cropped covers. Cover must be a new complete standalone `9:16` ChatGPT Image 2 / Image2 Q-comic image.
- Body Q images should follow the公众号生图 logic: Q版手绘信息图, clear title, core points, visual metaphor, stable Q author character, article-specific conclusion.
- Middle animation must explain the same point being spoken. Never leave stale labels from another article.
- Bottom captions must match the spoken narration clause by clause, not summarize the paragraph.
- Voice uses the local Qwen3 speaker-embedding route with the user's real voice reference.
- BGM uses the fixed light-tech BGM at low volume, with narration clearly in front.
- Always QA with extracted frames before saying the video is done.

## Required Local Assets

On a new computer, prepare equivalent files. Paths will differ across users. Treat these as configurable variables:

- `<VOICE_REFERENCE>`: creator's voice reference audio, used for local voice cloning.
- `<FIXED_BGM>`: creator's fixed background music, mixed quietly under narration.
- `<ARTICLE_SOURCE_DIR>`: folder containing WeChat article JSON, Markdown, or draft text.
- `<VIDEO_OUTPUT_ROOT>`: folder where the generated video project and renders are written.
- `<BASELINE_PROJECT>`: optional previous accepted project to copy as a style baseline.

If the machine lacks these assets, ask the user to provide or copy:

- the source article JSON,
- the fixed BGM file,
- the real voice reference,
- the latest baseline project folder if possible.

Original workflow example:

```text
VOICE_REFERENCE = creator-voice-reference.m4a
FIXED_BGM = creator-fixed-bgm.m4a
ARTICLE_SOURCE_DIR = 公众号文章 runs folder
BASELINE_PROJECT = latest accepted qvideo project
```

## Production Order

1. Locate today's article.
   - Search the公众号 project `runs/` folder for today's `*-manual-YYYYMMDD.json`.
   - If the user names the topic, pick the matching article.
   - Read title, digest, summary, and body paragraphs.
   - Do not rewrite the article unless the user asks.

2. Split the article into a unified storyboard.
   - Usually use 6 content beats.
   - Each beat must include:
     - `id`
     - `title`
     - `shortLabel`
     - narration paragraph
     - subtitle/quote
     - Q-comic image intent or actual image path
     - middle explainer headline
     - middle explainer labels/chips/details
     - caption clauses
   - Each layer must talk about the same point.

3. Write the narration.
   - Default length: standard-long, about `520-620` Chinese characters for 100-125 seconds when the article has enough logic.
   - Use natural-fast conversational style.
   - Add some emotion and push, but not shouting.
   - Avoid broadcast voice, slow explainer prose, and long pauses.
   - Keep sentences short enough for captions.

4. Generate local Qwen3 cloned voice.
   - Use the user's real reference voice:
     `<VOICE_REFERENCE>`
   - Use local Qwen3 speaker-embedding / 声纹向量, not an external TTS service.
   - Default speed: around `1.06`; if the user wants more push, use slight post-tempo rather than rushing every sentence.
   - Prefer short chunks around `70-90` Chinese characters.
   - After generation, stitch and clean the audio.
   - Check total duration and long silence before rendering.

5. Derive timing from real audio.
   - Do not rely only on planned word count.
   - Create an `audio-sync.json` using real durations, either per generated part or char-weighted from the final narration file.
   - Scene starts, middle highlights, and bottom captions should follow the actual voice duration.

6. Generate images.
   - Cover: new full `9:16` Image2 vertical Q-comic poster.
   - Body Q cards: current-article Q-comic logic images, usually horizontal, displayed fully in the top area.
   - Ending: new full `9:16` Image2 vertical Q-comic ending image.
   - Do not create cover or ending by composing HTML blocks, cropping a横图, or stitching top/middle/bottom screenshots.

7. Build the vertical video.
   - Canvas: `1080x1920`.
   - Content safe zone: keep the main stack in the center with black breathing room above and below, so 视频号/抖音 UI does not cover the core content.
   - First frame must already be the complete cover. No dark fade-in before cover.
   - Body scenes use:
     - compact top theme bar,
     - current Q-comic article card,
     - dark-tech middle explainer,
     - thin bottom synced caption strip.
   - Ending card appears after the body with a short closing narration.

8. Mix BGM.
   - Use the fixed BGM:
     `<FIXED_BGM>`
   - Start with `--bgm-volume 0.12`.
   - Keep narration clearly in front.
   - If BGM covers the voice, lower it again.
   - Do not fall back to old fantasy-game or unrelated BGM unless the user explicitly asks.

9. Validate and deliver.
   - Run layout check.
   - Render MP4.
   - Extract frames:
     - first frame / cover,
     - early body frame,
     - middle body frame,
     - late body frame,
     - ending frame.
   - Confirm:
     - frame 0 is cover, not black/dim,
     - Q card is complete,
     - middle explainer is not empty,
     - middle labels match the current article,
     - captions are visible and synchronized,
     - ending is complete,
     - BGM does not mask narration.
   - Send the final MP4 and cover image directly in chat when possible.

## Article Storyboard Rules

A good 6-beat automotive article video usually follows:

1. Hook / what happened.
2. Why this is not just a surface event.
3. Core pressure or contradiction.
4. What ordinary users should actually look at.
5. Buying / industry / brand implication.
6. Final judgment.

Do not mechanically force every article into this shape. If the article is a快评, use tighter beats. If it is a深拆, keep more detail.

Each beat should contain:

```json
{
  "id": "article-specific-id",
  "title": "短标题",
  "shortLabel": "栏目标签",
  "narration": "真实口播稿，后续用于字幕同步。",
  "subtitle": "本段一句话判断。",
  "quote": "适合画面强调的金句。",
  "dynamic": {
    "type": "statement | warning | chain | conversion | checklist | lift",
    "headline": "中间解释区主标题",
    "chips": ["关键词1", "关键词2", "关键词3"],
    "core": "本段核心"
  },
  "detailRows": [
    ["维度1", "解释1"],
    ["维度2", "解释2"],
    ["维度3", "解释3"]
  ],
  "metrics": [
    ["标签1", "值1"],
    ["标签2", "值2"],
    ["标签3", "值3"]
  ],
  "imageTwoCard": "assets/qcards_image_two/current-topic-card.png"
}
```

## Image2 Cover Rule

The cover is a complete poster image, not a video frame layout.

Cover prompt should include:

- Q版手绘信息图;
- full vertical `9:16`;
- large title;
- clear subtitle;
- article-specific visual metaphor;
- stable Q author character;
- 3-4 visual evidence blocks;
- bottom final judgment;
- no real brand logo if avoidable, but topic can be recognizable when the article is about a named model/brand.

Cover must work as:

- platform cover image,
- first frame of the video,
- first 2-3 seconds opening scene.

The first frame must show the cover directly. Avoid black fade-in before the cover, because platform previews may use frame 0.

## Body Q-Comic Image Rule

Body Q cards should reuse the current article's own Q-comic illustration logic.

Each body Q image should:

- correspond to one storyboard beat;
- show the article's current point, not a generic car poster;
- include readable Chinese keywords;
- include one central visual metaphor;
- use Q author character as narrator/explainer;
- avoid overloaded tiny text;
- avoid old topic labels.

If existing body images are from the same article and were generated with Image2, they can be used. If they are old, off-topic, or cropped, regenerate.

## Middle Explainer Design Rule

The middle explainer is not another Q image. It is a dark-tech animated explanation board.

Accepted style:

- dark premium tech background;
- fine grid;
- glass panels;
- cyan scan/flow lines;
- amber/yellow tags;
- large but not oversized headlines;
- readable details;
- no empty center;
- no stale labels from previous articles.

Use one of these visual logic types:

- `statement`: big judgment card + supporting evidence.
- `warning`: two-sided pressure / conflict / risk warning.
- `chain`: step-by-step chain, product -> price -> experience.
- `conversion`: old standard -> new standard.
- `checklist`: buying or action checklist.
- `lift`: final upgrade / larger industry conclusion.

Important:

- Do not add a decorative car just to fill space.
- Do not repeat the same curve chart in every scene.
- Do not fade inactive text until it becomes unreadable.
- At scene start, the middle board should already have visible content; local highlights can appear later with the voice.
- Highlighted text should follow the narration point by point.

## Caption Rule

Bottom captions are real subtitles.

- Use exact narration text, split into short spoken clauses.
- Show one clause at a time.
- Caption timing follows real voice duration.
- Weighting by character count is acceptable for a first pass.
- Style: large bold white Chinese text with black shadow/outline.
- Keep the caption strip thin so it does not steal height from the middle explainer.
- Do not show an entire paragraph at once.
- Do not use small gray summary text.

## Voice Rule

Use the local Qwen3 voice clone route.

Voice direction:

- natural-fast;
- energetic;
- conversational;
- short pauses;
- not broadcast tone;
- not too slow;
- no obvious broken pauses.

Reference voice:

`<VOICE_REFERENCE>`

Typical flow:

1. Convert reference to clean 24k mono WAV.
2. Generate Qwen3 speaker-embedding parts.
3. Stitch and trim.
4. Check duration.
5. Check long silence over `0.8s`.
6. Use final narration duration to rebuild scene timing.

If audio is good but visuals are wrong, keep the audio and fix visuals. Do not regenerate voice unnecessarily.

## Ending Rule

Ending is long-term fixed in structure, but the image content changes per topic.

Ending image:

- complete Image2 vertical Q-comic long image;
- final judgment;
- 2-3 action/check points;
- one comment question;
- light follow/continue prompt;
- topic-specific picture and conclusion.

Ending narration:

```text
所以，<本期最终判断>。<本期互动问题>？评论区聊聊。
```

Ending voice should be slightly faster than body narration. It should feel like a clean收尾, not another正文段落.

BGM continues underneath.

## BGM Rule

Default BGM:

`<FIXED_BGM>`

Default volume:

`0.12`

Principles:

- narration first;
- BGM as subtle second lane;
- no loud music competing with the voice;
- if user says BGM is big, lower it further;
- do not change BGM unless user explicitly asks.

## QA Checklist

Before final delivery:

- Article source is correct and current.
- Six beats are all from the article.
- Cover is standalone Image2 full vertical image.
- Frame 0 directly shows the cover.
- Body Q images are current-article Q-comic images.
- Middle explainer labels match the article, not old template labels.
- Middle board has visible content at scene start.
- Captions match narration.
- Captions are readable on phone.
- Voice has no long awkward silence.
- BGM is audible but low.
- Ending card is standalone Image2 and complete.
- Final MP4 and cover are provided to the user.

## Failure Fixes

- If cover looks like a cropped article card: discard and regenerate full Image2 vertical cover.
- If middle explainer looks low or empty: rebuild labels and layout around the current article's logic, not generic tech decoration.
- If captions do not match voice: rebuild captions from `beat.narration`, not `beat.subtitle`.
- If animation turns pages too late: rebuild timing from real voice duration.
- If BGM covers voice: lower BGM from `0.12` further, do not boost narration only.
- If visuals are wrong but voice is good: keep voice, fix visuals.
- If user wants “昨天那个逻辑”: use this vertical workflow, not the older landscape GT7 workflow.

## Final Delivery Format

When done, answer in Chinese and show the media directly:

```markdown
做好了，竖版成片如下：

![视频标题](/absolute/path/to/final.mp4)

封面单独给你：

![封面](/absolute/path/to/cover.png)
```

Also mention:

- approximate duration;
- BGM volume used;
- whether cover/ending are standalone Image2;
- whether Qwen3 local cloned voice was used.
