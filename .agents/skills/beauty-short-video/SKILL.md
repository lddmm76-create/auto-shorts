---
name: beauty-short-video
description: >
  Produce repeatable Korean beauty and health short-form videos for TikTok, Instagram Reels,
  YouTube Shorts and Naver Blog clips. Use for script-to-video, clinic information shorts,
  sunscreen/skincare education, treatment explainers, AI model B-roll, voiceover, bilingual
  subtitles, vertical editing, and batch variants. Routes generation to available image/video
  tools and performs deterministic local assembly with FFmpeg; never assumes CUDA or paid API
  access.
license: MIT
metadata:
  version: "1.0.0"
  based_on:
    - https://github.com/akillness/jeo-skills
    - https://github.com/social-media-skills/video-editing-skill
---

# Korean Beauty Short-Video Production Skill

## User profile and fixed production defaults

Use these defaults unless the user explicitly changes them.

- Primary content: beauty, skincare, dermatology/aesthetic clinic education and promotions.
- Main target: vertical 9:16, 1080x1920, 30 fps, H.264 MP4.
- Language: Korean narration. When bilingual subtitles are requested, English first and Korean translation directly below.
- Models in B-roll: Korean women in their 20s or 30s, chosen to match the topic. Use distinct faces and vary pose, hairstyle, framing and action between shots.
- Motion: natural real footage or generated video motion. Do not replace a requested moving scene with a still poster.
- Subtitles: lower safe area but never over the model's face; use a Korean-capable font such as Noto Sans KR / Noto Sans CJK KR. Verify glyphs in the rendered frames.
- Do not add clinic logos, contact details, prices, treatment claims or directions unless supplied or verified.
- For The Beauty Clinic, use only confirmed details: 더뷰티의원, 055-372-3993, 양산시 물금읍 범어로 62 치선타운 405호, and closing time 20:00. Never reuse the obsolete 14:00 closing time.
- Prefer free/local tools and existing connected tools. Never spend credits or trigger a paid generation without clear user approval.
- The user's known Windows machine has Intel Iris Xe graphics, not an NVIDIA CUDA GPU. Do not instruct CUDA-only workflows or assume GPU acceleration. Prefer CPU-compatible FFmpeg and Node workflows.

## Choose the right production route

1. **AI footage / model / image-to-video required:** use the connected image/video generation tool only if available and permitted. Generate individual B-roll shots, not a poster. Ask for approval before any operation that consumes paid credits. If no generation tool is available, prepare the shot prompts and use supplied footage.
2. **Existing footage editing:** use local FFmpeg for trim, concat, crop, subtitles, audio normalization and export. For talking-head recordings, use the upstream Video Editing Skill for transcription, pause removal and cut planning.
3. **Text-led motion graphics:** use Remotion only when it materially helps. Before using it commercially, check the current Remotion licence for the user's organisation. The upstream Remotion Shorts template documents that its bundled fonts do not support Korean/CJK; do not use its stock template unchanged for Korean text. Either patch and verify a Korean font implementation first, or use FFmpeg subtitle rendering instead.
4. **Do not promise full automation where a step requires a human account login, paid API, source footage, voice service or platform approval.**

## Production workflow

### 1. Write the script

For a 20–45 second short, prepare:
- Hook in the first 1–2 seconds.
- One main point per scene.
- Voiceover text in natural spoken Korean.
- Visual direction for every scene.
- On-screen English and Korean subtitle lines only when bilingual output is requested.
- A clear ending / save / follow / inquiry action.
- Source notes for medical, scientific, pricing or statistical claims.

For medical content, do not invent efficacy, safety, duration, contraindications, before/after results or guaranteed outcomes. Distinguish general education from clinic-specific claims. Flag claims that need clinician review.

### 2. Create a scene plan

Default structure:

| Time | Purpose | Visual |
|---|---|---|
| 0–2 s | Hook | Close-up or strong visual action |
| 2–8 s | Problem | Relevant skin / lifestyle B-roll |
| 8–18 s | Explanation | Demonstration, product use or simple graphic |
| 18–30 s | Practical steps | 2–3 concise actions |
| 30–40 s | Summary / CTA | Calm model shot and short CTA |

Use a different shot size or angle for each scene. Avoid repeated faces, repeated poses, static poster replacements, visible staff gestures, unnecessary hands, face arrows and invented clinic logos.

### 3. Prepare assets

Use descriptive names, for example:
- assets/scene01_hook.mp4
- assets/scene02_problem.mp4
- assets/scene03_demo.mp4
- assets/scene04_steps.mp4
- assets/scene05_end.mp4
- assets/voice_ko.wav
- assets/music_licensed.mp3
- subtitles.srt

Check aspect ratio, duration, frame rate, audio presence and ownership/licence. Never use copyrighted music unless the user has rights to it.

### 4. Assemble with FFmpeg

Use FFmpeg as the deterministic local assembly layer. Check installation first:

    ffmpeg -version
    ffprobe -version

For a source clip, reframe to vertical without stretching:

    ffmpeg -i input.mp4 -vf "scale=1080:1920:force_original_aspect_ratio=increase,crop=1080:1920,setsar=1,fps=30" -c:v libx264 -pix_fmt yuv420p -c:a aac -movflags +faststart output_vertical.mp4

For Korean subtitles, specify a real installed Korean font with the subtitles filter's force_style or fontsdir option. Escape Windows paths correctly. Do not assume Arial contains Korean glyphs. Test one short render first and inspect it.

For bilingual subtitles, use two lines per cue: English first, Korean below. Keep each line concise and place captions within the platform safe area. Avoid placing captions across eyes, mouth or treatment areas.

Normalize final audio to a sensible social-video loudness (target around -14 LUFS integrated, true peak no higher than -1 dBTP) and verify that speech remains intelligible over music.

### 5. Quality checks before delivery

Run ffprobe and inspect rendered frames at the beginning, middle and end.
- Correct 1080x1920 / 9:16 / 30 fps output.
- No black frames, frozen stills where motion was requested, missing assets or broken transitions.
- Korean characters render correctly; no tofu boxes or clipped text.
- English line is above Korean line when bilingual captions are requested.
- Captions do not cover the model's face or key treatment area.
- Voice and video are synchronized; no clipped words.
- Music is licensed and quieter than narration.
- No unsupported medical claims, incorrect clinic details or fabricated results.
- Export opens and plays successfully.

If any check fails, fix and render again before claiming completion.

### 6. Deliver and publish

Deliver the MP4 plus script, subtitle file and asset list. Do not publish automatically. Prepare platform-specific captions and ask for explicit confirmation before posting. If a connected publishing service is not configured, provide the final files for manual upload.

## How to respond

Do the work, not just describe a plan. Keep user-facing explanations short. Do not ask for information already present in the conversation. Ask only for an essential missing input. Report what was actually rendered and checked; never claim that a local file was created or played unless it was.
