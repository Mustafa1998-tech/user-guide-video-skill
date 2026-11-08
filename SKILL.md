---
name: arabic-software-training-video
description: Produce or improve Arabic software-training videos from an existing application, user guide, or narrated video. Covers real UI capture, Arabic voice-over and captions, progressive focus motion, original music, editable Python/FFmpeg production, and documented media QA. Use for narrated application walkthroughs; not for rebuilding an application or generic promotional videos.
metadata:
  short-description: Arabic application walkthroughs with narration, focus motion, and media QA
---

# Arabic Software User Guide Video

Turn an existing application's interface and documentation into a practical walkthrough that can be reviewed and edited. Every instruction must refer to a real interface element. Every quality claim must be supported by an actual check.

## Establish scope and references

- Read the user's request and attachments before choosing a production style. Identify the language or dialect, branding, deliverables, and limits on displaying data.
- Inspect previous video, source narration, captions, and timing when available. Distinguish the approved source script from a transcript inferred from audio.
- Treat the current application as the authority for functionality, field names, buttons, and routes. Use supplied images and official templates as visual references.
- Reuse an editable production project when available rather than recapturing correct material unnecessarily.
- Modern Standard Arabic is the default for institutional Arabic material. Respect an explicit request for another dialect; do not mix styles within the same version.
- A video-production request does not authorize application-code, permission, network, or production-data changes, publication, or sending material to other people.

## Choose available tools

Use tools that are actually available. Do not assume a voice service, API key, or GPU exists.

| Tool | Purpose |
|---|---|
| Python and a virtual environment | Organize and run the production pipeline |
| Playwright + Chromium | Capture the actual interface and test playback |
| Pillow | Frames, titles, layers, pointer, and focus positions |
| NumPy | Audio processing or original procedural music |
| FFmpeg, locally or through imageio-ffmpeg | Motion, composition, encoding, and audio processing |
| edge-tts or an authorized provider | Narration and word-boundary timing |
| arabic-reshaper and python-bidi | Arabic shaping fallback when RAQM is unavailable |
| PyAV | Media duration, frame counts, and clip checks |
| faster-whisper | Optional local transcription for review when resources permit |
| openpyxl | Pronunciation and review records |
| HTML/Chromium or a suitable PDF tool | Readable Arabic quality report |

Check Python/package compatibility before installing dependencies. Use an isolated environment and record versions. Obtain fonts from their official sources and preserve licenses.

## Create an editable storyboard

Use structured data such as `storyboard.json`. For each step, record:

- Chapter, step title, spoken script, and required capture.
- The element to highlight and whether motion illustrates a screenshot or records a real action.
- The evidence supporting the instruction, any waiting period, and the actual result where applicable.

Write short sentences that explain one action at a time. Keep interface labels as displayed. Do not read every visible word to fill time, or omit necessary explanations to shorten the video.

Apply partial Arabic diacritics to ambiguous words, especially product names, organization names, and technical terms. Maintain an editable pronunciation dictionary. Text diacritics alone do not prove that generated speech is pronounced correctly.

## Capture the interface and protect data

1. Capture the real interface at a resolution that supports readable zooming. Use an appropriate device pixel ratio rather than AI upscaling.
2. Save target-element rectangles and crop offsets alongside captures, together with viewport dimensions and device pixel ratio.
3. Review labels, values, tooltips, links, and the visible account, not just filled inputs.
4. Use a training environment or documented masking in the preview. Do not change production data merely to create a safe screenshot.
5. Label substituted information as examples. `example.org` and `192.0.2.10` can replace operational links and addresses.
6. Pointer motion or zoom over a still screenshot is an illustration, not a live recording. Describe it accurately.
7. To capture a genuine successful save, use an authorized isolated test environment and verify the write destination first. Clean up test records afterward. If unavailable, explain the procedure without fabricating a success message.

Do not send application screenshots or data to a narration provider. Send only the general explanatory text, respecting the user's restrictions on external processing.

## Narration and Arabic captions

- Verify voice availability and test a representative passage. A regional voice identifier does not by itself establish dialect, formal Arabic, or natural delivery.
- Retain approved text, audio, and word boundaries for each segment. Regenerate only changed segments.
- Derive audio-cache keys from text, voice, rate, and pronunciation settings; file existence alone is not a valid cache key.
- Build SRT from the approved script, retaining punctuation, and align its words with timing boundaries. Do not assemble raw transcript tokens and lose punctuation.
- Document estimated timing where exact alignment is unavailable. Do not describe it as precise listening-based verification.
- Check Arabic rendering. Prefer native shaping with RAQM; use reshaper/bidi only when needed. Do not shape or reverse text twice.
- Test the font with Arabic, numbers, and mixed technical text. Avoid incomplete font subsets.
- Position captions outside the important action area. Keep them readable at phone size and preferably within one or two lines.

## Motion and branding

- Extract colors, fonts, and logos from the actual project. Use the original logo without redrawing or recoloring it.
- Show the current instruction clearly instead of crowding all instructions around a small screenshot.
- Zoom progressively into the action while preserving aspect ratio and the entire relevant field or button.
- Use a clear pointer, eased movement, and a brief click indication where useful. Align the click with the corresponding spoken instruction.
- Keep transitions calm. Avoid shaking, flashing, and purposeless repeated zooming.
- When an introduction and ending are requested, use the same identity and reveal the logo, organization, and title progressively. Durations such as 8–12 seconds are examples, not universal requirements.
- Do not present a proposed tagline as an officially approved slogan.

## Arrows: color, placement, and motion

These are recommended production defaults, not claims about every existing video. Adapt them to the application's density and the user's reference while keeping one consistent annotation style throughout a delivery.

### Appearance

- Use **red `#D52424`** for the instructional arrow, with a **white `#FFFFFF` outline** to separate it from both light and dark interfaces. Keep the application's own colors and logo unchanged.
- At 1920×1080, start with a 5 px shaft, 2 px white outline, 18 px arrowhead, and approximately 90–160 px total length. Scale these values proportionally to the output resolution and check readability at phone size.
- A small black shadow at roughly 18% opacity with 3 px blur is optional. Do not add neon glow, heavy 3D effects, emoji, or a text arrow glyph. Draw the annotation as a clean vector path or a high-resolution transparent layer.
- Distinguish the tutorial arrow from the actual mouse pointer: the arrow explains the target; the pointer indicates navigation or an actual click. Avoid showing both when they obscure the same control.

### Placement and coordinates

- Point at the edge of the actual button, field, or link, leaving about 6–12 px clearance at Full HD. Do not cover its label, typed value, icon, focus outline, validation message, or captions.
- Prefer a diagonal or short curved path from nearby empty space. Display one instructional arrow per action. For several actions, reveal arrows sequentially rather than leaving a collection on screen.
- Save a target rectangle and an anchor relative to the source capture. Apply the same crop, scaling, pan, and zoom transform to the arrow tip as to the screenshot. Never hard-code a fixed screen coordinate for a moving zoom.
- Before additional zoom/pan, a simple crop-and-scale mapping is `screenX = offsetX + scale * (sourceX - cropX)` and likewise for Y. Apply any later animation transform too, and check the actual encoded frame.
- RTL/LTR affects annotation text layout, not the real target location. Do not mirror an arrow automatically merely because the narration language changes.

### Timing and movement

1. Let the relevant screen settle. Fade the arrow in over approximately 0.15–0.25 seconds.
2. If movement helps explain the action, move the tip toward its target once over approximately 0.35–0.65 seconds using eased motion. Do not bounce, shake, spin, or repeat the movement continuously.
3. A useful easing function is `e = (1 - cos(pi * u)) / 2`, where `u` is elapsed progress clamped to 0–1. Interpolate position using `p = start + (end - start) * e`. For a curved path, evaluate the curve at eased progress and orient the arrowhead along its tangent.
4. Complete the movement as the narrator names the target or says “click here.” Derive this cue from the narration timeline or a reviewed word boundary; do not apply the same arbitrary delay to every scene.
5. Hold the arrow still while the viewer reads the control and hears the instruction. A 1–2 second hold can be a starting point, but the spoken instruction and target readability determine the actual duration.
6. If depicting a click, show a single subtle ring for about 0.3–0.5 seconds at the target, synchronized to the cue. This annotation must not imply that a real action or successful save occurred when it did not.
7. Fade the arrow out over approximately 0.15–0.25 seconds before switching targets or scenes. In a reduced-motion version, replace travel/zoom with a static arrow and a gentle fade; avoid pulsing or flashing.

Store color, dimensions, source rectangle, anchor, path, cue, entrance duration, hold, and exit duration in editable storyboard/render settings. Preview the arrow at the start, during zoom, at the cue, and at the end. Confirm it remains attached to the correct element, within frame, and readable on both themes without hiding captions or interface content.

## Audio and music

Use original or appropriately licensed music, retaining its source or generation method. Do not imitate a specific protected composition.

Normalize narration and prevent clipping. If music accompanies speech, duck it according to the narration signal rather than assuming a fixed level is sufficient. Avoid noise reduction on clean digital speech when it damages consonants.

Keep narration, music, and mix settings separate for editing. Do not speed up speech to meet an arbitrary duration; adjust scenes to fit the explanation.

## Timing and encoding details

- Measure audio using PCM/WAV or sample counts rather than estimated MP3 duration.
- Build the final timeline from actual encoded-clip lengths or frame-grid-rounded durations. Include chapter separators and audio lead-ins/tails.
- Bind SRT and chapter boundaries to the final timeline, not an earlier timeline with cumulative rounding drift.
- Inspect the installed FFmpeg version's options. Do not assume `filter_complex_script` exists; pass the filter graph directly when appropriate.
- Write decimal durations such as `0.65` rather than `.65` for filters that reject the latter.
- Use explicit paths and structured subprocess arguments. Do not construct shell commands from narration or chapter titles.
- Invalidate render caches when images, target rectangles, fonts, logos, or layout code change.
- When exporting standalone chapters, inspect keyframe boundaries and audio starts. Verify the extracted files themselves.

## Quality review and truthful approval

Perform checks appropriate to the material:

- Decode the complete video/audio and check resolution, frame rate, duration, and tracks.
- Measure loudness and peak levels; check for gaps and clipping.
- Compare captions with the approved script and validate timing order and final boundaries.
- Inspect frames from the actual final render, including introduction, ending, zooms, validation messages, and success states.
- Test playback and seeking in a browser or suitable player, including a phone-size preview.
- Confirm each referenced element exists, the focus target is correct, and important text is not cropped.
- Validate PDF, XLSX, standalone clips, and archive contents when requested.

**Automatic transcription is not listening.** ASR may identify passages needing review, but discrepancies can be recognition errors or spelling differences.

Record technical checks, automated text comparison, documented listening, and formal approval separately. Never mark listening or approval as complete unless it happened.

If required direct or human listening is unavailable, state that clearly. Deliver the supported files and a segment-by-segment listening review record; do not claim flawless pronunciation. Do not report an ASR-based change as a confirmed listening correction.

The pronunciation record should include timestamp, segment, approved text, transcript or flagged word, requested correction, and listening/resolution status.

## Delivery

Follow requested names and formats. A full delivery may include:

- Main MP4 and separate introduction/ending.
- Narration WAV, Arabic SRT, and chapter timestamps.
- Pronunciation-review XLSX and quality-report PDF showing verified and outstanding items.
- Storyboard, safe captures, fonts/licenses, audio assets, editing code, and dependency information.
- Standalone chapter clips when useful.

Keep the editing project portable; exclude developer-machine paths and login credentials. Inspect the package before creating an archive. Link only files that exist, and state material limitations without claiming unperformed work.
