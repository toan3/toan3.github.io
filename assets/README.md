# Marketing Assets Status

## Generated automatically

- `docs/assets/marketing/web_hero.png` — web hero image (2400×1600)
- `docs/assets/marketing/web_hero.gif` — web hero GIF (800px wide)
- `docs/assets/marketing/preview_frames_branded/` — branded frames for App Preview video
- `fastlane/screenshots/en-US/<size>/` — localized App Store screenshots (en-US)
- `fastlane/screenshots/vi/<size>/` — localized App Store screenshots (vi)

## Current status

The **brand overlay pipeline** is fully implemented and validated. The assets above were generated using **synthetic placeholders** because the current sandboxed environment cannot:

1. Launch the YouPlay GUI app.
2. Record the screen.
3. Load external YouTube content over the network.

To replace placeholders with real app captures, run the pipeline on a normal macOS session with screen-recording permission and network access:

```bash
./Scripts/generate_marketing_assets.sh
```

If you have a pre-built app bundle (for example from Xcode), point to it:

```bash
YOUTUBE_DUBBER_APP=/path/to/YouPlay.app ./Scripts/generate_marketing_assets.sh
```

To encode the App Preview video from branded frames (requires ffmpeg):

```bash
ffmpeg -framerate 30 -i docs/assets/marketing/preview_frames_branded/frame_%04d.png \
  -c:v libx264 -pix_fmt yuv420p -movflags +faststart -crf 18 \
  docs/assets/marketing/app_preview.mp4
```

## Notes

- Replace `docs/assets/screenshots/raw/*.png` with real screenshots before final submission.
- The current screenshots use a synthetic app window; they are intended to validate the brand-overlay pipeline only.
- Taglines are placeholders pending PO approval.
