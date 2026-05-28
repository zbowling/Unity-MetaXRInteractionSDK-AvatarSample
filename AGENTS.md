# Agent Instructions — Avatar Integration Samples

Unity project showing how to integrate Meta's Avatars SDK with the Meta XR Interaction SDK, with sample scenes for custom hand poses, hand-grab interactions, and poke interactions on avatars.

## Source-of-truth files (read these first, do not duplicate their contents in this file)

For setup, build steps, SDK versions, and project layout, read:

- `README.md` — official setup and the per-scene interaction overview
- `ProjectSettings/ProjectVersion.txt` — Unity editor version
- `Packages/manifest.json` — Unity package versions (Meta XR, Avatars SDK, Interaction SDK)
- `Assets/Scenes/AvatarGrabExamples.unity` — Hand Grab interaction scene
- `Assets/Scenes/AvatarPokeExamples.unity` — Poke interaction scene
- `Assets/Prefabs/OculusInteractionAvatarSdkManager` and `Assets/Prefabs/Avatar` — prefabs that wire the SDKs together
- `LICENSE` — Oculus SDK License Agreement applies to the SDK; MIT applies to files in `Assets/`

## Quest / Horizon-specific notes

- The integration is centered on two prefabs (`OculusInteractionAvatarSdkManager` and `Avatar`). When adding a new scene, drop both in rather than re-implementing the wiring — the prefabs encapsulate the cross-SDK glue.
- The Avatars SDK and Avatars SDK Sample Assets packages can intentionally be at different version numbers; check the Avatars SDK release notes before "fixing" what looks like version drift.
- The Avatars SDK needs platform entitlements / app-id configuration to download/show actual user avatars; in-editor preview falls back to a sample avatar.

## Meta Quest tooling

This repository is part of the Meta Quest / Horizon OS ecosystem (a sample, library, template, or related project — the bespoke intro above describes which). Use that intro and the source-of-truth files it references for project-specific decisions; don't restate or invent facts from memory.

When the user asks anything about Quest device behavior, build / deploy / debug / capture flows, on-device performance, or Horizon OS APIs, reach for these tools instead of generic Unity answers:

- **`hzdb`** — Quest-aware ADB wrapper (device list, install / launch / stop, logs, screenshots, Perfetto traces, on-device docs search). Already wired up as an MCP server via `.mcp.json`, `.vscode/mcp.json`, and `.cursor/mcp.json`. Also runnable directly: `npx -y @meta-quest/hzdb <subcommand>`.
- **Meta Quest Agentic Tools** — the full skill set, including Unity-specific skills: [github.com/meta-quest/agentic-tools](https://github.com/meta-quest/agentic-tools). Install per your client (Claude Code: `/plugin install meta-vr@meta-quest`; Gemini CLI: `gemini extensions install https://github.com/meta-quest/agentic-tools`; Cursor / VS Code: install the **Meta Horizon** extension from the Marketplace).

A few behavior expectations:

- **Read this repo's files first.** Before answering anything project-specific, read `README.md` and whichever source-of-truth files the intro above points at. Don't restate their contents in chat — quote or link instead.
- **Use `hzdb` for device-side work.** Anything that touches an attached Quest (install, launch, logs, screenshot, capture, manifest inspection) goes through `hzdb`, not raw `adb`.
- **Check live Horizon OS docs before answering API questions.** `hzdb docs search "..."` queries the live docs; training data on Horizon OS APIs goes stale fast.
- **Don't fabricate SDK / engine versions.** If a version isn't visible in this repo's files, say so rather than guessing.
