# Google Fonts Issue Report

**Instructions:** Copy the content below and file it at https://github.com/google/fonts/issues/new

---

**Title:** Red Hat Display/Text/Mono v21/v19/v16 woff2 files return HTTP 404

**Labels:** `bug`, `infrastructure`

---

## Summary

Google Fonts is returning HTTP 404 errors for woff2 format files for all Red Hat font families (Display, Text, and Mono). The CSS API has adapted to serve TTF format as a fallback, so fonts continue to load, but the underlying woff2 infrastructure issue persists.

This appears similar to issue #10804 (Figtree v9 woff2 404s) and suggests an infrastructure problem between CSS generation and asset deployment.

## Affected Fonts

- **Red Hat Display** v21
- **Red Hat Text** v19
- **Red Hat Mono** v16

## Reproduction Steps

1. Request CSS endpoint for Red Hat Display:
   ```
   https://fonts.googleapis.com/css2?family=Red+Hat+Display:wght@400;700&display=swap
   ```

2. Observe that CSS returns TTF format URLs (not woff2 as expected for modern browsers):
   ```css
   @font-face {
     font-family: 'Red Hat Display';
     font-style: normal;
     font-weight: 400;
     font-display: swap;
     src: url(https://fonts.gstatic.com/s/redhatdisplay/v21/8vIf7wUr0m80wwYf0QCXZzYzUoTK8RZQvRd-D1NYbmyWckg.ttf) format('truetype');
   }
   ```

3. Attempt to access a woff2 URL directly (using v21 path pattern):
   ```
   https://fonts.gstatic.com/s/redhatdisplay/v21/8vIq7wUr0m80wwYf0QCXZzYzUoTK8RZQvRd-D1NYbmyWEEMbCa8AIHrEG1nO6OOJzScMKMPL.woff2
   ```

4. Observe HTTP 404 response

## Example URLs

### Working (TTF)
```
https://fonts.gstatic.com/s/redhatdisplay/v21/8vIf7wUr0m80wwYf0QCXZzYzUoTK8RZQvRd-D1NYbmyWckg.ttf
```
**Status:** HTTP 200 ✅

### Failing (woff2)
```
https://fonts.gstatic.com/s/redhatdisplay/v21/8vIq7wUr0m80wwYf0QCXZzYzUoTK8RZQvRd-D1NYbmyWEEMbCa8AIHrEG1nO6OOJzScMKMPL.woff2
```
**Status:** HTTP 404 ❌

## Expected Behavior

- CSS API should return woff2 URLs for modern browsers (better compression)
- woff2 files should be accessible on fonts.gstatic.com
- TTF should only be served to older browsers that don't support woff2

## Actual Behavior

- CSS API returns TTF URLs for all browsers
- Direct woff2 requests return HTTP 404
- Suggests woff2 files were not properly deployed for these font versions

## Impact

**Current Impact: Low**
- Fonts continue to load via TTF fallback
- No visual issues for end users
- CSS API has successfully adapted

**Performance Impact: Minor**
- TTF files are approximately 20-40% larger than woff2
- Slightly increased bandwidth usage and load times

**Historical Impact: Medium**
- Users who cached woff2 CSS references (before the API switched to TTF) see 404 errors
- Browser console shows 404 errors for cached woff2 URLs

## Related Issues

This appears to follow a similar pattern to:

- **#10804** - Figtree v9 CSS API intermittently returns 404 for generated woff2 URLs
  - Similar symptom: CSS API returns non-existent woff2 URLs
  - Indicates infrastructure issue between CSS generation and asset serving

- **#1642** - .woff files returning 404s (2018)
  - Historical precedent of format serving issues
  - Resolution involved adjusting format serving strategy

## Additional Context

- **First Discovered:** 2026-08-13 during production deployment
- **Investigation Date:** 2026-09-24
- **Font Repository:** https://github.com/RedHatOfficial/RedHatFont
- **Testing:** Confirmed across all weights (300-900) and italic styles
- **All three Red Hat families affected:** Display, Text, and Mono

## Suggested Resolution

1. **Investigate** why woff2 files are not accessible for these font versions
2. **Deploy** missing woff2 files to fonts.gstatic.com
3. **Verify** CSS API can successfully return woff2 URLs
4. **Consider** adding automated testing to prevent similar issues with future font updates

## Workaround for Users

While the TTF fallback works, users who prefer optimal performance can self-host the fonts. The Red Hat Font repository includes all formats (woff2, TTF, OTF) and comprehensive self-hosting documentation.

---

Thank you for maintaining Google Fonts! We appreciate your work and hope this detailed report helps identify the root cause.
