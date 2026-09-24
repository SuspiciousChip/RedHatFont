# Internal Tracking Issue Template

**Instructions:** Create a new issue in this repository using the content below to track the Google Fonts issue internally.

---

**Title:** [External] Google Fonts infrastructure issue - woff2 files unavailable

**Labels:** `external-dependency`, `google-fonts`, `documentation`, `monitoring`

---

## Summary

Google Fonts is experiencing an infrastructure issue where woff2 format files for Red Hat Display, Text, and Mono fonts return HTTP 404. The CSS API has adapted to serve TTF format as a fallback, so fonts continue to load correctly but with larger file sizes.

This issue is being tracked for internal awareness and coordination with Red Hat stakeholders.

## Current Status

- **Issue Discovered:** 2026-08-13
- **Investigation Completed:** 2026-09-24
- **User Impact:** Low (fonts load via TTF fallback)
- **Google Fonts Issue:** [Link to be added after filing]

## What We've Done

### Documentation
- ✅ Created [GOOGLE_FONTS_STATUS.md](../blob/master/GOOGLE_FONTS_STATUS.md) with comprehensive status information
- ✅ Updated [README.md](../blob/master/README.md) with:
  - Google Fonts status notice
  - Enhanced self-hosting guide (3 options)
  - Version information section
- ✅ Created detailed investigation spec in `.kiro/specs/google-fonts-404-issue.md`

### Reporting & Communication
- ✅ Prepared Google Fonts issue report ([template](../blob/master/.github/GOOGLE_FONTS_ISSUE_REPORT.md))
- ✅ Drafted stakeholder notification email
- 📋 **TODO:** File issue in google/fonts repository
- 📋 **TODO:** Send stakeholder notifications

### Monitoring & Testing
- ✅ Implemented automated monitoring via [GitHub Actions](../blob/master/.github/workflows/test-google-fonts.yml)
  - Runs weekly (Mondays 9 AM UTC)
  - Tests all three font families
  - Detects format changes (woff2 vs TTF)
  - Auto-creates alerts on failure
- ✅ Created [manual testing checklist](../blob/master/.github/GOOGLE_FONTS_CHECKLIST.md)

## Technical Details

### Affected Fonts
- Red Hat Display v21
- Red Hat Text v19
- Red Hat Mono v16

### Issue Details
- **Symptom:** woff2 URLs return HTTP 404
- **Workaround:** Google Fonts CSS API serves TTF format
- **Impact:** ~20-40% larger file sizes, minimal performance impact

### Example URLs
**Working (TTF):**
```
https://fonts.gstatic.com/s/redhatdisplay/v21/8vIf7wUr0m80wwYf0QCXZzYzUoTK8RZQvRd-D1NYbmyWckg.ttf
```

**Failing (woff2):**
```
https://fonts.gstatic.com/s/redhatdisplay/v21/8vIq7wUr0m80wwYf0QCXZzYzUoTK8RZQvRd-D1NYbmyWEEMbCa8AIHrEG1nO6OOJzScMKMPL.woff2
```

## Related Issues

- Similar pattern: [google/fonts#10804](https://github.com/google/fonts/issues/10804) (Figtree woff2 404s)
- Historical: [google/fonts#1642](https://github.com/google/fonts/issues/1642) (woff 404s in 2018)

## Action Items

### Immediate (Phase 1) ✅
- [x] Create status documentation
- [x] Update README with self-hosting guide
- [x] Prepare Google Fonts issue report
- [x] Implement monitoring
- [x] Create testing checklist
- [x] Prepare stakeholder notification

### Pending (Phase 2)
- [ ] File issue in google/fonts repository
- [ ] Send notifications to Red Hat stakeholders
- [ ] Identify Red Hat contact for Google Fonts management
- [ ] Verify official Red Hat sites are not affected

### Ongoing
- [ ] Monitor automated test results
- [ ] Update GOOGLE_FONTS_STATUS.md as situation changes
- [ ] Track Google Fonts issue for updates
- [ ] Close this issue when woff2 files are accessible

## User Guidance

### For External Users
Users experiencing issues should:
1. Check [GOOGLE_FONTS_STATUS.md](../blob/master/GOOGLE_FONTS_STATUS.md) for current status
2. Consider [self-hosting](../blob/master/README.md#self-hosting-fonts-recommended) for better control
3. Report persistent issues here

### For Red Hat Teams
Internal teams should:
1. Verify fonts load correctly on your properties
2. Consider self-hosting for critical applications
3. Review [stakeholder notification](../blob/master/.github/STAKEHOLDER_NOTIFICATION.md) for details

## Monitoring

This issue will be automatically updated by:
- Weekly GitHub Actions monitoring workflow
- Manual reviews during font releases
- Updates from Google Fonts team

## Resolution Criteria

This issue can be closed when:
- [ ] woff2 URLs return HTTP 200
- [ ] Google Fonts CSS API serves woff2 to modern browsers
- [ ] All tests pass for at least 2 consecutive weeks
- [ ] GOOGLE_FONTS_STATUS.md updated to reflect resolution

## Resources

- **Status Page:** [GOOGLE_FONTS_STATUS.md](../blob/master/GOOGLE_FONTS_STATUS.md)
- **Testing Checklist:** [.github/GOOGLE_FONTS_CHECKLIST.md](../blob/master/.github/GOOGLE_FONTS_CHECKLIST.md)
- **Monitoring Workflow:** [.github/workflows/test-google-fonts.yml](../blob/master/.github/workflows/test-google-fonts.yml)
- **Investigation Spec:** `.kiro/specs/google-fonts-404-issue.md`
- **Google Fonts Issue:** [To be added]

---

## Updates

### 2026-09-24
- Investigation completed
- Documentation created
- Monitoring implemented
- Ready for stakeholder communication

---

**Note:** This is an external dependency issue. We cannot fix Google's infrastructure directly, but we are:
1. Documenting the issue thoroughly
2. Providing alternatives (self-hosting)
3. Monitoring for changes
4. Coordinating with Google Fonts team
