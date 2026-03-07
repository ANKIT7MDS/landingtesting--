# EventLens — Release Notes
## Changes in this build

### 🔥 New Files
- `auth.js` — Shared auth module. Include in ALL pages.
- `manifest.json` — Fixed PWA manifest (start_url, icons, theme)

### 📄 Modified Files

#### index.html
- Landing page MERGED into vLogin view
- Plans pricing section added
- PWA manifest + theme-color meta added
- Google Fonts (Plus Jakarta Sans, Sora) added

#### client-gallery.html  
- Limit: 3000 → 60 per page (CRITICAL perf fix)
- IntersectionObserver infinite scroll added
- No more "load all at once"

#### staff-upload.html
- Resumable upload state (sessionStorage)
- Resume bar UI — user sees "Resume करें?" on refresh
- Retry with exponential backoff
- Upload state saved after each batch

#### landing-page.html (standalone)
- Clean light theme version (keep for reference)
- All 6 plans with pricing

### 🔧 TODO (Next Sprint)
- [ ] Add auth.js to all HTML files (replace inline auth)
- [ ] Political forms mobile responsive
- [ ] Plan enforcement backend middleware
- [ ] S3 lifecycle rules (CloudShell)
- [ ] Rekognition search cache
- [ ] Remove: eventlens-landing-v2.html (duplicate)
- [ ] Remove: political_mandal_reporting_dashboard_v3_mandal_filter.html (old)

### ⚠️ Repo Cleanup Needed
Delete these files from repo:
- `eventlens-landing-v2.html` (duplicate landing)
- `EventLens_Political_Suite.pptx` (should not be in web repo)
- `landing-page-new.html` (temp file)

### 🔐 Auth Pattern (use everywhere)
```html
<script src="auth.js"></script>
<script>
  // Check login
  if (!ELAuth.isLoggedIn()) {
    location.href = 'index.html';
  }
  // Get token for API calls
  const headers = ELAuth.authHeaders();
  // Get user info
  const user = ELAuth.getUser();
  // Check plan feature
  if (ELAuth.hasFeature('analytics')) { ... }
</script>
```
