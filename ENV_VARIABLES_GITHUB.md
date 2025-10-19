# Environment Variables in GitHub Actions

## ❓ Your Question

You have these in `.env`:
```env
GOOGLE_CREDENTIALS_JSON_PATH=./google_credentials.json
GOOGLE_SHEETS_ID=1CJMBuqpD1s05mLY4Yw4FANKVe-fDLhsCQA9Gv70O1TM
GOOGLE_SHEET_NAME=Sheet1
USE_CHROME_PROFILE=true
CHROME_PROFILE_BACKUP=true
PERFORM_HUMAN_PAUSE_ON_CAPTCHA=true
```

**How to set these in GitHub?**
**Will the script look for them in secrets?**

---

## ✅ Answer

### **Yes! The script will automatically read them from GitHub Secrets.**

Here's how it works:

---

## 🔐 Step 1: Create GitHub Secrets

You need to create **7 total secrets** (5 from files + 2 from .env):

### **From Files (5 secrets):**

1. **PROVEN_SESSION** - From `state/proven_session.json`
2. **YOUTUBE_CREDENTIALS** - From `youtube_credentials.json`
3. **YOUTUBE_TOKEN** - From `youtube_token.json`
4. **GOOGLE_CREDENTIALS** - From `google_credentials.json`
5. **OPENROUTER_API_KEY** - From `manifest.json`

### **From .env (2 secrets):**

6. **GOOGLE_SHEETS_ID**
   - **Value:** `1CJMBuqpD1s05mLY4Yw4FANKVe-fDLhsCQA9Gv70O1TM`

7. **GOOGLE_SHEET_NAME**
   - **Value:** `Sheet1`

---

## 🔧 How GitHub Actions Uses Them

### **The Workflow File Sets Environment Variables:**

In `.github/workflows/full_pipeline.yml`, we set these as environment variables:

```yaml
- name: Run Full Pipeline
  env:
    # Google Sheets configuration
    GOOGLE_CREDENTIALS_JSON_PATH: ./google_credentials.json
    GOOGLE_SHEETS_ID: ${{ secrets.GOOGLE_SHEETS_ID }}
    GOOGLE_SHEET_NAME: ${{ secrets.GOOGLE_SHEET_NAME }}
    
    # Chrome profile settings (disabled in headless mode)
    USE_CHROME_PROFILE: false
    CHROME_PROFILE_BACKUP: false
    
    # Human intervention (disabled in CI)
    PERFORM_HUMAN_PAUSE_ON_CAPTCHA: false
```

### **Your Python Code Reads Them:**

Your code uses `python-dotenv` to load environment variables:

```python
from dotenv import load_dotenv
import os

load_dotenv()  # Loads from .env file locally

# Read environment variables
sheets_id = os.getenv('GOOGLE_SHEETS_ID')
sheet_name = os.getenv('GOOGLE_SHEET_NAME')
```

**In GitHub Actions:**
- `.env` file doesn't exist (not committed)
- Environment variables are set by the workflow
- Your code reads from `os.getenv()` - works the same way!

---

## 📋 What Happens to Each Variable

### **1. GOOGLE_CREDENTIALS_JSON_PATH**
```yaml
GOOGLE_CREDENTIALS_JSON_PATH: ./google_credentials.json
```
- **Local:** Points to your local file
- **GitHub:** Points to file created from `GOOGLE_CREDENTIALS` secret
- **No secret needed** - hardcoded in workflow

### **2. GOOGLE_SHEETS_ID**
```yaml
GOOGLE_SHEETS_ID: ${{ secrets.GOOGLE_SHEETS_ID }}
```
- **Local:** Read from `.env`
- **GitHub:** Read from secret → Set as env var → Your code reads it
- **Secret needed:** ✅ Yes

### **3. GOOGLE_SHEET_NAME**
```yaml
GOOGLE_SHEET_NAME: ${{ secrets.GOOGLE_SHEET_NAME }}
```
- **Local:** Read from `.env`
- **GitHub:** Read from secret → Set as env var → Your code reads it
- **Secret needed:** ✅ Yes

### **4. USE_CHROME_PROFILE**
```yaml
USE_CHROME_PROFILE: false
```
- **Local:** `true` (uses saved Chrome profile)
- **GitHub:** `false` (headless mode, no profiles)
- **No secret needed** - hardcoded to `false`

### **5. CHROME_PROFILE_BACKUP**
```yaml
CHROME_PROFILE_BACKUP: false
```
- **Local:** `true` (backs up Chrome profile)
- **GitHub:** `false` (no profiles in CI)
- **No secret needed** - hardcoded to `false`

### **6. PERFORM_HUMAN_PAUSE_ON_CAPTCHA**
```yaml
PERFORM_HUMAN_PAUSE_ON_CAPTCHA: false
```
- **Local:** `true` (pauses for human to solve CAPTCHA)
- **GitHub:** `false` (no human available in CI)
- **No secret needed** - hardcoded to `false`

---

## 🎯 Summary Table

| Variable | Local (.env) | GitHub (Secret) | GitHub (Hardcoded) |
|----------|--------------|-----------------|-------------------|
| `GOOGLE_CREDENTIALS_JSON_PATH` | ✅ | ❌ | ✅ `./google_credentials.json` |
| `GOOGLE_SHEETS_ID` | ✅ | ✅ | ❌ |
| `GOOGLE_SHEET_NAME` | ✅ | ✅ | ❌ |
| `USE_CHROME_PROFILE` | ✅ `true` | ❌ | ✅ `false` |
| `CHROME_PROFILE_BACKUP` | ✅ `true` | ❌ | ✅ `false` |
| `PERFORM_HUMAN_PAUSE_ON_CAPTCHA` | ✅ `true` | ❌ | ✅ `false` |

---

## 🚀 Quick Setup

### **1. Run the extraction script:**
```bash
python extract_secrets_for_github.py
```

This will show you:
- Content of all credential files
- Values from `.env` file
- Exactly what to copy to GitHub Secrets

### **2. Create secrets in GitHub:**

Go to: **GitHub Repo → Settings → Secrets and variables → Actions**

Create these 7 secrets:

| Secret Name | Value From |
|------------|------------|
| `PROVEN_SESSION` | `state/proven_session.json` |
| `YOUTUBE_CREDENTIALS` | `youtube_credentials.json` |
| `YOUTUBE_TOKEN` | `youtube_token.json` |
| `GOOGLE_CREDENTIALS` | `google_credentials.json` |
| `OPENROUTER_API_KEY` | `manifest.json` |
| `GOOGLE_SHEETS_ID` | `.env` (your spreadsheet ID) |
| `GOOGLE_SHEET_NAME` | `.env` (usually "Sheet1") |

### **3. Done!**

Your code will automatically:
- ✅ Read secrets from GitHub
- ✅ Set them as environment variables
- ✅ Use `os.getenv()` to access them
- ✅ Work exactly like it does locally

---

## 🔍 How to Verify

### **Check if your code uses environment variables:**

```bash
# Search for os.getenv usage
grep -r "os.getenv" src/
```

### **Common patterns:**
```python
# Your code probably has something like this:
sheets_id = os.getenv('GOOGLE_SHEETS_ID')
sheet_name = os.getenv('GOOGLE_SHEET_NAME', 'Sheet1')
use_chrome = os.getenv('USE_CHROME_PROFILE', 'false').lower() == 'true'
```

---

## 💡 Why This Works

### **Local Development:**
```
.env file → load_dotenv() → os.getenv() → Your code
```

### **GitHub Actions:**
```
GitHub Secrets → Workflow env: → os.getenv() → Your code
```

**Same interface (`os.getenv()`), different source!**

---

## 🐛 Troubleshooting

### **Issue: "GOOGLE_SHEETS_ID not found"**
**Solution:** Create the secret in GitHub Settings

### **Issue: "Can't access Google Sheets"**
**Solution:** 
1. Verify `GOOGLE_CREDENTIALS` secret is correct
2. Verify `GOOGLE_SHEETS_ID` is correct
3. Check if sheet is shared with service account email

### **Issue: "Chrome profile not found"**
**Solution:** This is expected in GitHub Actions (headless mode)
- `USE_CHROME_PROFILE` is set to `false` automatically
- Uses session from `PROVEN_SESSION` secret instead

---

## ✅ Final Checklist

Before running in GitHub Actions:

- [ ] Created `GOOGLE_SHEETS_ID` secret
- [ ] Created `GOOGLE_SHEET_NAME` secret
- [ ] Created other 5 secrets (credentials)
- [ ] Verified `.env` is in `.gitignore` (not committed)
- [ ] Tested locally with `.env` file
- [ ] Ready to push to GitHub

---

## 🎉 That's It!

Your environment variables will work seamlessly in both:
- ✅ **Local development** (from `.env` file)
- ✅ **GitHub Actions** (from secrets)

No code changes needed! 🚀
