# 🎬 CapCut AI Video Automation + Professional Video Editor

**Complete end-to-end automation: CapCut AI video generation → Download → Professional editing → YouTube-ready videos**

## 📋 Project Overview

This system provides **fully automated video production pipeline** with zero manual intervention:

### **🎯 Core Capabilities:**

#### **Part 1: Video Generation (CapCut AI)**
1. **🔐 Session Management** - Proven browser sessions (login once, use forever)
2. **📝 Form Automation** - Auto-fills video descriptions and customizations
3. **🎬 Generation Monitoring** - Dynamic waiting with multi-tab support
4. **📤 Export Automation** - Downloads videos in 1080p @ 60fps
5. **📊 Batch Processing** - Handles multiple jobs from CSV/Google Sheets

#### **Part 2: Professional Video Editing (NEW!)**
6. **✂️ Silence Removal** - Cuts dead air automatically (-30dB threshold)
7. **⚡ Speed Optimization** - 1.2x speed for better pacing
8. **🎨 Color Grading** - Cinematic look (+20% saturation, +10% contrast, vignette)
9. **🔊 Audio Enhancement** - Broadcast-quality sound (normalization, compression, clarity)
10. **🎵 Background Music** - Professional blending with EQ and smooth fades
11. **🎬 Jump Cuts** - Removes awkward pauses automatically
12. **💾 Smart Caching** - Resumes interrupted processing, detects video changes

### **🚀 What Makes This Special:**
- **Zero Login Required** - Uses saved browser sessions
- **Complete Pipeline** - From text prompt to YouTube-ready video
- **Professional Quality** - Broadcast-grade audio/video processing
- **Intelligent Processing** - Smart caching, automatic video change detection
- **Production Ready** - Battle-tested workflow from start to finish

## 🚀 Current Status: **PRODUCTION READY**

### ✅ **Working Features:**
- ✅ **Proven session loading** (no login required)
- ✅ **Navigation to CapCut AI** (correct URL)
- ✅ **Popup handling** (Terms of Service, etc.)
- ✅ **Form filling** (video descriptions)
- ✅ **Customization settings** (aspect ratio, voice, style, duration)
- ✅ **Generate button clicking**
- ✅ **Dynamic generation waiting** (exits when Export appears)
- ✅ **Complete export process** (filename, 1080p, 60fps)

### 🔧 **Latest Updates (Oct 16, 2025):**

#### **Video Generation:**
- ✅ **GOOGLE SHEET UPDATE FIX** - Robust retry logic (3 attempts) with detailed logging
- ✅ **CASE-INSENSITIVE MATCHING** - Finds jobs even with different capitalization
- ✅ **AUTO-CREATE COLUMNS** - Creates 'uploaded' and 'video_generation' columns if missing
- ✅ **REMOVED BROKEN FEATURES** - Removed non-working resolution/framerate selection (uses CapCut defaults)
- ✅ **VIDEO DOWNLOADER MODULE** - Standalone download from My Cloud with proper .mp4 extension
- ✅ **PROPER FILENAME HANDLING** - Cleans filenames, removes "All-in-one video editor" suffix
- ✅ **DYNAMIC PAGE LOAD DETECTION** - Waits up to 45 seconds for Download button to appear
- ✅ **PLAYWRIGHT DOWNLOAD FIX** - Uses `expect_download()` for reliable file downloads
- ✅ **DUAL EXPORT BUTTON FIX** - Clicks top button (opens dialog) then bottom button (exports)
- ✅ **NEW TAB DETECTION** - Automatically switches to generation tab with `expect_page()`
- ✅ **Multi-tab support** - Handles CapCut opening new tabs/pages

#### **Video Editing (NEW!):**
- ✅ **AUTO VIDEO EDITOR** - Complete ffmpeg-based editing pipeline
- ✅ **SILENCE REMOVAL** - Uses ffmpeg silenceremove filter (works perfectly!)
- ✅ **COLOR GRADING** - Professional cinematic look with saturation, contrast, vignette
- ✅ **AUDIO ENHANCEMENT** - Loudness normalization, compression, clarity boost
- ✅ **BACKGROUND MUSIC** - Advanced EQ, compression, smooth fades (3 seconds)
- ✅ **SMART CACHING** - SHA256 checksum validation, auto-detects video changes
- ✅ **RESUME CAPABILITY** - Can resume interrupted processing
- ✅ **CHUNK PROCESSING** - Handles long videos efficiently

## 📁 Project Structure & Key Files

### **🎯 Core System (Essential):**
```
src/
├── main.py                 # 🎬 Main orchestrator (video creation & export)
├── video_downloader.py     # 📥 Download videos from My Cloud
├── proven_browser.py       # 🔐 Session management with Playwright
├── sheets_reader.py        # 📊 CSV/Google Sheets data loading
└── state_store.py          # 💾 Job state tracking and persistence

Root Directory:
├── auto_edit.py            # ✂️ Professional video editor (NEW!)
├── manifest.json           # ⚙️ Video editing configuration
└── manifest.example.json   # 📋 Example editing config
```

### **📋 Configuration:**
```
config/
├── selectors.json          # 🎯 CapCut UI element selectors
└── settings.json           # ⚙️ System configuration

sheets/
└── sample_input.csv        # 📝 Sample job data format

state/
└── proven_session.json     # 🍪 Saved browser session (auto-created)
```

### **🚀 Quick Start Scripts:**
```
TEST_FIXED_SYSTEM.bat       # 🧪 Test complete workflow (1 job)
RUN_MAIN_VISIBLE.bat        # 🎬 Run full automation (visible browser)
INSTALL_DEPS.bat            # 📦 Install all dependencies
```

### **📦 Dependencies:**
```
requirements.txt            # 📋 Python package requirements
install_deps.py             # 🔧 Automated dependency installer
.env                        # 🔐 Environment variables (create from template)
```

## 🎯 Complete Workflow Steps

### **Main Workflow (`src/main.py`):**
```
1. 🚀 Load proven session (39 cookies) → Navigate to CapCut AI
2. ❌ Close popups (Terms of Service, etc.)
3. 📝 Fill video description textarea
4. ⚙️ Set customizations:
   - Aspect ratio (16:9, 9:16, etc.)
   - Voice (Ms. Labebe, etc.)  
   - Style (Realistic Film, etc.)
   - Duration (1 min, etc.)
5. 🎬 Click Generate button
6. 🔄 **NEW TAB DETECTION** - Switch to generation page automatically
7. ⏳ Wait dynamically for completion (until Export button appears)
8. 📤 Export with settings:
   - Filename: Job title (max 45 chars)
   - Resolution: 1080p
   - Frame rate: 60fps
9. ⏳ **Wait 1 minute** for export to complete
10. 📥 **Download from My Cloud** (calls video_downloader.py)
```

### **Download Workflow (`src/video_downloader.py`):**
```
1. 🌐 Navigate to CapCut My Cloud page
2. 🚫 Close any popups/modals (Escape key + close buttons)
3. 📜 Scroll to "Exported videos" section
4. 🎬 Click first video thumbnail (uses expect_page() to catch new tab)
5. ⏳ Wait up to 45 seconds for page to load (dynamic detection)
6. 🆕 New tab opens with video details
7. ⬇️ Click "Download" button (uses expect_download())
8. 💾 Save video with proper .mp4 extension to downloads/ folder
9. 🧹 Clean filename (remove "All-in-one video editor" suffix)
```

### **Module Responsibilities:**
- **`main.py`** - Steps 1-9 (video creation & export) - 1,735 lines
- **`video_downloader.py`** - Step 10 (download from My Cloud) - 470 lines
- **`proven_browser.py`** - Session management (loads proven_session.json) - 152 lines
- **`sheets_reader.py`** - Load jobs from Google Sheets/CSV - 484 lines
- **`state_store.py`** - Track job progress and state - ~200 lines

### **Key Technical Details:**
- **Popup Handling**: Tries 11 different close button selectors + Escape key
- **New Tab Detection**: Uses `context.expect_page()` with 20s timeout
- **Download Handling**: Uses `page.expect_download()` (Playwright best practice)
- **Dynamic Waiting**: Polls for Download button every 1s up to 45s
- **Filename Cleaning**: Removes special chars, splits on " | " and " - "
- **Session Persistence**: Loads 39 cookies from `proven_session.json`

## 🚀 Quick Start

### **Prerequisites:**
```bash
# Install dependencies
py install_deps.py

# Or manually:
pip install numpy opencv-python pandas python-dotenv playwright
playwright install chromium
```

### **Run Complete Automation:**
```bash
# Full workflow (video creation + export + download)
py src/main.py --limit 1

# Or double-click:
TEST_FIXED_SYSTEM.bat
RUN_MAIN_VISIBLE.bat
```

### **Test Individual Components:**
```bash
# Test ONLY video download (standalone)
py src/video_downloader.py

# Or double-click:
TEST_DOWNLOAD_ONLY.bat

# Test browser session
py src/proven_browser.py
```

## 📊 Input Data Format

### **CSV Format (`sheets/sample_input.csv`):**
```csv
title,style,voice,duration,aspect_ratio
"environmental pollution Video",cinematic,female,1m30s,16:9
"Social Media Promo",casual,male,30s,9:16
```

### **Column Descriptions:**
- **`title`** - Video description/topic (max 45 chars for filename)
- **`style`** - Video style (cinematic, casual, documentary, etc.)
- **`voice`** - Narrator voice (female, male, Ms. Labebe, etc.)
- **`duration`** - Video length (30s, 1m, 1m30s, etc.)
- **`aspect_ratio`** - Video dimensions (16:9, 9:16, 1:1)

### **Google Sheets Integration:**
- Same columns as CSV format
- Configure sheet ID in `src/sheets_reader.py`
- Requires Google Sheets API credentials

## 🔧 Technical Architecture

### **🏗️ System Design:**
```
Input (CSV/Sheets) → Load Jobs → Browser Session → CapCut Automation → Export Videos
```

### **🧩 Core Components:**
- **`CapCutOrchestrator`** - Main workflow controller (simplified)
- **`ProvenBrowser`** - Session management with Playwright
- **`SheetsReader`** - CSV/Google Sheets data loading
- **`StateStore`** - Job state tracking and persistence

### **🎯 Key Features:**
- **Dual Export Button Handling** - Clicks top button → dialog → bottom button
- **Enhanced Dropdown Selection** - Actually clicks resolution/fps options
- **Multi-Tab Detection** - Automatically switches to generation tabs
- **Dynamic Generation Waiting** - Exits when Export button appears
- **Robust Error Handling** - Continues with next job on failures

### **Browser Strategy:**
- **Playwright** for main automation
- **Proven sessions** to avoid repeated logins
- **Multi-tab support** - Automatically switches to generation tabs
- **Visible browser** by default (headless optional)
- **Cookie-based authentication**

## 🐛 Debugging & Troubleshooting

### **Form Field Selection - How It Works:**

Understanding the 2-step selection process is critical for debugging form filling issues.

#### **🎨 Visual Style Selection (`_set_visual_style`)**

**Process:**
1. **Step 1: Open Dropdown** - Click the default style button (e.g., "Realistic Film")
   - Selectors tried: `text='Realistic Film'`, `div:has-text('Realistic Film')`, `span:has-text('Realistic Film')`
   - Wait: 1.5 seconds after click
   
2. **Step 2: Select Option** - Click the desired style from opened dropdown
   - Selectors tried: `text='{visual_style}'`, `span:has-text('{visual_style})'`, `:text('{visual_style}')`
   - Wait: 1 second after selection

**Example:**
```
Setting visual style to: Cartoon 3D
Step 1: Opening visual style dropdown...
  ✅ Clicked default style to open dropdown
Step 2: Selecting 'Cartoon 3D'...
  ✅ Found and clicked visual style: Cartoon 3D
```

**Debugging Tips:**
- If dropdown doesn't open: Check if "Realistic Film" text exists on page
- If option not found: Verify exact spelling/capitalization in Google Sheets
- Scrolling: Visual styles may require horizontal scrolling (not yet implemented)

---

#### **🎤 Voice Selection (`_set_voice`)**

**Process:**
1. **Step 1: Open Dropdown** - Click the default voice button (e.g., "Ms. Labebe" or "Lady Holiday")
   - Selectors tried: `text='Ms. Labebe'`, `text='Lady Holiday'`, `div:has-text('Ms. Labebe')`
   - Wait: 1.5 seconds after click
   
2. **Step 2: Select Option** - Click the desired voice from opened dropdown
   - Selectors tried: `text='{voice}'`, `div:has-text('{voice})'`, `:text('{voice}')`
   - Wait: 1 second after selection

**Example:**
```
Setting voice to: Nice Witch
Step 1: Opening voice dropdown...
  ✅ Clicked default voice to open dropdown
Step 2: Selecting 'Nice Witch'...
  ✅ Found and clicked voice: Nice Witch
```

**Debugging Tips:**
- If dropdown doesn't open: Check if "Ms. Labebe" or "Lady Holiday" exists
- If option not found: Voice may require vertical scrolling (see memory for scrolling implementation)
- No validation: Any voice name can be used (CapCut has many options)

---

#### **⏱️ Duration Selection (`_set_duration`)**

**Process:**
1. **Step 1: Open Dropdown** - Click the dropdown arrow OR default duration text
   - **Preferred**: Click `.lv-select-suffix-icon` (dropdown arrow)
   - **Fallback**: Click `text='1 min'`, `text='30s'`, or `.lv-select-view-value`
   - Wait: 1.5 seconds after click
   
2. **Step 2: Select Option** - Click the desired duration from opened dropdown
   - Selectors tried: `text='{duration}'`, `li:has-text('{duration})'`, `[role='option']:has-text('{duration}')`
   - Wait: 1 second after selection

**Format Conversion:**
- Input: `60` (seconds) → Converted to: `1 min`
- Input: `30` (seconds) → Converted to: `30s`
- Input: `"1 min"` → Used as-is

**Example:**
```
Setting duration to: 1 min
Step 1: Opening duration dropdown...
  ✅ Clicked dropdown arrow to open duration options
Step 2: Selecting '1 min'...
  ✅ Found duration element: 1 min
```

**Debugging Tips:**
- If arrow doesn't work: Fallback to clicking default duration text
- Common values: "30s", "1 min", "2 min", "3 min"
- Format matters: Use "1 min" not "1m" or "60s"

---

#### **📐 Aspect Ratio Selection (`_set_aspect_ratio`)**

**Process:**
1. **Step 1: Open Dropdown** - Click the default aspect ratio (e.g., "16:9")
   - Selectors tried: `text='16:9'`, `span:has-text('16:9')`, `.lv-select-view-value`
   - Wait: 1.5 seconds after click
   
2. **Step 2: Select Option** - Click the desired aspect ratio from opened dropdown
   - Selectors tried: `text='{aspect_ratio}'`, `span:has-text('{aspect_ratio})'`, `:text('{aspect_ratio}')`
   - Wait: 1 second after selection

**Example:**
```
Setting aspect ratio to: 9:16
Step 1: Opening aspect ratio dropdown...
  ✅ Clicked default ratio to open dropdown
Step 2: Selecting '9:16'...
  ✅ Found aspect ratio element: 9:16
```

**Debugging Tips:**
- Common values: "16:9" (landscape), "9:16" (portrait), "1:1" (square)
- Format matters: Use "16:9" not "16x9" or "widescreen"
- Usually visible without scrolling

---

#### **📝 Description/Title Input (`fill_capcut_form`)**

**Process:**
1. **Find Textarea** - Locate the description input field
   - Selectors tried: `.lv-textarea`, `textarea[placeholder*='Describe your video idea']`
   - Wait: 2 seconds after filling
   
2. **Fill Text** - Clear existing text and fill with job title
   - Method: `textarea.click()` → `textarea.fill("")` → `textarea.fill(job['title'])`

**Example:**
```
1️⃣ Looking for description textarea...
  Trying: .lv-textarea
  ✅ Found textarea with: .lv-textarea
  ✅ Filled with: environmental pollution Video
```

**Debugging Tips:**
- Selector `.lv-textarea` is most reliable (from capture test)
- Always clear before filling to avoid appending text
- Max length: 45 characters for filename (longer text is OK for description)

---

### **Common Form Filling Issues:**

#### **1. Dropdown Doesn't Open:**
- **Cause**: Default button text changed or not visible
- **Solution**: Check browser console, update selectors in `main.py`
- **Debug**: Add `time.sleep(5)` before dropdown click to inspect page manually

#### **2. Option Not Found in Dropdown:**
- **Cause**: Exact text mismatch or option requires scrolling
- **Solution**: 
  - Verify exact spelling in Google Sheets (case-sensitive)
  - Check if option requires scrolling (voice uses vertical scroll)
  - Use browser DevTools to inspect dropdown HTML

#### **3. Wrong Option Selected:**
- **Cause**: Multiple elements with same text
- **Solution**: Selectors use `.first` to click first match
- **Debug**: Check if dropdown is actually open before selecting

#### **4. Form Fills But Generate Fails:**
- **Cause**: CapCut validation error or missing required field
- **Solution**: Check CapCut UI for error messages
- **Debug**: Take screenshot before clicking Generate button

---

### **Common Issues & Solutions:**

#### **1. Download Issues:**
- **Problem**: Files download without .mp4 extension
  - **Solution**: Fixed! Now uses `page.expect_download()` + proper filename handling
  - **Location**: Files save to `C:\Users\2002\CascadeProjects\gg\downloads\`

- **Problem**: Files have "All-in-one video editor" in name
  - **Solution**: Fixed! Filename cleaning removes CapCut suffixes

- **Problem**: Download button not found
  - **Solution**: Dynamic wait up to 45 seconds, checks every 1 second

#### **2. New Tab/Page Issues:**
- **Problem**: "No new page opened" error
  - **Solution**: Now uses `context.expect_page()` with 20s timeout
  - **Waits**: Up to 15 seconds for tab to appear, then 45s for content

- **Problem**: Page loads slowly
  - **Solution**: Dynamic detection - waits for Download button visibility

#### **3. Session Issues:**
- **Problem**: "proven_session.json not found"
  - **Solution**: Ensure file exists in `state/` folder
  - **Contains**: 39 cookies from working CapCut login

#### **4. Module Import Errors:**
- **Problem**: "No module named 'playwright'"
  - **Solution**: Run `py install_deps.py` or `pip install playwright`
  - **Then**: Run `playwright install chromium`

### **Quick Reference Table:**

| Field | Step 1: Open Dropdown | Step 2: Select Option | Wait Time | Scrolling Needed? |
|-------|----------------------|----------------------|-----------|-------------------|
| **Visual Style** | Click "Realistic Film" | Click `text='{style}'` | 1.5s → 1s | Horizontal (not implemented) |
| **Voice** | Click "Ms. Labebe" | Click `text='{voice}'` | 1.5s → 1s | Vertical (5x 100px) |
| **Duration** | Click `.lv-select-suffix-icon` | Click `text='{duration}'` | 1.5s → 1s | No |
| **Aspect Ratio** | Click "16:9" | Click `text='{ratio}'` | 1.5s → 1s | No |
| **Description** | N/A (direct input) | Fill `.lv-textarea` | 2s | No |

**Key Selectors:**
- **Dropdown arrow**: `.lv-select-suffix-icon`
- **Dropdown value**: `.lv-select-view-value`
- **Textarea**: `.lv-textarea`
- **Text matching**: `text='exact text'` (Playwright syntax)

---

### **Debug Mode:**
```bash
# Dry run (no actual actions)
py src/main.py --dry-run --limit 1

# Visible browser (default)
py src/main.py --limit 1

# Headless mode
py src/main.py --headless --limit 1

# Test download only (standalone)
py src/video_downloader.py
```

### **Debug Screenshots:**
- **Location**: `downloads/debug_before_click.png`
- **Shows**: Page state before clicking video thumbnail
- **Use**: Check if videos are visible and selectors are correct

### **Selector Update Guide:**

If CapCut UI changes and selectors break:

1. **Open browser DevTools** (F12) while automation runs
2. **Inspect the element** you want to click
3. **Find unique identifier**: class, text content, aria-label, etc.
4. **Update selectors** in `src/main.py`:
   - Line 1482-1487: Visual style default button
   - Line 1508-1511: Visual style options
   - Line 1572-1576: Voice default button
   - Line 1597-1601: Voice options
   - Line 1674-1688: Duration dropdown
   - Line 1705-1709: Duration options
   - Line 1770-1774: Aspect ratio default button
   - Line 1794-1798: Aspect ratio options
5. **Test with visible browser** to verify changes work

## 📈 Performance & Scaling

### **Current Capacity:**
- **Single job**: ~3-6 minutes (including 1-minute download wait)
- **Batch processing**: Sequential (can be parallelized)
- **Session reuse**: No login delays between jobs
- **Multi-tab handling**: Automatic tab switching for generation pages

### **Optimization Opportunities:**
- Parallel job processing
- Multiple browser contexts
- Faster element detection
- Video generation time prediction

## 🔐 Security & Session Management

### **Session Files:**
- **`state/proven_session.json`** - Contains login cookies (keep secure)
- **`.env`** - Environment variables (not in git)
- **`state/job_states.json`** - Job progress tracking

### **Best Practices:**
- Keep session files private
- Regenerate sessions periodically
- Monitor for CapCut UI changes

## 🚧 Development Status

### **Current Phase: PRODUCTION READY** ✅
- Complete workflow implemented
- All major bugs fixed
- Export automation working
- Dynamic generation waiting implemented
- **Multi-tab support** - Handles CapCut's new tab behavior
- **Download waiting** - Ensures videos download completely

### **Next Enhancements:**
- Parallel job processing
- Better error recovery
- UI change detection
- Performance optimization

## 📞 Support & Maintenance

### **When CapCut UI Changes:**
1. Update `config/selectors.json` with new selectors
2. Test with `py src/main.py --dry-run --limit 1`
3. Check browser console for element changes

### **Session Renewal:**
1. Delete `state/proven_session.json`
2. Run login process to create new session
3. Test with automation

## 🧹 Project Cleanup

### **Unnecessary Files to Remove:**
Run `CLEANUP_UNNECESSARY_FILES.bat` to remove:
- ❌ `FIXED_proven_solution.py` (old solution, replaced by `proven_browser.py`)
- ❌ `test_full_system.py` (replaced by `TEST_FIXED_SYSTEM.bat`)
- ❌ `INTEGRATION_COMPLETE.md` (outdated documentation)
- ❌ Old batch files (`RUN_FIXED.bat`, `TEST_FORM_FILL.bat`, etc.)
- ❌ Empty folders (`__pycache__`, `tests`, `.venv`, `.github`)

### **Essential Files Only:**
After cleanup, you'll have a clean project with only working components:
```
📁 CapCut Automation (Clean & Simplified)
├── 📁 src/
│   ├── main.py             # 🎬 Main orchestrator (1,735 lines)
│   ├── video_downloader.py # 📥 Download from My Cloud (470 lines)
│   ├── proven_browser.py   # 🔐 Session management (152 lines)
│   ├── sheets_reader.py    # 📊 CSV/Google Sheets data loading (484 lines)
│   └── state_store.py      # 💾 Job state tracking (~200 lines)
├── 📁 config/
│   ├── selectors.json      # 🎯 CapCut UI element selectors
│   └── settings.json       # ⚙️ System configuration
├── 📁 sheets/
│   └── sample_input.csv    # 📝 Sample job data
├── 📁 downloads/           # 📥 Downloaded videos (auto-created)
│   └── *.mp4              # Videos with proper .mp4 extension
├── 📁 state/               # 🍪 Auto-created session storage
├── TEST_FIXED_SYSTEM.bat   # 🧪 Main test script
├── RUN_MAIN_VISIBLE.bat    # 🎬 Main run script
├── INSTALL_DEPS.bat        # 📦 Dependency installer
├── requirements.txt        # 📋 Python dependencies
├── .env                    # 🔐 Environment variables
└── README.md               # 📖 This documentation
```

**Total: Only 13 essential files + 4 folders = Ultra-clean project!**

## 📥 Output & Downloaded Videos

### **Download Location:**
```
C:\Users\2002\CascadeProjects\gg\downloads\
```

### **File Format:**
- **Extension**: `.mp4` (proper video format)
- **Naming**: Clean filenames (e.g., "Environmental Pollution Video.mp4")
- **Quality**: 1080p @ 60fps (as set in export settings)
- **Size**: ~40-50 MB per minute of video

### **Filename Cleaning:**
- Removes "All-in-one video editor" suffix
- Removes "CapCut" branding
- Splits on " | " and " - " separators
- Removes special characters (keeps alphanumeric, spaces, hyphens, underscores)

### **Accessing Downloads:**
```bash
# Open downloads folder
explorer C:\Users\2002\CascadeProjects\gg\downloads

# Or from project root
cd downloads
dir *.mp4
```

## 🎯 Development Workflow

### **For New Users:**
1. **Setup**: Run `INSTALL_DEPS.bat`
2. **Test**: Run `TEST_FIXED_SYSTEM.bat` (1 job)
3. **Production**: Run `RUN_MAIN_VISIBLE.bat` (all jobs)

### **For Developers:**
1. **Understand**: Read this README completely
2. **Explore**: Check `src/main.py` (simplified 1,200 lines)
3. **Customize**: Modify `sheets/sample_input.csv` with your data
4. **Debug**: Use `--dry-run` flag for testing

---

## 🎬 Video Editing Pipeline (NEW!)

### **Overview**
After videos are generated and downloaded, the **Auto Video Editor** (`auto_edit.py`) transforms raw videos into engaging YouTube content with professional-grade effects using **ffmpeg**.

### **Core Features (Always Applied):**

#### **1. Silence Removal** ✂️
- **Method:** ffmpeg `silenceremove` filter
- **Threshold:** -30dB (configurable)
- **Duration:** 0.3 seconds minimum
- **Result:** Removes dead air, tighter editing

#### **2. Speed Optimization** ⚡
- **Speed:** 1.2x (20% faster)
- **Audio:** Pitch-corrected (no chipmunk voice)
- **Result:** Better pacing, keeps viewers engaged

#### **3. Jump Cuts** 🎬
- **Method:** Scene detection + smart cutting
- **Threshold:** 0.3 seconds
- **Result:** Removes awkward pauses between sentences

#### **4. Color Grading** 🎨
- **Saturation:** +20% (more vibrant)
- **Contrast:** +10% (punchier image)
- **Brightness:** +2% (slightly brighter)
- **Vignette:** Darkens edges, focuses center
- **Sharpening:** Professional crisp look
- **Result:** Cinematic, eye-catching appearance

#### **5. Audio Enhancement** 🔊
- **Loudness normalization:** -16 LUFS (YouTube standard)
- **Compression:** 4:1 ratio for consistency
- **Presence boost:** +2dB at 3kHz (clearer voice)
- **Bitrate:** 192k AAC
- **Result:** Broadcast-quality professional sound

#### **6. Background Music** 🎵
- **EQ Processing:**
  - High-pass filter (80Hz) - Removes rumble
  - Low-pass filter (10kHz) - Removes harshness
  - Reduce highs (8kHz: -4dB) - Smooth sound
  - Boost low-mids (250Hz: +2dB) - Warmth
  - Reduce mid-highs (4kHz: -2dB) - Space for voice
- **Compression:** Smooths volume peaks
- **Fade:** 3-second exponential fade in/out
- **Volume:** 12% (configurable, voice always clear)
- **Result:** Professional blend, music enhances without overpowering

#### **7. Subtitle Extraction** 📝
- **Method:** Whisper AI (OpenAI, free & local)
- **Model:** Base model (74MB, cached after first run)
- **Output:** .srt file (for YouTube subtitles)
- **Transcript:** .txt file (for AI metadata generation)
- **Processing:** ~30-60 seconds for 2-minute video
- **Result:** Professional subtitles, accessibility, better SEO

#### **8. AI Metadata Generation** 🤖
- **API:** OpenRouter DeepSeek (fast & cheap, ~$0.001/video)
- **Generates:**
  - YouTube title (max 60 chars, SEO-optimized)
  - Description (2-3 paragraphs, keyword-rich)
  - 25 relevant tags (broad + specific keywords)
  - 10 trending hashtags (with # symbol)
- **Output:** .metadata.json file
- **Processing:** ~5-10 seconds
- **Result:** Ready-to-use YouTube metadata

#### **9. Smart Caching** 💾
- **Checksum validation:** SHA256 hash of input video
- **Auto-detection:** Detects when video changes
- **Resume capability:** Can resume interrupted processing
- **Result:** Fast re-runs, safe video changes

### **Quick Start - Video Editing**

#### **🚀 Simple Method (Auto-Detection - Recommended):**
```bash
# 1. Put your video in downloads/ folder
# 2. Run the batch file
edit_video.bat

# That's it! The system will:
# - Auto-detect the latest video in downloads/
# - Update manifest.json automatically
# - Process the video
# - Save results to edited/ folder
```

#### **⚙️ Advanced Method (Manual Configuration):**
```bash
# 1. Ensure ffmpeg is installed (required)
ffmpeg -version

# 2. Edit manifest.json with your video path
# "input_video": "downloads/YourVideo.mp4"
# "output_video": "edited/YourVideo_EDITED.mp4"

# 3. Run the editor
py auto_edit.py --manifest manifest.json --work-dir work

# Output will be in edited/ folder
```

**✨ Auto-Detection Features:**
- ✅ No manual editing required
- ✅ Works with any video filename
- ✅ Automatically finds latest video
- ✅ Generates clean output filenames
- ✅ See `AUTO_DETECT_VIDEO.md` for details

### **Processing Time**
- **2-minute video:** ~3-4 minutes
- **5-minute video:** ~8-10 minutes
- **Re-run same video:** ~5 seconds (uses cache)
- **Different video:** Auto-detects, processes fresh

### **Manifest Configuration**

Create a JSON manifest to configure editing:

```json
{
  "input_video": "downloads/Environmental_Pollution_Video.mp4",
  "output_video": "edited/Environmental_Pollution_Video_EDITED.mp4",
  
  "speed_multiplier": 1.20,
  
  "remove_silence": true,
  "silence_threshold": -30.0,
  "silence_duration": 0.3,
  
  "jump_cut_threshold": 0.3,
  
  "apply_transitions": true,
  "apply_zoom_effects": false,
  "add_sound_effects": true,
  "add_subtitles": false,
  "add_subscribe_popup": false,
  
  "background_music": "background.mp3",
  "background_music_volume": 0.12,
  
  "extract_subtitles": true,
  "generate_metadata": true,
  "openrouter_api_key": "sk-or-v1-your-api-key-here",
  
  "chunk_duration": 300,
  "max_workers": 2
}
```

**Key Settings:**
- `speed_multiplier`: 1.0 = normal, 1.2 = 20% faster (recommended)
- `silence_threshold`: -30dB = aggressive, -40dB = moderate
- `silence_duration`: Minimum silence length to remove (seconds)
- `apply_transitions`: Color grading, vignette, sharpening
- `apply_zoom_effects`: Dynamic zoom (disabled for static videos)
- `add_sound_effects`: Audio enhancement (loudness, compression, clarity)
- `background_music_volume`: 0.12 = 12% volume (good for continuous speech)
- `extract_subtitles`: true = Extract subtitles with Whisper AI
- `generate_metadata`: true = Generate YouTube metadata with DeepSeek AI
- `openrouter_api_key`: Your OpenRouter API key (get from https://openrouter.ai/)

### **Before & After Example**

**Original Video (78 seconds, 41 MB):**
- Dead air and pauses
- Normal speed
- Flat colors
- Inconsistent audio
- No subtitles
- No metadata

**Edited Video (64 seconds, 7 MB) + AI Assets:**
- ✅ 18% shorter (silence removed + 1.2x speed)
- ✅ 82% smaller file size
- ✅ Vibrant cinematic colors
- ✅ Professional broadcast audio
- ✅ Background music with smooth blending
- ✅ **Auto-generated subtitles (.srt)**
- ✅ **AI-generated metadata (title, description, 25 tags, 10 hashtags)**
- ✅ YouTube-ready quality

### **Documentation**

See these files for detailed information:
- `HOW_IT_WORKS.md` - Smart caching system explained
- `BACKGROUND_MUSIC_EXPLAINED.md` - Music processing details
- `AI_FEATURES_GUIDE.md` - Subtitle extraction & AI metadata generation
- `GITHUB_ACTIONS_OPTIMIZATION.md` - GitHub Actions optimization guide
- `ASSETS_NEEDED.md` - Optional assets guide (subtitles, subscribe button)

### **Chunked Processing**

The editor processes videos in chunks for efficiency:
- **Default chunk size**: 5 minutes (300 seconds)
- **Resumable**: Can resume from last checkpoint
- **Smart caching**: SHA256 checksum validation
- **Auto-detection**: Detects when video changes
- **Result**: Fast re-runs, safe processing
├── subscribe_sound.mp3    # Sound effect for popup
└── sound_effects/         # Various sound effects
    ├── whoosh.mp3
    ├── pop.mp3
    └── transition.mp3

background_music.mp3       # Background music track
```

### **Output Structure**

```
downloads/                 # Generated videos from CapCut
├── Video1.mp4
└── Video2.mp4

edited/                    # Edited videos ready for upload
├── Video1_EDITED.mp4
└── Video2_EDITED.mp4

work/                      # Working directory (can be deleted)
├── chunks/                # Video chunks during processing
├── temp/                  # Temporary files
└── edit_state.json        # Resume state
```

### **Troubleshooting**

**Issue**: `auto-editor` not found
```bash
pip install auto-editor
```

**Issue**: `scenedetect` not found
```bash
pip install scenedetect[opencv]
```

**Issue**: MoviePy errors
```bash
pip install moviepy --upgrade
```

**Issue**: FFmpeg not found
- **Windows**: Download from https://ffmpeg.org/download.html
- **Linux**: `sudo apt-get install ffmpeg`
- **Mac**: `brew install ffmpeg`

**Issue**: Out of memory during processing
- Reduce `chunk_duration` in manifest (e.g., 180 seconds)
- Process fewer effects at once
- Close other applications

### **Performance Tips**

1. **Chunk size**: Smaller chunks (180s) for slower machines
2. **Disable effects**: Turn off zoom/transitions for faster processing
3. **Use SSD**: Store work directory on SSD for better I/O
4. **Parallel processing**: Set `max_workers: 2` for dual-core CPUs

---

---

## 📤 YouTube Upload System (Part 3)

### **Overview**
After videos are edited, the **YouTube Uploader** (`youtube_uploader.py`) automatically uploads videos to YouTube with AI-generated metadata, subtitles, and SEO optimization.

### **Key Features:**

#### **1. Automated Upload** 🚀
- **Auto-detection:** Finds .mp4, .metadata.json, and .srt files automatically
- **Metadata integration:** Uses AI-generated title, description, tags, hashtags
- **Subtitle upload:** Automatically uploads .srt captions (English)
- **Privacy control:** Public/Unlisted/Private (default: public)
- **Resume support:** Uses refresh tokens (no browser needed after first auth)

#### **2. AI Metadata Integration** 🤖
- **Title:** SEO-optimized, max 60 characters
- **Description:** 2-3 paragraphs with keywords + hashtags appended
- **Tags:** 25 relevant tags for maximum reach
- **Hashtags:** 10 trending hashtags added to description
- **Category:** Configurable (default: People & Blogs)

#### **3. Authentication System** 🔐
- **First time:** Browser opens → Sign in → Grant permissions → Token saved
- **Subsequent uploads:** Uses refresh token (no browser needed)
- **Token lifetime:** 6+ months (auto-renews when used)
- **GitHub Actions:** Works in CI/CD with secrets

### **Setup Instructions**

#### **Step 1: Get YouTube API Credentials**

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create new project: "YouTube Video Uploader"
3. Enable **YouTube Data API v3**
4. Create **OAuth 2.0 Client ID** (Desktop app)
5. Download JSON → Save as `youtube_credentials.json`
6. Move to project root: `C:\Users\2002\CascadeProjects\gg\`

#### **Step 2: Install Dependencies**

```bash
# Option A: Use batch file
INSTALL_YOUTUBE_DEPS.bat

# Option B: Command line
py -m pip install google-auth google-auth-oauthlib google-auth-httplib2 google-api-python-client
```

#### **Step 3: First Upload (Authentication)**

```bash
# Upload video (browser will open for first-time auth)
py youtube_uploader.py --video "edited/YourVideo_EDITED.mp4" --privacy public

# Or use batch file
upload_to_youtube.bat
```

**What happens:**
1. Browser opens automatically
2. Sign in with your YouTube/Google account
3. Click "Continue" (ignore "unverified app" warning - it's your own app)
4. Grant permissions to upload videos
5. Token saved to `youtube_token.json` for future uploads
6. Video uploads with metadata and subtitles

#### **Step 4: Subsequent Uploads (No Browser)**

```bash
# All future uploads use saved token (no browser needed)
py youtube_uploader.py --video "edited/AnotherVideo_EDITED.mp4"
```

### **Usage Examples**

```bash
# Upload as public (default)
py youtube_uploader.py --video "edited/MyVideo_EDITED.mp4"

# Upload as unlisted
py youtube_uploader.py --video "edited/MyVideo_EDITED.mp4" --privacy unlisted

# Upload as private
py youtube_uploader.py --video "edited/MyVideo_EDITED.mp4" --privacy private

# Custom category (Science & Technology)
py youtube_uploader.py --video "edited/MyVideo_EDITED.mp4" --category 28

# Manual metadata/subtitles
py youtube_uploader.py --video "edited/MyVideo.mp4" --metadata "custom.json" --subtitles "custom.srt"
```

### **What Gets Uploaded**

From your `edited/` folder:

1. **Video:** `YourVideo_EDITED.mp4` (1080p, edited)
2. **Metadata:** `YourVideo_EDITED.metadata.json`
   - Title: "Save Our Planet: Small Changes, Big Impact!"
   - Description: AI-generated SEO-optimized description
   - Tags: 25 relevant tags
   - Hashtags: 10 trending hashtags (appended to description)
3. **Subtitles:** `YourVideo_EDITED.srt` (English captions)

**Example uploaded description:**
```
Ever feel like the air isn't as fresh as it used to be, or the rivers don't seem as clear? You're not just imagining it. Our beautiful planet is facing a serious challenge—pollution...

#SaveOurPlanet #EcoFriendly #Sustainability #ClimateAction #GoGreen #ZeroWaste #ProtectOurPlanet #GreenLiving #EarthDay #CleanEarth
```

### **GitHub Actions Integration**

#### **Setup for CI/CD:**

1. **Authenticate locally once:**
   ```bash
   py youtube_uploader.py --video "edited/test.mp4"
   ```
   This creates `youtube_token.json`

2. **Add GitHub Secrets:**
   - Go to: Repository → Settings → Secrets → Actions
   - Add `YOUTUBE_CREDENTIALS` = contents of `youtube_credentials.json`
   - Add `YOUTUBE_TOKEN` = contents of `youtube_token.json`

3. **Run workflow:**
   - Go to: Actions → Upload to YouTube
   - Click: Run workflow
   - Enter: Video filename and privacy setting
   - Video uploads automatically (no browser needed)

#### **Workflow file:** `.github/workflows/upload_youtube.yml`

```yaml
name: Upload to YouTube

on:
  workflow_dispatch:
    inputs:
      video_file:
        description: 'Video filename in edited/ folder'
        required: true
        default: 'Environmental_Pollution_Video_EDITED.mp4'
      privacy:
        description: 'Privacy setting'
        required: true
        default: 'public'
        type: choice
        options:
          - public
          - unlisted
          - private
```

### **Token Management**

#### **Access Token:**
- **Expires:** 1 hour
- **Auto-refreshed:** Yes, using refresh token
- **Action needed:** None

#### **Refresh Token:**
- **Expires:** 6 months (if not used) OR never (if used regularly)
- **Auto-renewed:** Yes, when used
- **Action needed:** Re-authenticate locally if expired

#### **When to Re-authenticate:**

You'll need to re-authenticate if:
1. 6+ months of inactivity (refresh token expires)
2. Revoked access manually in Google account
3. Changed password on Google account
4. Error: "invalid_grant" or "Token has been expired or revoked"

**Solution:**
```bash
# Delete old token
del youtube_token.json

# Re-authenticate (browser will open)
py youtube_uploader.py --video "edited/test.mp4"

# Update GitHub Secret if using Actions
```

### **YouTube Category IDs**

- `1` = Film & Animation
- `2` = Autos & Vehicles
- `10` = Music
- `15` = Pets & Animals
- `17` = Sports
- `19` = Travel & Events
- `20` = Gaming
- `22` = People & Blogs (default)
- `23` = Comedy
- `24` = Entertainment
- `25` = News & Politics
- `26` = Howto & Style
- `27` = Education
- `28` = Science & Technology

### **File Structure**

```
gg/
├── youtube_credentials.json    # YouTube API credentials (from Google Cloud)
├── youtube_token.json          # Auto-generated after first login
├── youtube_uploader.py         # Upload script
├── upload_to_youtube.bat       # Quick upload batch file
├── INSTALL_YOUTUBE_DEPS.bat    # Dependency installer
├── YOUTUBE_SETUP.md            # Detailed setup guide
├── GITHUB_ACTIONS_YOUTUBE.md   # CI/CD integration guide
└── edited/
    ├── YourVideo_EDITED.mp4
    ├── YourVideo_EDITED.metadata.json
    ├── YourVideo_EDITED.srt
    └── YourVideo_EDITED.txt
```

### **Troubleshooting**

#### **"Credentials file not found"**
- Download from: https://console.cloud.google.com/apis/credentials
- Save as `youtube_credentials.json` in project root

#### **"YouTube Data API v3 has not been used"**
- Enable API: https://console.cloud.google.com/apis/library/youtube.googleapis.com

#### **"Access blocked: This app's request is invalid"**
- Configure OAuth consent screen
- Add your email as test user

#### **"Quota exceeded"**
- YouTube API has daily quota (10,000 units/day)
- Each upload = ~1,600 units
- You can upload ~6 videos/day
- Quota resets at midnight Pacific Time

#### **"Subtitle upload failed: insufficientPermissions"**
- Delete `youtube_token.json`
- Re-authenticate to grant caption permissions
- New scope: `youtube.force-ssl` (for captions)

### **Security Notes**

- **Never commit** `youtube_credentials.json` or `youtube_token.json` to git
- Keep credentials secure and private
- Revoke access anytime: https://myaccount.google.com/permissions
- Use GitHub Secrets for CI/CD (encrypted storage)

### **Default Settings**

- **Privacy:** Public (ready for viewers)
- **Hashtags:** Automatically appended to description
- **Subtitles:** Auto-uploaded if .srt file exists
- **Category:** People & Blogs (22)
- **Made for Kids:** No (default)

### **Documentation Files**

- `YOUTUBE_SETUP.md` - Complete setup guide with screenshots
- `GITHUB_ACTIONS_YOUTUBE.md` - CI/CD integration guide
- `youtube_credentials.example.json` - Template for credentials

---

## 📝 Version History

### **v3.1 (Oct 16, 2025)** - YouTube Upload System
- ✅ Automated YouTube upload with API integration
- ✅ AI metadata integration (title, description, 25 tags, 10 hashtags)
- ✅ Automatic subtitle upload (.srt captions)
- ✅ OAuth 2.0 authentication with refresh tokens
- ✅ GitHub Actions support (CI/CD ready)
- ✅ Public/Unlisted/Private privacy control
- ✅ Token auto-refresh (6+ month lifetime)
- ✅ Hashtags appended to description automatically

### **v3.0 (Oct 15-16, 2025)** - Professional Video Editor + AI Features
- ✅ Complete video editing pipeline with ffmpeg
- ✅ Silence removal using silenceremove filter
- ✅ Color grading (saturation, contrast, vignette, sharpening)
- ✅ Audio enhancement (normalization, compression, clarity)
- ✅ Background music with advanced EQ and smooth fades
- ✅ Whisper AI subtitle extraction (.srt output)
- ✅ DeepSeek AI metadata generation (title, description, tags, hashtags)
- ✅ Smart caching with SHA256 checksum validation
- ✅ Resume capability for interrupted processing
- ✅ Auto video change detection

### **v2.1 (Oct 15, 2025)** - Video Downloader
- ✅ Standalone video downloader module
- ✅ Proper .mp4 file extension handling
- ✅ Dynamic page load detection (up to 45s)
- ✅ Filename cleaning (removes CapCut branding)
- ✅ Enhanced dropdown selection
- ✅ Multi-tab detection
- ✅ Simplified codebase (removed 300+ lines)

### **v2.0 (Oct 12, 2025)** - Simplified & Enhanced
- ✅ Dual export button fix
- ✅ Dynamic generation waiting
- ✅ Robust error handling

---

**Last Updated:** October 16, 2025  
**Status:** Production Ready - Complete End-to-End Pipeline (Generation + Editing + Upload)  
**Version:** 3.1 (YouTube Upload System Added)  
**Next Review:** When CapCut updates their interface

---

## 🎯 Complete Pipeline Summary

### **Full Workflow (All 3 Parts):**

```
1. Video Generation (CapCut AI)
   ↓
   Input: Google Sheets/CSV with video prompts
   Process: Browser automation → CapCut AI generation
   Output: Raw MP4 videos in downloads/
   Time: ~3-6 minutes per video

2. Video Editing (FFmpeg + AI)
   ↓
   Input: Raw videos from downloads/
   Process: Silence removal, color grading, audio enhancement, background music
   AI: Whisper subtitle extraction + DeepSeek metadata generation
   Output: Edited MP4 + .srt + .metadata.json + .txt in edited/
   Time: ~3-4 minutes per 2-minute video

3. YouTube Upload (YouTube API)
   ↓
   Input: Edited videos from edited/
   Process: OAuth authentication → Upload with metadata + subtitles
   Output: Published YouTube video (public/unlisted/private)
   Time: ~10-30 seconds per video
```

### **Key Files to Understand:**

#### **Part 1: Video Generation**
- `src/main.py` - Main orchestrator (1,750 lines)
- `src/video_downloader.py` - Download handler (534 lines)
- `src/proven_browser.py` - Session manager (152 lines)
- `config/settings.json` - System configuration
- `config/selectors.json` - CapCut UI selectors

#### **Part 2: Video Editing**
- `auto_edit.py` - Video editor (911 lines)
- `manifest.json` - Editing configuration
- `background.mp3` - Background music track
- `HOW_IT_WORKS.md` - Smart caching explained
- `BACKGROUND_MUSIC_EXPLAINED.md` - Music processing details

#### **Part 3: YouTube Upload**
- `youtube_uploader.py` - Upload script (310 lines)
- `youtube_credentials.json` - API credentials (from Google Cloud)
- `youtube_token.json` - Auth token (auto-generated)
- `upload_to_youtube.bat` - Quick upload script
- `YOUTUBE_SETUP.md` - Complete setup guide
- `GITHUB_ACTIONS_YOUTUBE.md` - CI/CD integration guide
- `.github/workflows/upload_youtube.yml` - GitHub Actions workflow



### **Output Files:**

```
downloads/
└── Environmental_Pollution_Video.mp4          # Raw generated video

edited/
├── Environmental_Pollution_Video_EDITED.mp4   # Edited video (YouTube-ready)
├── Environmental_Pollution_Video_EDITED.srt   # Subtitles (English)
├── Environmental_Pollution_Video_EDITED.txt   # Full transcript
└── Environmental_Pollution_Video_EDITED.metadata.json  # YouTube metadata
```




## 📚 Documentation Index

### **Setup Guides:**
- `README.md` - This file (complete overview)
- `YOUTUBE_SETUP.md` - YouTube API setup guide
- `GITHUB_ACTIONS_YOUTUBE.md` - CI/CD integration
- `SETUP_COMPLETE.md` - Initial setup checklist

### **Technical Documentation:**
- `HOW_IT_WORKS.md` - Smart caching system
- `BACKGROUND_MUSIC_EXPLAINED.md` - Music processing
- `ASSETS_NEEDED.md` - Optional assets guide
- `QUICK_START_EDITING.md` - Video editing quick start

### **Configuration Files:**
- `manifest.json` - Video editing settings
- `config/settings.json` - System configuration
- `config/selectors.json` - CapCut UI selectors
- `.env` - Environment variables

### **Batch Scripts:**
- `TEST_FIXED_SYSTEM.bat` - Test video generation
- `edit_video.bat` - Run video editor
- `upload_to_youtube.bat` - Upload to YouTube
- `INSTALL_DEPS.bat` - Install dependencies
- `INSTALL_YOUTUBE_DEPS.bat` - Install YouTube API deps