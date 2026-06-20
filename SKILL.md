---
name: wechat-videohao-qvideo
description: Use this when turning a WeChat public-account article, newsletter, industry analysis, or long-form Chinese article into a multi-platform vertical short video: ChatGPT Image 2 cover and ending, Q-comic logic cards, dark middle explainer, narration-synced captions, cloned or consistent voiceover, low-volume looping BGM, upload-grade MP4, and publishing copy. Default to 9:16 vertical unless the user explicitly requests landscape.
---

# WeChat / Douyin / Videohao Q-Video Skill

Use this Skill when the user wants to turn a written article into a polished vertical short video for WeChat Channels, Douyin, TikTok-style feeds, Xiaohongshu, Bilibili vertical video, or other mobile-first platforms.

Default output:

```text
Full 9:16 Image 2 cover
-> body video stack
-> full 9:16 Image 2 ending card
```

Body video stack:

```text
compact topic bar
-> current-article Q-comic infographic
-> dark animated explainer board
-> bottom real narration subtitles
```

The core rule:

```text
voiceover, Q-comic image, middle explainer, and subtitles must explain the same point at the same time.
```

## Non-Negotiable Rules

- Default to `1080x1920` vertical video. Only make landscape when the user explicitly asks.
- Use the current article, not a generic topic and not a previous episode.
- Cover and ending must be complete standalone `9:16` ChatGPT Image 2 / Image 2 images.
- Do not make the cover or ending by cropping a horizontal card, stitching screenshots, or reusing a body layout.
- Body Q-comic images should be article-specific: Q-style hand-drawn infographic, stable creator character, short logic text, clear visual metaphor.
- The middle explainer is not decoration. It must summarize and structure the current chapter's core idea.
- Bottom subtitles must be real spoken narration, not a separate summary.
- BGM must continue through the whole video. If the BGM file is shorter than the video, loop it.
- Keep narration clearly in front. BGM is atmosphere, not the main character.
- Render an upload-grade MP4, not only a low-bitrate preview.
- Always QA frames and audio before calling the video final.

## Multi-Platform Visual Rule

Treat cover and ending images as multi-platform publishing assets by default.

Do not put platform-specific words into the image, such as:

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

Before sending an Image 2 prompt, remove platform-specific wording from the prompt. After generation, visually check corners, stickers, seals, badges, title bars, and small labels. If platform wording appears, regenerate or fix the image before rendering the video.

## Recommended Local Inputs

Adapt paths to your machine. Treat these as configurable variables:

- `<ARTICLE_SOURCE>`: article text, Markdown, JSON, or draft export.
- `<VOICE_REFERENCE>`: optional creator voice reference for local voice cloning.
- `<FIXED_BGM>`: preferred background music file.
- `<OUTPUT_ROOT>`: folder where the video project and final renders are written.
- `<BASELINE_PROJECT>`: optional previous accepted project used as a style baseline.

If any input is missing, ask the user for it instead of silently switching to unrelated placeholders.

## Production Order

1. Read the article.
   - Extract title, digest, key paragraphs, claims, evidence, conclusion, and reader-facing implication.
   - Classify the article as quick comment, deep analysis, or topic explainer.
   - Do not rewrite the article unless the user asks.

2. Build a storyboard.
   - Usually use 5-6 body chapters.
   - Each chapter should contain:
     - chapter title,
     - one summary sentence,
     - 3 small nodes or checkpoints,
     - narration paragraph,
     - bottom subtitle clauses,
     - Q-comic image intent,
     - middle explainer content.

3. Write narration.
   - Use natural, conversational Chinese.
   - Open with a voice hook on the cover. Do not let the cover sit silently.
   - Keep sentences short enough for subtitle display.
   - Make the narration match the middle explainer exactly in logic, though not word-for-word.

4. Generate voiceover.
   - Prefer a consistent creator voice or cloned voice.
   - Avoid default system voices unless the user accepts them.
   - Split long narration into manageable chunks, then stitch.
   - Check actual audio durations before timing visuals.

5. Generate visual assets.
   - Cover: full 9:16 Image 2 poster, topic-specific.
   - Body Q cards: article-specific Q-comic logic images.
   - Ending: full 9:16 Image 2 closing poster, topic-specific.
   - Inspect images for platform-specific labels, stale topic text, wrong logos, and unreadable small text.

6. Build the video.
   - Canvas: `1080x1920`.
   - Keep the body stack inside a mobile-safe center area with black breathing room above and below.
   - Use a compact topic bar above the Q-comic card.
   - Put the dark explainer directly below the Q-comic card.
   - Put the bottom subtitle strip under the explainer, not at the extreme bottom edge.

7. Sync chapter motion.
   - Chapter title and summary should appear quickly at chapter start.
   - Small nodes should light up quickly when the narration reaches the corresponding idea.
   - Do not chase word-perfect animation. Aim for reasonable narration-to-logic alignment.
   - Default chapter breathing gap: `0.3s`.
   - If the video feels too tight, use `0.35s`.
   - If the user wants a faster flow, try `0.15s`.
   - Use very short audio fades only to avoid pops, not obvious cut-to-black style fading.

8. Mix BGM.
   - Start around `0.10-0.12` volume under narration.
   - Loop BGM for the entire video if needed.
   - Check that BGM continues after the first segment and through the ending.
   - Lower BGM if it competes with narration.

9. Render and QA.
   - Export upload-grade MP4.
   - Recommended target: `1080x1920`, H.264, AAC, around `10-12 Mbps` video bitrate.
   - Extract frames:
     - frame 0 / cover,
     - early body,
     - middle body,
     - late body,
     - ending.
   - Check audio track, total duration, and long silence.

## Storyboard Shape

Use this shape for each body chapter:

```json
{
  "id": "chapter-id",
  "title": "短标题",
  "summary": "本章中心思想，一句话说清。",
  "nodes": [
    {"label": "维度1", "text": "节点短句1"},
    {"label": "维度2", "text": "节点短句2"},
    {"label": "维度3", "text": "节点短句3"}
  ],
  "narration": "真实口播稿。",
  "captionClauses": ["底部字幕短句1", "底部字幕短句2"],
  "qComicIntent": "本章 Q 版图解画面要表达什么。",
  "middleExplainerIntent": "中间深色解释框要表达什么。"
}
```

## Cover Image Guidance

The cover is a shareable poster, not a cropped video frame.

Include:

- large article-specific title,
- sharp subtitle,
- Q-style creator character,
- central visual metaphor,
- 3-4 evidence or logic blocks,
- bottom conclusion sentence.

Avoid:

- platform-specific badges,
- real brand logos unless legally and contextually appropriate,
- tiny unreadable walls of text,
- generic stock-poster composition,
- old article labels.

The first frame of the video should already show the full cover. Do not fade in from black.

## Body Q-Comic Guidance

Each body Q-comic card should:

- match the current chapter,
- carry one central visual metaphor,
- use short readable Chinese keywords,
- include the Q creator as explainer when useful,
- avoid too much tiny text,
- avoid stale labels from other episodes.

## Middle Explainer Guidance

The middle explainer should look like a dark premium explanation board.

Use:

- deep background,
- glass panels,
- fine grid or scan lines,
- amber/yellow highlights,
- cyan active highlight,
- clear headline,
- one summary sentence,
- 3 nodes or checkpoints.

Good structures:

- risk checklist,
- responsibility split,
- timeline,
- chain reaction,
- old rule vs new rule,
- user decision checklist,
- final judgment.

Avoid:

- random decorative charts,
- generic car animation that explains nothing,
- empty panels,
- unreadably faded inactive text,
- labels from old topics.

## Subtitle Guidance

- Bottom subtitle = current spoken line.
- Keep it short and readable.
- Do not put a separate summary in the subtitle strip.
- If the spoken sentence is too long, split into clauses.

## Final QA Checklist

Before delivery, verify:

- final video is `1080x1920`,
- video bitrate is upload-grade, not preview-grade,
- audio track exists,
- BGM loops or lasts through the full video,
- no long accidental silence,
- frame 0 is the full cover,
- cover and ending are Image 2 full vertical images,
- cover and ending contain no platform-specific text by default,
- body Q-card matches the current chapter,
- middle explainer matches narration,
- bottom subtitles match spoken narration,
- ending card is complete and topic-specific.

## Delivery Package

Final response should include:

- final MP4 file,
- short title,
- video description,
- topic tags,
- optional standalone cover path.

Do not send only a raw file path. The user should know what changed, why it is ready, and how to publish it.
