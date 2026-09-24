# Google Fonts Distribution Status

**Last Updated:** 2026-09-24

## Current Status: ⚠️ Known Issue

Google Fonts is currently experiencing an infrastructure issue affecting woff2 file delivery for Red Hat fonts.

### What's Happening

- **Issue:** woff2 format files return HTTP 404
- **Workaround:** Google Fonts CSS API automatically serves TTF format
- **Impact:** Fonts load correctly but with larger file sizes (~20-40% larger than woff2)
- **Affected Versions:**
  - Red Hat Display v21
  - Red Hat Text v19
  - Red Hat Mono v16

### Timeline

- **2026-08-13:** Issue first discovered during production deployment
- **2026-09-24:** Issue investigated and documented in this repository
- **2026-09-24:** Issue reported to Google Fonts team
- **Status:** Awaiting response from Google Fonts

### What This Means For Users

**If you're using Google Fonts:**
- ✅ Your fonts will continue to load normally
- ⚠️ Slightly larger file sizes (performance impact minimal)
- 📝 No action required on your part

**If you have cached woff2 CSS:**
- ⚠️ You may see 404 errors in browser console
- 🔄 Clear browser cache or wait for cache expiration
- ✅ New requests will receive working TTF URLs

### Recommended Actions

1. **For new projects:** Consider [self-hosting](README.md#self-hosting-fonts-recommended) for more control
2. **For existing projects:** Google Fonts continues to work, monitor for updates
3. **For production sites:** Test font loading, consider self-hosted backup

### Alternatives to Google Fonts

See [Self-Hosting section in README](README.md#self-hosting-fonts-recommended) for:
- Direct download and hosting
- jsDelivr CDN option
- npm package integration

### Tracking & Updates

- **Google Fonts Issue:** To be added once filed
- **Repository Issue:** [#TBD - Internal tracking issue]
- **Updates:** This file will be updated as situation changes

---

## Technical Details

### Example URLs

**Working TTF URL:**
```
https://fonts.gstatic.com/s/redhatdisplay/v21/8vIf7wUr0m80wwYf0QCXZzYzUoTK8RZQvRd-D1NYbmyWckg.ttf
```
Status: HTTP 200 ✅

**Failing woff2 URL:**
```
https://fonts.gstatic.com/s/redhatdisplay/v21/8vIq7wUr0m80wwYf0QCXZzYzUoTK8RZQvRd-D1NYbmyWEEMbCa8AIHrEG1nO6OOJzScMKMPL.woff2
```
Status: HTTP 404 ❌

### CSS Endpoint Behavior

As of 2026-09-24, the Google Fonts CSS API returns TTF format:

```css
/* Example from https://fonts.googleapis.com/css2?family=Red+Hat+Display:wght@400;700 */
@font-face {
  font-family: 'Red Hat Display';
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: url(https://fonts.gstatic.com/s/redhatdisplay/v21/8vIf7wUr0m80wwYf0QCXZzYzUoTK8RZQvRd-D1NYbmyWckg.ttf) format('truetype');
}
```

Previously, modern browsers would receive woff2 URLs, but the infrastructure issue prevents proper woff2 serving.

---

## Historical Context

This is not the first time Google Fonts has had infrastructure issues with font formats:

- **2018:** Similar issue with .woff files ([google/fonts#1642](https://github.com/google/fonts/issues/1642))
- **2024:** Figtree woff2 404s ([google/fonts#10804](https://github.com/google/fonts/issues/10804))

These issues typically resolve but demonstrate the value of having self-hosting as a backup strategy.

---

## Need Help?

- **Report issues:** [File an issue](https://github.com/RedHatOfficial/RedHatFont/issues)
- **Questions:** Check [README.md](README.md) for detailed documentation
- **Self-hosting help:** See [self-hosting guide](README.md#self-hosting-fonts-recommended)
