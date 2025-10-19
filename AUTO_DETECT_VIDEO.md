# Auto Video Detection - How It Works

## Problem Fixed
Previously, `manifest.json` had a hardcoded video title:
```json
"input_video": "downloads/Environmental Pollution Video.mp4"
```

This caused errors when processing different videos.

## Solution
The system now **automatically detects** the latest video in the `downloads/` folder.

## How It Works

### 1. Auto-Detection Logic (`auto_edit.py`)
When you run `edit_video.bat`, it calls `auto_edit.py` which:
1. Checks if `manifest.json` has `"AUTO_DETECT"` values
2. Searches the `downloads/` folder for `.mp4` files
3. Finds the **most recent** video (sorted by modification date)
4. Automatically generates the output filename (adds `_EDITED` suffix, replaces spaces)
5. Updates `manifest.json` with the detected paths
6. Processes the video

### 2. Example Flow
```
downloads/
  └── My Cool Video.mp4  (latest)

↓ Auto-detection finds it ↓

manifest.json updated:
  "input_video": "downloads/My Cool Video.mp4"
  "output_video": "edited/My_Cool_Video_EDITED.mp4"

↓ Editor runs ↓

edited/
  └── My_Cool_Video_EDITED.mp4
  └── My_Cool_Video_EDITED.srt
  └── My_Cool_Video_EDITED.metadata.json
  └── My_Cool_Video_EDITED.txt
```

### 3. Benefits
✅ **No manual editing** - Just drop video in `downloads/` folder
✅ **Works with any video** - No hardcoded titles
✅ **Always processes latest** - Automatically finds newest video
✅ **Clean filenames** - Spaces replaced with underscores

## Usage

### Simple Method (Recommended)
1. Put your video in `downloads/` folder
2. Run `edit_video.bat`
3. Done! Check `edited/` folder for results

### Manual Method (Advanced)
If you want to specify a video manually:
1. Edit `manifest.json`
2. Set `input_video` and `output_video` paths
3. Run `edit_video.bat`

## Files Modified

### Video Editor:
- **manifest.json** - Changed to `AUTO_DETECT` placeholders
- **auto_edit.py** - Added `auto_detect_latest_video()` function (lines 1089-1122)
- **auto_edit.py** - Added auto-detection logic in `main()` (lines 1156-1173)
- **edit_video.bat** - Simplified to just call auto_edit.py

### YouTube Uploader:
- **youtube_uploader.py** - Added `auto_detect_latest_edited_video()` function (lines 257-285)
- **youtube_uploader.py** - Added auto-detection in `main()` (lines 302-307)
- **upload_to_youtube.bat** - Changed to use `--video AUTO`

## Error Handling
- ❌ No `downloads/` folder → Clear error message
- ❌ No `.mp4` files found → Clear error message
- ✅ Multiple videos → Processes the **latest** one

## Complete Workflow

### End-to-End Automation (No Hardcoded Filenames!)

```bash
# Step 1: Put raw video in downloads/
downloads/My Video.mp4

# Step 2: Edit the video
edit_video.bat
# → Auto-detects: downloads/My Video.mp4
# → Creates: edited/My_Video_EDITED.mp4
# → Creates: edited/My_Video_EDITED.srt
# → Creates: edited/My_Video_EDITED.metadata.json

# Step 3: Upload to YouTube
upload_to_youtube.bat
# → Auto-detects: edited/My_Video_EDITED.mp4
# → Auto-detects: edited/My_Video_EDITED.metadata.json
# → Auto-detects: edited/My_Video_EDITED.srt
# → Uploads to YouTube with AI metadata!
```

### Command Line Usage

**Video Editor:**
```bash
# Auto-detect (recommended)
py auto_edit.py --manifest manifest.json --work-dir work

# Manual path
py auto_edit.py --manifest custom_manifest.json --work-dir work
```

**YouTube Uploader:**
```bash
# Auto-detect (recommended)
py youtube_uploader.py --video AUTO --privacy public

# Manual path
py youtube_uploader.py --video "edited/MyVideo.mp4" --privacy unlisted
```

## Notes
- The script finds the **most recent** video by modification date
- Output filename automatically removes spaces and adds `_EDITED`
- Original video in `downloads/` is never modified
- YouTube uploader auto-detects metadata (.metadata.json) and subtitles (.srt)
