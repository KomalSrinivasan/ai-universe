# GitHub Pages Setup Guide

If you're seeing **404 errors**, follow these steps to enable GitHub Pages:

## 📋 Quick Fix Checklist

### Step 1: Enable GitHub Pages

1. Go to your repository: https://github.com/KomalSrinivasan/ai-universe
2. Click **Settings** (top menu)
3. Scroll down to **Pages** (left sidebar under "Code and automation")
4. Under **Build and deployment**:
   - **Source**: Select `Deploy from a branch`
   - **Branch**: Select `gh-pages` branch
   - **Folder**: Select `/ (root)`
5. Click **Save**

### Step 2: Wait for Deployment

- GitHub will show a message: "Your site is ready to be published at..."
- Wait 1-2 minutes for the first deployment
- Refresh the Settings > Pages page to see the live URL

### Step 3: Verify Deployment

Check the Actions tab:
1. Go to **Actions** tab in your repository
2. Look for the "Deploy MkDocs to GitHub Pages" workflow
3. Ensure it has a **green checkmark** ✅
4. If there's a ❌ red X, click it to see the error

---

## 🔧 Troubleshooting

### Issue: "404 File not found"

**Cause**: GitHub Pages isn't enabled or `gh-pages` branch doesn't exist.

**Solution**:
```bash
# Check if gh-pages branch exists
git branch -a | grep gh-pages

# If missing, trigger deployment by pushing a commit
git commit --allow-empty -m "Trigger GitHub Pages deployment"
git push origin main

# This will trigger the GitHub Action that creates gh-pages branch
```

### Issue: Workflow fails with errors

**Solution**: Check the workflow logs:
1. Go to **Actions** tab
2. Click the failed workflow
3. Click on the "deploy" job
4. Expand each step to see errors
5. Common fixes:
   - Ensure `requirements.txt` is present
   - Ensure `mkdocs.yml` is valid
   - Check permissions in Settings > Actions > General

### Issue: Site shows but pages are 404

**Cause**: Base URL mismatch

**Solution**: Verify `site_url` in `mkdocs.yml`:
```yaml
site_url: https://komalsrinivasan.github.io/ai-universe/
```

Must match your GitHub username and repository name exactly (case-sensitive).

---

## ✅ Expected Workflow

When you push to `main` branch:

1. **GitHub Actions triggers** (`.github/workflows/deploy-docs.yml`)
2. **Workflow runs**:
   - Checks out code
   - Installs Python and dependencies
   - Builds documentation with MkDocs
   - Creates `.nojekyll` file
   - Pushes to `gh-pages` branch
3. **GitHub Pages deploys** from `gh-pages` branch
4. **Site is live** at https://komalsrinivasan.github.io/ai-universe/

---

## 🚀 Manual Deployment (If Needed)

If automatic deployment fails, deploy manually:

```bash
# Ensure you're on main branch
git checkout main

# Build the site
source .venv/bin/activate  # or activate your virtual environment
mkdocs build --clean

# Deploy to gh-pages
mkdocs gh-deploy --force

# This will:
# - Build the site
# - Create/update gh-pages branch
# - Push to GitHub
```

---

## 📝 Verifying Everything Works

After enabling GitHub Pages:

1. **Homepage**: https://komalsrinivasan.github.io/ai-universe/
   - Should show the main landing page

2. **Category Pages**:
   - https://komalsrinivasan.github.io/ai-universe/categories/foundation-models/
   - https://komalsrinivasan.github.io/ai-universe/categories/infrastructure/
   - etc.

3. **Guide Pages**:
   - https://komalsrinivasan.github.io/ai-universe/guides/getting-started/
   - https://komalsrinivasan.github.io/ai-universe/guides/quick-reference/

---

## 🔍 Debug Checklist

- [ ] Repository is public (or GitHub Pages enabled for private repo)
- [ ] GitHub Pages is enabled in Settings > Pages
- [ ] Source is set to `gh-pages` branch
- [ ] `gh-pages` branch exists (check in branches dropdown)
- [ ] Latest workflow run succeeded (check Actions tab)
- [ ] `site_url` in mkdocs.yml matches GitHub Pages URL
- [ ] `.nojekyll` file exists in deployed site

---

## 💡 Pro Tips

### Force Rebuild

If the site isn't updating:

```bash
# Create empty commit to trigger rebuild
git commit --allow-empty -m "chore: force rebuild"
git push origin main
```

### Check Deployment Status

```bash
# View GitHub Pages status via API
curl -H "Authorization: token YOUR_GITHUB_TOKEN" \
  https://api.github.com/repos/KomalSrinivasan/ai-universe/pages
```

### Local Testing

Always test locally before deploying:

```bash
# Serve locally
mkdocs serve

# Test build
mkdocs build --clean

# Visit http://localhost:8000
```

---

## 📞 Still Having Issues?

If problems persist:

1. **Check workflow file**: `.github/workflows/deploy-docs.yml`
2. **Verify permissions**: Settings > Actions > General > Workflow permissions
   - Should be "Read and write permissions"
3. **Check branch protection**: Settings > Branches
   - `gh-pages` should NOT have protection rules
4. **Review logs**: Actions tab > Latest workflow > View logs

---

## 🎯 Expected Timeline

From push to live site:

- **Code push**: Instant
- **Workflow trigger**: ~10 seconds
- **Build & deploy**: 1-2 minutes
- **GitHub Pages publish**: 30-60 seconds
- **Total**: ~2-3 minutes

---

## ✨ Success Indicators

You'll know it's working when:

- ✅ Actions tab shows green checkmark
- ✅ Settings > Pages shows "Your site is live at..."
- ✅ Visiting the URL shows your documentation
- ✅ All navigation links work
- ✅ Search functionality works
- ✅ Dark/light mode toggles correctly

---

**After following this guide, your site should be live at:**

🌐 **https://komalsrinivasan.github.io/ai-universe/**
