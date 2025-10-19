# GitHub Actions Setup Guide

## 🎯 Overview

This guide will help you set up the complete video production pipeline to run automatically in GitHub Actions.

---

## 📋 Prerequisites

Before setting up GitHub Actions, ensure you have:

1. ✅ **Working local pipeline** - Test `RUN_FULL_PIPELINE.bat` locally first
2. ✅ **GitHub repository** - Push your code to GitHub (public or private)
3. ✅ **CapCut session** - Valid `state/proven_session.json` file
4. ✅ **YouTube credentials** - `youtube_credentials.json` and `youtube_token.json`
5. ✅ **Google Sheets credentials** - `google_credentials.json` (if using Sheets)
6. ✅ **OpenRouter API key** - For DeepSeek AI metadata generation

---

## 🔐 Step 1: Create GitHub Secrets

GitHub Secrets store sensitive data securely. **Never commit credentials to your repository!**

### Navigate to Secrets:
1. Go to your GitHub repository
2. Click **Settings** → **Secrets and variables** → **Actions**
3. Click **New repository secret**

### Create These Secrets:

#### **1. PROVEN_SESSION**
```bash
# Copy content from: state/proven_session.json
# This contains your CapCut login cookies
```
- **Name:** `PROVEN_SESSION`
- **Value:** Entire content of `state/proven_session.json` file

#### **2. YOUTUBE_CREDENTIALS**
```bash
# Copy content from: youtube_credentials.json
# OAuth 2.0 credentials from Google Cloud Console
```
- **Name:** `YOUTUBE_CREDENTIALS`
- **Value:** Entire content of `youtube_credentials.json` file

#### **3. YOUTUBE_TOKEN**
```bash
# Copy content from: youtube_token.json
# Access token (generated after first local upload)
```
- **Name:** `YOUTUBE_TOKEN`
- **Value:** Entire content of `youtube_token.json` file

#### **4. GOOGLE_CREDENTIALS**
```bash
# Copy content from: google_credentials.json
# Google Sheets API credentials
```
- **Name:** `GOOGLE_CREDENTIALS`
- **Value:** Entire content of `google_credentials.json` file

#### **5. OPENROUTER_API_KEY**
```bash
# Your OpenRouter API key for DeepSeek AI
# Get from: https://openrouter.ai/
```
- **Name:** `OPENROUTER_API_KEY`
- **Value:** `sk-or-v1-xxxxxxxxxxxxx`

#### **6. GOOGLE_SHEETS_ID**
```bash
# Your Google Sheets ID (from the spreadsheet URL)
# Example: 1CJMBuqpD1s05mLY4Yw4FANKVe-fDLhsCQA9Gv70O1TM
```
- **Name:** `GOOGLE_SHEETS_ID`
- **Value:** `1CJMBuqpD1s05mLY4Yw4FANKVe-fDLhsCQA9Gv70O1TM`

#### **7. GOOGLE_SHEET_NAME**
```bash
# The name of the sheet tab (usually "Sheet1")
```
- **Name:** `GOOGLE_SHEET_NAME`
- **Value:** `Sheet1`

---

## 📁 Step 2: Prepare Repository

### Files to Commit:
```bash
✅ src/                    # All source code
✅ config/                 # Configuration files
✅ .github/workflows/      # GitHub Actions workflow
✅ auto_edit.py            # Video editor
✅ youtube_uploader.py     # YouTube uploader
✅ run_full_pipeline.py    # Pipeline orchestrator
✅ requirements.txt        # Python dependencies
✅ manifest.json           # Editor configuration
✅ background.mp3          # Background music (if using)
✅ README.md               # Documentation
✅ .gitignore              # Ignore sensitive files
```

### Files to NEVER Commit (already in .gitignore):
```bash
❌ state/proven_session.json     # CapCut session (use secret)
❌ youtube_credentials.json      # YouTube OAuth (use secret)
❌ youtube_token.json            # YouTube token (use secret)
❌ google_credentials.json       # Google API (use secret)
❌ .env                          # Environment variables
❌ downloads/                    # Generated videos
❌ edited/                       # Edited videos
❌ work/                         # Temporary files
```

### Commit and Push:
```bash
git add .
git commit -m "Setup GitHub Actions pipeline"
git push origin main
```

---

## 🚀 Step 3: Run the Pipeline

### Method 1: Manual Trigger (Recommended for Testing)

1. Go to your GitHub repository
2. Click **Actions** tab
3. Click **Full Video Production Pipeline** workflow
4. Click **Run workflow** button
5. Select privacy setting (public/unlisted/private)
6. Click **Run workflow**

### Method 2: Scheduled Run (Automatic)

The workflow is configured to run daily at 2 AM UTC:
```yaml
schedule:
  - cron: '0 2 * * *'  # Daily at 2 AM UTC
```

To change the schedule, edit `.github/workflows/full_pipeline.yml`:
```yaml
# Every 6 hours
- cron: '0 */6 * * *'

# Every Monday at 9 AM
- cron: '0 9 * * 1'

# Twice daily (6 AM and 6 PM)
- cron: '0 6,18 * * *'
```

### Method 3: Trigger on Push (Optional)

Uncomment these lines in `.github/workflows/full_pipeline.yml`:
```yaml
push:
  branches: [ main ]
```

---

## 📊 Step 4: Monitor Execution

### View Workflow Run:
1. Go to **Actions** tab
2. Click on the running workflow
3. Watch real-time logs for each step

### Workflow Steps:
```
1. ✅ Checkout repository
2. ✅ Set up Python 3.11
3. ✅ Install system dependencies (FFmpeg, etc.)
4. ✅ Install Python packages
5. ✅ Install Playwright + Chromium
6. ✅ Create directories
7. ✅ Setup credentials from secrets
8. ✅ Run full pipeline
   ├── Video Generation (CapCut AI - headless)
   ├── Video Editing (FFmpeg + AI)
   └── YouTube Upload
9. ✅ Upload artifacts
10. ✅ Cleanup sensitive files
```

### Expected Duration:
- **Video Generation:** 3-6 minutes
- **Video Editing:** 3-5 minutes
- **YouTube Upload:** 10-30 seconds
- **Total:** ~7-12 minutes per video

---

## 📦 Step 5: Download Artifacts

After the workflow completes, you can download the generated files:

### Available Artifacts:
1. **raw-video-XXX** - Original video from CapCut (7 days retention)
2. **edited-video-XXX** - Edited video + subtitles + metadata (30 days retention)
3. **pipeline-logs-XXX** - Execution logs (7 days retention)

### Download Steps:
1. Go to workflow run page
2. Scroll to **Artifacts** section
3. Click artifact name to download

---

## 🔧 Troubleshooting

### Issue 1: "PROVEN_SESSION secret not found"
**Solution:** Make sure you created all 5 required secrets in Step 1

### Issue 2: "Playwright browser not found"
**Solution:** Workflow automatically installs Chromium. Check if step completed successfully.

### Issue 3: "Input video not found"
**Solution:** 
- Check if video generation step succeeded
- Verify CapCut session is still valid
- Session may have expired - regenerate `proven_session.json` locally

### Issue 4: "YouTube upload failed"
**Solution:**
- Verify `YOUTUBE_CREDENTIALS` and `YOUTUBE_TOKEN` secrets are correct
- Token may have expired - regenerate locally and update secret

### Issue 5: "FFmpeg not found"
**Solution:** System dependencies step should install FFmpeg. Check logs.

### Issue 6: "OpenRouter API error"
**Solution:** 
- Verify `OPENROUTER_API_KEY` secret is correct
- Check API key has credits
- API may be rate-limited

---

## 🎯 Best Practices

### 1. Test Locally First
Always test the pipeline locally before running in GitHub Actions:
```bash
RUN_FULL_PIPELINE.bat
```

### 2. Monitor Costs
- GitHub Actions: Free tier = 2,000 minutes/month
- OpenRouter API: ~$0.001 per video
- YouTube API: Free (quota limits apply)

### 3. Session Management
- CapCut session expires after ~30 days
- Regenerate `proven_session.json` locally when needed
- Update `PROVEN_SESSION` secret in GitHub

### 4. Artifact Cleanup
- Raw videos: 7 days retention (large files)
- Edited videos: 30 days retention (backup)
- Logs: 7 days retention
- Manually delete old artifacts to save storage

### 5. Privacy Settings
- Default: Public
- For testing: Use "unlisted" or "private"
- Change in workflow dispatch input

---

## 📈 Scaling

### Process Multiple Videos:
The current setup processes 1 video per run. To process multiple:

1. **Option A:** Run workflow multiple times manually
2. **Option B:** Modify `src/main.py` to process multiple jobs
3. **Option C:** Use matrix strategy in workflow (advanced)

### Parallel Processing:
```yaml
# In .github/workflows/full_pipeline.yml
strategy:
  matrix:
    video: [1, 2, 3]  # Process 3 videos in parallel
```

---

## 🔄 Updating Secrets

When credentials expire or change:

1. Generate new credentials locally
2. Go to **Settings** → **Secrets and variables** → **Actions**
3. Click on secret name
4. Click **Update secret**
5. Paste new value
6. Click **Update secret**

---

## ✅ Verification Checklist

Before running in GitHub Actions:

- [ ] All 5 secrets created
- [ ] Repository pushed to GitHub
- [ ] Workflow file exists: `.github/workflows/full_pipeline.yml`
- [ ] `.gitignore` prevents committing credentials
- [ ] Local pipeline works successfully
- [ ] CapCut session is valid
- [ ] YouTube credentials are valid
- [ ] OpenRouter API key has credits

---

## 🎉 Success!

Once set up, your pipeline will:

✅ **Generate videos** from CapCut AI (headless)  
✅ **Edit videos** professionally with AI  
✅ **Upload to YouTube** automatically  
✅ **Save artifacts** for download  
✅ **Run on schedule** (optional)  

**No manual intervention required!** 🚀

---

## 📞 Support

If you encounter issues:

1. Check workflow logs in Actions tab
2. Verify all secrets are set correctly
3. Test locally first
4. Check artifact downloads for error details
5. Review `GITHUB_ACTIONS_SETUP.md` (this file)

---

## 🔗 Related Files

- `.github/workflows/full_pipeline.yml` - Workflow configuration
- `run_full_pipeline.py` - Pipeline orchestrator
- `requirements.txt` - Python dependencies
- `.gitignore` - Files to ignore
- `README.md` - Project documentation
