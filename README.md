# WeChat Videohao Q-Video Skill

A Codex Skill for turning long-form WeChat public-account articles into vertical short videos for 视频号, Douyin, TikTok-style feeds, and other mobile-first content channels.

中文一句话：这是一个“公众号文章转视频号竖版短视频”的 Codex Skill。它把一篇文章拆成脚本、图解、动画、字幕、配音、BGM、封面和结尾，让内容创作者不用每次从零设计视频流程。

## What This Skill Does

This Skill helps Codex convert an article into a complete vertical explainer video workflow.

It is designed for creators who already have written content, especially analytical articles, and want to turn them into short videos without losing the article's logic.

Instead of making a simple slideshow, it builds a structured video:

```text
Full vertical cover
        ↓
Segmented article explainer
        ↓
Full vertical ending card
```

The body of the video uses a stable mobile-first stack:

```text
Top topic bar
Current article Q-comic infographic
Dark-tech animated explainer board
Voice-synced bottom captions
```

The key principle:

> In every segment, the voiceover, Q-comic image, animated explainer, and captions must explain the same point at the same time.

This prevents the common low-quality result where the audio talks about one thing, the image shows another, and the animation is just decorative.

## Who This Is For

This Skill is useful for:

- WeChat public-account writers who want to repurpose articles into 视频号 content.
- Automotive commentators turning market analysis into short videos.
- Product analysts explaining launches, pricing, strategy, user pain points, or industry competition.
- Solo creators who want a repeatable video production workflow.
- Small teams that need consistent daily short videos from written reports.
- AI content operators building article-to-video pipelines.

It was originally tuned for automotive industry commentary, but the structure can be adapted to:

- AI tool tutorials;
- consumer electronics analysis;
- finance or business explainers;
- SaaS product updates;
- local service industry reports;
- company newsletters;
- educational micro-lessons;
- personal IP commentary videos.

## What Problem It Solves

Long articles often fail when moved to short video because:

- the script is too long;
- the video becomes a boring PPT;
- captions do not match the voice;
- images are beautiful but do not explain the argument;
- animated panels are generic and unrelated;
- the cover is just a cropped screenshot;
- the ending feels dead or unfinished;
- every episode has a different visual style.

This Skill turns the article into a repeatable production system:

1. Extract the article's core logic.
2. Split it into 5-6 short-video segments.
3. Write a natural-fast voiceover script.
4. Generate article-specific Q-comic infographics.
5. Build a dark-tech animated explanation layer.
6. Sync captions with the spoken narration.
7. Add a recognizable cover and ending card.
8. Mix narration and BGM with voice in front.
9. Render and QA the final video.

## What Value It Provides

### 1. Content Strategy

It forces the article to become a short-video argument:

- what happened;
- why it matters;
- what the pressure or contradiction is;
- what ordinary users should pay attention to;
- what conclusion or action point remains.

This makes the video easier to follow than a raw reading of the article.

### 2. Visual Consistency

Each episode uses the same visual architecture:

- Q-comic article logic card;
- dark-tech explainer panel;
- synced caption bar;
- full vertical cover;
- fixed-style ending.

This helps a creator build a recognizable video identity over time.

### 3. Better Viewer Comprehension

The video uses different layers for different jobs:

- voiceover explains the story;
- Q-comic card gives the viewer a quick visual summary;
- animated board shows the logic path;
- captions help viewers follow without full attention;
- cover and ending make the video platform-ready.

### 4. Faster Daily Production

Once configured, the same workflow can be reused for daily articles. The creator only needs a new article and topic-specific visuals; the structure remains stable.

### 5. Personal Voice and Brand

The workflow supports local voice cloning and fixed BGM, so the output can feel like a personal creator channel rather than a generic AI slideshow.

## Typical Use Cases

### Daily WeChat Article to 视频号

Input:

- one finished WeChat article;
- optional existing article images;
- creator voice reference;
- fixed BGM.

Output:

- vertical MP4;
- standalone cover image;
- ending card;
- structured storyboard;
- synced captions.

### Automotive Market Commentary

Good for topics like:

- car model discontinuation;
- price war;
- dealer pressure;
- EV charging infrastructure;
- smart driving competition;
- brand positioning;
- sales ranking analysis.

Example segment logic:

```text
Event -> Market pressure -> User decision -> Brand implication -> Final judgment
```

### Product or Industry Explainer

Good for articles that explain:

- why a product failed;
- why a new feature matters;
- how a business model changes;
- what ordinary users should check before buying;
- how a company strategy affects the market.

### Knowledge Creator Workflow

Good for creators who publish:

- weekly insight videos;
- AI tool explainers;
- product teardown videos;
- industry trend summaries;
- short educational clips.

## Tools Used In The Workflow

This Skill is not tied to one rendering tool. It describes a coordinated production pipeline.

Recommended tools:

- **Codex Skills**: orchestrates the workflow and remembers production rules.
- **WeChat article JSON / Markdown / draft text**: source content.
- **ChatGPT Image 2 / Image2**: generates full vertical cover, Q-comic cards, and ending images.
- **Qwen3 local voice cloning**: creates the creator-style voiceover from a local reference recording.
- **HyperFrames**: builds HTML-based animated video compositions.
- **Remotion**: optional alternative or companion for React-based video composition.
- **GSAP**: controls motion, reveals, highlights, and timing inside HTML video compositions.
- **ffmpeg**: mixes audio, loops BGM, extracts QA frames, and checks duration/silence.

You can replace individual tools if your stack is different. The important part is the production logic:

```text
Article logic -> Storyboard -> Voice -> Image -> Animation -> Captions -> BGM -> QA -> MP4
```

## Output Structure

A typical final episode includes:

```text
assets/
  qcovers/
    topic-vertical-cover-image2.png
  qcards_image_two/
    segment-01.png
    segment-02.png
    ...
  qendings/
    topic-ending-image2.png
  narration.wav
  ending-narration.wav

data/
  storyboard.json
  narration.txt
  ending-narration.txt
  audio-sync.json

renders/
  topic-vertical-final.mp4
  qc_frames/
    first_frame.png
    body_frame_early.png
    body_frame_middle.png
    ending_frame.png
```

## Video Design Logic

### Cover

The cover is a complete `9:16` vertical Q-comic poster.

It should contain:

- large title;
- sharp subtitle;
- Q-style creator character;
- article-specific visual metaphor;
- 3-4 key evidence blocks;
- bottom final judgment.

The first video frame should already show this cover. Avoid a black or dim fade-in before the cover, because short-video platforms may use the first frame as preview.

### Body Q-Comic Card

The top body image is not decoration. It is a visual article card.

It should:

- summarize the current segment;
- use a Q-comic hand-drawn infographic style;
- include short, readable Chinese keywords;
- show one clear visual metaphor;
- match the voiceover point.

### Middle Explainer

The middle area is a dark-tech animated logic board.

It can show:

- pressure chains;
- comparison paths;
- conversion from old standard to new standard;
- warning labels;
- checklist flow;
- capability bridge;
- signal tracking;
- evidence cards.

Avoid:

- generic charts repeated in every segment;
- decorative cars that do not explain anything;
- old labels from previous articles;
- empty panels at scene start;
- text so faint that viewers cannot read it.

### Captions

Captions are real voice subtitles, not summaries.

They should:

- use the exact narration text;
- split into short spoken clauses;
- appear as the voice reaches that phrase;
- stay large and readable on mobile;
- use a thin bottom strip so the main visual area remains spacious.

### Ending

The ending has a fixed structure but topic-specific content:

- final judgment;
- 2-3 action/check points;
- one comment question;
- light follow/continue prompt.

It should also have a short ending voiceover, usually faster than the body narration:

```text
所以，<本期最终判断>。<本期互动问题>？评论区聊聊。
```

## Installation

Clone the repository:

```bash
git clone https://github.com/hh19880814-bot/wechat-videohao-qvideo-skill.git
```

Install it into Codex:

```bash
mkdir -p ~/.codex/skills
cp -R wechat-videohao-qvideo-skill ~/.codex/skills/
```

Restart Codex or start a new thread.

## How To Trigger It

Example prompts:

```text
Use the Videohao Q-video Skill to turn today's WeChat article into a vertical short video.
```

```text
把这篇公众号文章按视频号 Q-video Skill 做成竖版短视频。
```

```text
调用这个 Skill，把汽车行业文章生成视频号成片，带封面、配音、字幕和结尾。
```

## What The User Needs To Provide

At minimum:

- article text or article JSON;
- desired topic/title if there are multiple articles;
- preferred duration range if different from default;
- whether to use existing article images or regenerate all images.

For a full personal workflow:

- a voice reference recording;
- a preferred BGM;
- an example of accepted visual style;
- local paths for the article project and video output project.

## Personal Assets And Privacy

This repository does not include private assets.

It does not commit:

- real voice recordings;
- BGM audio;
- article source files;
- generated videos;
- generated covers;
- generated Q-comic images.

For the original local workflow, private assets are stored outside the repo. A user adapting this Skill should replace those paths with their own files:

```text
<your-voice-reference>.m4a
<your-fixed-bgm>.m4a
<your-article-source-folder>
<your-video-output-folder>
```

## Example Configuration

The original workflow used:

```text
voice reference: creator-voice-reference.m4a
BGM: creator-fixed-bgm.m4a
BGM volume: about 0.12
canvas: 1080x1920
layout: center-safe vertical stack
style: Q-comic article card + dark-tech explainer
voice: natural-fast Chinese narration
```

Your own setup can replace all of these.

## Quality Checklist

Before final delivery, check:

- the article source is correct;
- the storyboard is based on the current article;
- the cover is a standalone full vertical image;
- frame 0 directly shows the cover;
- Q-comic body cards are not reused from old topics;
- the middle explainer has visible content from scene start;
- animation labels match the narration;
- captions follow the voice clause by clause;
- the voice has no awkward long silence;
- BGM is audible but does not cover narration;
- the ending card is complete and topic-specific;
- the final MP4 and cover image are ready for publishing.

## Common Failure Modes

| Problem | Cause | Fix |
|---|---|---|
| Cover looks like a cropped article card | It was stitched or converted from a body image | Regenerate a full vertical Image2 cover |
| Video feels like PPT | Middle board is static or generic | Use article-specific animated logic |
| Captions do not match voice | Captions use summaries instead of narration | Rebuild captions from the exact voiceover |
| Animation turns too late | Timing was planned before audio | Derive scene timing from real voice duration |
| BGM is too loud | Music treated as equal to narration | Lower BGM, keep voice in front |
| Q image and voice mismatch | Segment logic was not unified | Rebuild storyboard with one core point per segment |

## Why This Matters

Short videos are not just shorter articles. They need:

- faster opening judgment;
- clearer visual hierarchy;
- synchronized voice and text;
- platform-safe layout;
- recognizable creator style;
- repeatable production discipline.

This Skill packages those decisions into a reusable Codex workflow.

The practical value is simple:

> Turn written insight into a publishable short video without losing the original article's thinking.

## Repository Contents

```text
SKILL.md   The actual Codex Skill
README.md  Human-readable explanation
.gitignore Prevents private media assets from being committed
```

## License / Reuse

MIT License. You can adapt the workflow for your own article-to-video pipeline.

Before reuse, replace:

- voice reference;
- BGM;
- article source paths;
- image style;
- output project paths;
- any creator-specific wording.

The workflow is most valuable when customized to a creator's own voice, visual identity, and publishing rhythm.
