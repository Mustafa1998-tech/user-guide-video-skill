# User Guide Video Skill

[العربية](README.ar.md) · [English skill](SKILL.md) · [المهارة بالعربية](SKILL.ar.md)

A reusable AI-agent skill for producing Arabic software user-guide videos from real application screens. It documents the workflow used to create application walkthroughs: browser capture, structured storyboards, Arabic narration, captions, pointer/arrow emphasis, progressive zoom, Python/FFmpeg editing, and evidence-based media QA.

This repository provides **instructions**, not a one-command video generator or bundled application footage. Arabic and English files document the same workflow. Voice services, fonts, browser tooling, and media tools must be available in the environment where you use it.

## Files

| File | Contents |
|---|---|
| `SKILL.md` | English skill instructions and agent-discovery metadata |
| `SKILL.ar.md` | Equivalent original Arabic instructions |
| `README.ar.md` | Arabic usage guide |

## Use with an AI agent

Attach `SKILL.md` or `SKILL.ar.md`, identify your application, and request:

> Apply this skill to create an Arabic user-guide video for [application]. Use its actual interface and branding. Explain the workflows with narration, captions, a red arrow, and readable progressive zoom. Deliver an MP4 and editable production project. Record which quality checks were actually completed.

Specify the application URL or project location, authorized environment, language/dialect, target audience, required workflows, and output location. Provide credentials through the environment's private mechanism, not through files committed to this repository.

For a Codex-compatible installation, place this repository in a dedicated skill directory with `SKILL.md` at its root, for example `~/.codex/skills/arabic-software-training-video/`. Preserve any existing installation instead of overwriting it blindly. Invoke it as `$arabic-software-training-video`.

## Typical tools

Python, Playwright/Chromium, Pillow, NumPy, FFmpeg or imageio-ffmpeg, PyAV, an authorized speech provider such as edge-tts, and Arabic shaping/font support. Transcription and spreadsheet/PDF tools are optional, depending on deliverables. The skill explains which tool serves which purpose; verify package compatibility and actual availability before installation.

## Production principles

- Capture the real interface; do not invent controls or successful operations.
- Preserve brand identity and editable source material.
- Follow the skill's arrow specification: red `#D52424`, white outline, target-relative placement, a single eased approach, narration-synchronized cue, still hold, and gentle exit. Sizes/timings are adjustable production defaults.
- Distinguish animated screenshots from live recordings.
- Use original or licensed music and retain font licenses.
- Protect production data and require authorization for test writes.
- Do not equate ASR or a technical check with human listening or official approval.

The repository contains no application databases, credentials, internal network configuration, official organization logos, or customer footage. Third-party tools, fonts, services, and trademarks retain their own terms.
