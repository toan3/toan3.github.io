# YouPlay Marketing Assets Pipeline

This directory and the `Scripts/` pipeline generate App Store screenshots and web marketing assets for YouPlay.

## Quick start

```bash
./Scripts/generate_marketing_assets.sh
```

This builds the app, captures raw screenshots, records preview frames, renders brand overlays, and validates sizes.

## Manual steps

1. **Chốt video mẫu và tagline với PO** trước khi chạy. Mặc định:
   - Video: `https://www.youtube.com/watch?v=g9JIUM0MHgQ`
   - Tagline: `Watch Videos in Your Language`
2. **Cấp quyền Screen Recording** cho terminal/process chạy script khi macOS hỏi.
3. Đảm bảo `python3.12` có `Pillow`.
4. (Tùy chọn) Cài `ffmpeg` để encode video `.mp4`; nếu thiếu, pipeline vẫn tạo GIF từ frames.

## Scripts

| Script | Purpose |
|---|---|
| `Scripts/generate_marketing_assets.sh` | Orchestrates the full pipeline |
| `Scripts/capture_app_store_screenshots.py` | Launches app and captures 3 raw screenshots |
| `Scripts/record_app_preview.py` | Records a sequence of frames for the app preview |
| `Scripts/render_brand_overlay.py` | Composites brand gradient, waveform, text, and app window |
| `Scripts/validate_marketing_assets.sh` | Checks App Store screenshot dimensions |

## Outputs

- Raw screenshots: `docs/assets/screenshots/raw/`
- Web hero image: `docs/assets/marketing/web_hero.png`
- Web hero GIF: `docs/assets/marketing/web_hero.gif`
- App preview frames: `docs/assets/marketing/preview_frames_branded/`
- App Store screenshots:
  - `fastlane/screenshots/en-US/<size>/`
  - `fastlane/screenshots/vi/<size>/`

## Supported App Store sizes

- 1280×800
- 1440×900
- 2560×1600
- 2880×1800

## Brand reference

- Background gradient: `#FC7200` → `#FD9023`
- Waveform stroke: `#FFF4E9` at 88% opacity
- Waveform accent: `#FFFFFF` at 56% opacity
- Font: SF Pro (system font fallback)

## Notes

- Pipeline không sửa code app.
- Nếu YouTube UI thay đổi hoặc video mẫu unavailable, cần chọn video mẫu khác và chạy lại.


## Current status

The pipeline scripts are implemented and the brand-overlay renderer was validated with synthetic placeholders. Real app capture was blocked by the sandboxed environment (GUI launch, screen recording, and external network access are restricted). Run `./Scripts/generate_marketing_assets.sh` on a normal macOS session with screen-recording permission and network access to generate final assets from the real YouPlay app.
