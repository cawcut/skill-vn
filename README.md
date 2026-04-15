# VN Video Editor — AI Agent Skill

Local video, audio, and image processing on macOS and Windows, powered by [VN Video Editor](https://www.vlognow.me/#download). No cloud upload, no API key — everything runs on-device.

## Platform Support


| Platform                          | Status    | Skill Name             | CLI Binary                                  |
| --------------------------------- | --------- | ---------------------- | ------------------------------------------- |
| **macOS** (Intel + Apple Silicon) | Available | `vn-skill`             | `vnapp-cli` universal binary                |
| **Windows** (x64)                 | Available | `vn-skill-for-windows` | `vn-tools-cli.exe` (auto-installed via MSI) |


---

## macOS — `vn-skill`

### Requirements

- **macOS 13.0** or later
- **VN Video Editor** installed from the [Mac App Store](https://apps.apple.com/us/app/vn-video-editor/id1494451650)
- MCP Server enabled in VN Settings

### Install

```bash
clawhub install vn-skill
```

The CLI binary (`vnapp-cli`) is automatically downloaded during skill installation. It is a universal build (x86_64 + arm64), signed with Developer ID and notarized by Apple.

### Features


| Capability              | Command          | Description                                                  | VN Draft |
| ----------------------- | ---------------- | ------------------------------------------------------------ | -------- |
| Extract Audio           | `extract-audio`  | Extract audio track from video (M4A)                         | —     |
| Extract Frame           | `extract-frame`  | Grab a frame/thumbnail at any position (PNG/JPEG)            | —     |
| Auto Captions           | `auto-captions`  | Generate subtitles via on-device Whisper and burn into video | Yes   |
| Add SRT Subtitles       | `add-caption`    | Burn existing SRT file into video with customizable style    | Yes   |
| Compress Video          | `compress-video` | Re-encode video with target resolution, fps, bitrate         | Yes   |
| Compress Image          | `compress-image` | Compress/resize images (JPEG, PNG, WebP, HEIC)               | —     |
| Concatenate Videos      | `concat-video`   | Merge clips with 50+ transition styles                       | Yes   |
| Denoise                 | `denoise`        | Reduce noise from audio or video via DeepFilterNet           | —     |
| Portrait Cutout (Image) | `cutout-image`   | Remove background from person image (PNG with transparency)  | —     |
| Portrait Cutout (Video) | `cutout-video`   | Remove background from person video (MP4, composited on black) — **Apple Silicon only** | Yes |


### Draft Management

Commands marked **Yes** in the Draft column keep a VN draft by default after export (`--keep-draft`). This lets you open the result in VN Video Editor for further editing.

- **Default**: drafts are kept after export
- **Opt out**: tell the agent "don't keep drafts" once, and all subsequent draft-supporting commands in the session will skip drafts (`--no-keep-draft`)
- **Per-task override**: say "keep draft" or "no draft" on any individual task to override the session preference

### Skill Contents

```
vn-skill/
├── SKILL.md                        # Agent behavior spec, intent mapping, progress reporting, failure handling
└── references/
    └── cli-reference.md            # Complete CLI option reference
```

---

## Windows — `vn-skill-for-windows`

### Requirements

- **Windows 10+** (x64)

### Install

```bash
clawhub install vn-skill-for-windows
```

### Features


| Capability              | Command          | Description                                                |
| ----------------------- | ---------------- | ---------------------------------------------------------- |
| Extract Audio           | `extract-audio`  | Export audio track from video                              |
| Extract Frame           | `extract-frame`  | Save a single frame as an image (PNG/JPEG)                 |
| Auto Captions           | `auto-captions`  | Transcribe speech via on-device Whisper and burn subtitles |
| Add SRT Subtitles       | `add-caption`    | Burn existing SRT file into video with customizable style  |
| Compress Video          | `compress-video` | Re-encode video with target resolution, bitrate            |
| Compress Image          | `compress-image` | Compress/resize images (JPEG, PNG, WebP, HEIC)             |
| Concatenate Videos      | `concat-video`   | Join multiple video clips                                  |
| Denoise                 | `denoise`        | Remove background noise via DeepFilterNet                  |
| Portrait Cutout (Video) | `cutout-video`   | Segment foreground subject from video                      |


### Skill Contents

```
vn-skill-for-windows/
├── openclaw.plugin.json          # Plugin manifest
├── package.json                  # npm package metadata & OpenClaw SDK config
├── src/
│   └── index.ts                  # Plugin entry — auto-install & before_tool_call hook
├── scripts/
│   └── vn-tools-cli-install.ps1  # Silent MSI installer
├── skills/
│   └── vn-skill-for-windows/
│       └── SKILL.md              # Agent skill — command reference & UX guidelines
└── hooks/
    └── vn-skill-for-windows-package-compat/
        ├── HOOK.md
        └── handler.ts
```

---

## Support

- **macOS**: [vn.support+mac@ui.com](mailto:vn.support+mac@ui.com)
- **Windows**: [vn.support+windows@ui.com](mailto:vn.support+windows@ui.com)