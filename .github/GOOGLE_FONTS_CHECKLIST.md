# Google Fonts Testing Checklist

Use this checklist when releasing new font versions or investigating issues.

## Pre-Release Testing

Before submitting fonts to Google Fonts:

- [ ] Test all font files locally
- [ ] Verify metadata is correct in `fonts/METADATA.pb.txt`
- [ ] Check version numbers in CHANGELOG.md
- [ ] Test variable fonts
- [ ] Review CHANGELOG for completeness
- [ ] Verify all weights render correctly
- [ ] Test italic styles
- [ ] Check for any rendering issues

## Post-Release Verification

After fonts are live on Google Fonts (allow 24-48 hours for propagation):

- [ ] Test CSS endpoint for all three families
- [ ] Verify woff2 URLs are accessible (or note if TTF is served)
- [ ] Check all weight variations (300, 400, 500, 600, 700, 800, 900)
- [ ] Test italic styles
- [ ] Verify version numbers in URLs match expectations
- [ ] Test from multiple geographic regions (use VPN or proxy)
- [ ] Check browser console for errors
- [ ] Compare file sizes (woff2 should be smallest)

## CSS Endpoints to Test

### Red Hat Display
```bash
curl "https://fonts.googleapis.com/css2?family=Red+Hat+Display:wght@300;400;500;600;700;800;900&display=swap"
```

### Red Hat Text  
```bash
curl "https://fonts.googleapis.com/css2?family=Red+Hat+Text:wght@300;400;500;600;700&display=swap"
```

### Red Hat Mono
```bash
curl "https://fonts.googleapis.com/css2?family=Red+Hat+Mono:wght@300;400;500;600;700&display=swap"
```

### With Italics
```bash
curl "https://fonts.googleapis.com/css2?family=Red+Hat+Display:ital,wght@0,300;0,400;0,700;1,300;1,400;1,700&display=swap"
```

## Font URL Testing

### Extract and Test Font URLs

```bash
# Example: Red Hat Display
CSS_URL="https://fonts.googleapis.com/css2?family=Red+Hat+Display:wght@400;700&display=swap"

# Extract first font URL
FONT_URL=$(curl -s "$CSS_URL" | grep -oP 'url\(\K[^)]+' | head -1)

# Test with curl (should return HTTP/2 200)
curl -I "$FONT_URL"

# Check file size
curl -s "$FONT_URL" | wc -c
```

### Test Specific Format

```bash
# Test if woff2 is available (example v21 URL)
curl -I "https://fonts.gstatic.com/s/redhatdisplay/v21/8vIq7wUr0m80wwYf0QCXZzYzUoTK8RZQvRd-D1NYbmyWEEMbCa8AIHrEG1nO6OOJzScMKMPL.woff2"

# Test TTF URL
curl -I "https://fonts.gstatic.com/s/redhatdisplay/v21/8vIf7wUr0m80wwYf0QCXZzYzUoTK8RZQvRd-D1NYbmyWckg.ttf"
```

## Browser Testing

### Visual Inspection

- [ ] Open test page in Chrome
- [ ] Open test page in Firefox
- [ ] Open test page in Safari
- [ ] Open test page in Edge
- [ ] Check mobile rendering (iOS Safari, Chrome Mobile)

### DevTools Checks

1. Open browser DevTools (F12)
2. Go to Network tab
3. Filter by "Font" or "woff"
4. Reload page
5. Verify:
   - [ ] All font requests return 200
   - [ ] Check format served (woff2, ttf, etc.)
   - [ ] Note file sizes
   - [ ] Check load times
   - [ ] Verify no CORS errors

### Test HTML Page

Create a simple test page:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Red Hat Fonts Test</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Red+Hat+Display:ital,wght@0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,300;1,400;1,700&display=swap" rel="stylesheet">
  <style>
    body { font-family: 'Red Hat Display', sans-serif; padding: 2rem; }
    .weight-300 { font-weight: 300; }
    .weight-400 { font-weight: 400; }
    .weight-500 { font-weight: 500; }
    .weight-600 { font-weight: 600; }
    .weight-700 { font-weight: 700; }
    .weight-800 { font-weight: 800; }
    .weight-900 { font-weight: 900; }
    .italic { font-style: italic; }
  </style>
</head>
<body>
  <h1>Red Hat Display Font Test</h1>
  
  <h2>All Weights</h2>
  <p class="weight-300">Light (300): The quick brown fox jumps over the lazy dog</p>
  <p class="weight-400">Regular (400): The quick brown fox jumps over the lazy dog</p>
  <p class="weight-500">Medium (500): The quick brown fox jumps over the lazy dog</p>
  <p class="weight-600">SemiBold (600): The quick brown fox jumps over the lazy dog</p>
  <p class="weight-700">Bold (700): The quick brown fox jumps over the lazy dog</p>
  <p class="weight-800">ExtraBold (800): The quick brown fox jumps over the lazy dog</p>
  <p class="weight-900">Black (900): The quick brown fox jumps over the lazy dog</p>
  
  <h2>Italic Styles</h2>
  <p class="weight-300 italic">Light Italic (300): The quick brown fox jumps over the lazy dog</p>
  <p class="weight-400 italic">Italic (400): The quick brown fox jumps over the lazy dog</p>
  <p class="weight-700 italic">Bold Italic (700): The quick brown fox jumps over the lazy dog</p>
</body>
</html>
```

## Performance Testing

### PageSpeed Insights

- [ ] Test page with [PageSpeed Insights](https://pagespeed.web.dev/)
- [ ] Check font loading performance
- [ ] Verify font-display strategy
- [ ] Note any font-related warnings

### WebPageTest

- [ ] Test with [WebPageTest](https://www.webpagetest.org/)
- [ ] Check waterfall chart for font loading
- [ ] Verify fonts don't block rendering
- [ ] Compare woff2 vs TTF load times

## Issue Reporting

If problems found:

### 1. Gather Information

- [ ] Document exact URLs that fail
- [ ] Note HTTP status codes
- [ ] Check if issue is intermittent (test multiple times)
- [ ] Test from different locations/networks
- [ ] Capture screenshots if visual issues
- [ ] Save Network tab output

### 2. Check Existing Issues

- [ ] Search this repository's issues
- [ ] Check [google/fonts issues](https://github.com/google/fonts/issues)
- [ ] Look for similar recent reports

### 3. File Issue

- [ ] Use template in `.github/GOOGLE_FONTS_ISSUE_REPORT.md` for google/fonts
- [ ] Create tracking issue in this repository
- [ ] Update `GOOGLE_FONTS_STATUS.md` if needed
- [ ] Notify stakeholders if critical

### 4. Document in This Repository

- [ ] Update `GOOGLE_FONTS_STATUS.md` with new information
- [ ] Link to filed issues
- [ ] Update timeline
- [ ] Add to CHANGELOG if significant

## Version Tracking

### Check Current Versions

```bash
# Display
curl -s "https://fonts.googleapis.com/css2?family=Red+Hat+Display:wght@400" | grep -oP 'redhatdisplay/v\d+' | head -1

# Text
curl -s "https://fonts.googleapis.com/css2?family=Red+Hat+Text:wght@400" | grep -oP 'redhattext/v\d+' | head -1

# Mono
curl -s "https://fonts.googleapis.com/css2?family=Red+Hat+Mono:wght@400" | grep -oP 'redhatmono/v\d+' | head -1
```

### Document Version Changes

When Google Fonts version increments:

- [ ] Note version number in CHANGELOG.md
- [ ] Update version references in GOOGLE_FONTS_STATUS.md
- [ ] Test all endpoints with new version
- [ ] Verify backward compatibility
- [ ] Update documentation if needed

## Automated Testing

The repository includes automated monitoring via GitHub Actions:

- **Workflow:** `.github/workflows/test-google-fonts.yml`
- **Schedule:** Weekly (Mondays at 9 AM UTC)
- **Manual Trigger:** Available via GitHub Actions UI

### Review Automated Results

- [ ] Check workflow runs in Actions tab
- [ ] Review summary reports
- [ ] Investigate any failures
- [ ] Close auto-created issues when resolved

## Communication Checklist

When issues are detected:

- [ ] Update GOOGLE_FONTS_STATUS.md
- [ ] File issue in google/fonts (if warranted)
- [ ] Create tracking issue in this repository
- [ ] Notify Red Hat stakeholders (see template)
- [ ] Update README.md if user action needed
- [ ] Post update in relevant channels/discussions

## Resolution Verification

When Google Fonts team reports a fix:

- [ ] Run full testing checklist again
- [ ] Verify woff2 URLs return 200
- [ ] Check CSS API returns woff2 format
- [ ] Test all weights and styles
- [ ] Update GOOGLE_FONTS_STATUS.md with resolution
- [ ] Close related issues
- [ ] Thank Google Fonts team
- [ ] Notify stakeholders of resolution

---

## Quick Reference Commands

```bash
# Test all families quickly
for family in "Red+Hat+Display" "Red+Hat+Text" "Red+Hat+Mono"; do
  echo "Testing $family..."
  curl -f -s "https://fonts.googleapis.com/css2?family=${family}:wght@400;700" > /dev/null && echo "✅ $family OK" || echo "❌ $family FAILED"
done

# Extract all font URLs from CSS
curl -s "https://fonts.googleapis.com/css2?family=Red+Hat+Display:wght@300;400;700" | grep -oP 'url\(\K[^)]+'

# Test multiple URLs at once
curl -s "https://fonts.googleapis.com/css2?family=Red+Hat+Display:wght@400;700" | grep -oP 'url\(\K[^)]+' | while read url; do
  STATUS=$(curl -s -o /dev/null -w "%{http_code}" "$url")
  echo "$url - HTTP $STATUS"
done
```

---

**Last Updated:** 2026-09-24  
**Next Review:** After next font release or every 3 months
