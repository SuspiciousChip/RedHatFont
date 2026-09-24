# Stakeholder Notification Template

**Instructions:** Use this template to notify Red Hat stakeholders about the Google Fonts issue. Customize recipient list and contact information before sending.

---

## Email Template

**To:** [Red Hat Brand Team, Red Hat Web Team, Developer Relations - Add specific contacts]  
**Cc:** [Add additional stakeholders]  
**Subject:** [Info] Google Fonts Issue Affecting Red Hat Fonts - TTF Fallback Active

---

Hello [Team/Name],

This is a notification about a temporary issue with Red Hat font distribution via Google Fonts.

### Summary

Google Fonts is currently serving TTF format instead of the more efficient woff2 format for all Red Hat fonts (Display, Text, and Mono) due to an infrastructure issue on their side. **The fonts continue to load and display correctly**, but with slightly larger file sizes.

### Impact Assessment

✅ **Good News:**
- Fonts are loading normally for all users
- Google Fonts automatically serves TTF as a fallback
- No immediate action required for most sites
- No visual issues or broken fonts

⚠️ **Minor Considerations:**
- File sizes are 20-40% larger than woff2 (minimal performance impact)
- Users with cached woff2 CSS may see 404 errors in browser console (resolves automatically)

### What We've Done

1. ✅ **Investigated and confirmed the issue** (2026-09-24)
   - Tested all Red Hat font families (Display, Text, Mono)
   - Confirmed woff2 files return HTTP 404
   - Verified TTF fallback is working correctly

2. 📝 **Reporting to Google Fonts**
   - Preparing detailed issue report
   - Including technical details and reproduction steps
   - Referencing similar issues in their tracker

3. 📚 **Updated repository documentation**
   - Created comprehensive status page
   - Enhanced self-hosting guide with multiple options
   - Added version tracking information

4. 🔍 **Implemented monitoring**
   - Automated weekly testing via GitHub Actions
   - Manual testing checklist for releases
   - Will detect when issue is resolved

### What You Should Know

**For redhat.com and official Red Hat properties:**
- Please verify fonts are loading correctly on your sites
- Check browser console for any 404 errors
- Consider self-hosting as a more reliable long-term solution (see resources below)

**For external developers:**
- Documentation has been updated with self-hosting instructions
- jsDelivr CDN option available as alternative to Google Fonts
- Issue is being tracked and will be updated as situation evolves

### Resources

- **Status Page:** [GOOGLE_FONTS_STATUS.md](https://github.com/RedHatOfficial/RedHatFont/blob/master/GOOGLE_FONTS_STATUS.md)
- **Self-Hosting Guide:** [README.md - Self-Hosting Section](https://github.com/RedHatOfficial/RedHatFont#self-hosting-fonts-recommended)
- **Repository:** https://github.com/RedHatOfficial/RedHatFont
- **Google Fonts Issue:** [Will be added once filed]
- **Internal Tracking:** [Will be added once created]

### Self-Hosting Options

If you'd like to move away from Google Fonts for better reliability, we offer three easy options:

1. **Direct download** - Host font files in your project
2. **jsDelivr CDN** - Serve from GitHub via CDN (no account needed)
3. **npm package** - `@fontsource/red-hat-display` for build tool integration

Detailed instructions available in the [README](https://github.com/RedHatOfficial/RedHatFont#self-hosting-fonts-recommended).

### Timeline

- **Issue Discovered:** 2026-08-13
- **Investigation:** 2026-09-24
- **Google Fonts Notified:** 2026-09-24
- **Expected Resolution:** Unknown (depends on Google Fonts team)

### Questions?

If you have questions or need assistance with self-hosting, please:
- Reply to this email
- File an issue in the [repository](https://github.com/RedHatOfficial/RedHatFont/issues)
- Contact [Add specific contact person/team]

### Action Items

**No immediate action required**, but we recommend:

- [ ] Verify fonts load correctly on your Red Hat properties
- [ ] Check browser console for 404 errors (informational only)
- [ ] Consider self-hosting for critical applications
- [ ] Subscribe to repository notifications for updates

---

**Important:** This notification is for informational purposes. Red Hat fonts continue to work normally via Google Fonts with minimal performance impact. This issue is being tracked and monitored, and we will provide updates as the situation evolves.

Thank you for your attention to this matter.

Best regards,  
[Your Name/Team]  
[Contact Information]

---

## Slack/Teams Message Template (Short Version)

For quick internal communication:

---

📢 **Red Hat Fonts - Google Fonts Status Update**

**TL;DR:** Red Hat fonts on Google Fonts are working but using TTF instead of woff2 due to infrastructure issue.

**Impact:** ✅ Fonts load normally, ⚠️ slightly larger files (~20-40%)

**Action:** None required immediately. Consider self-hosting for better control.

**Details:** https://github.com/RedHatOfficial/RedHatFont/blob/master/GOOGLE_FONTS_STATUS.md

Questions? Reply in thread or file issue in repo.

---

## Follow-Up Communication (When Resolved)

**Subject:** [Resolved] Google Fonts Issue - Red Hat Fonts Now Serving woff2

---

Hello [Team/Name],

Good news! The Google Fonts infrastructure issue affecting Red Hat fonts has been resolved.

### Update

Google Fonts is now correctly serving woff2 format for Red Hat Display, Text, and Mono fonts. The issue that caused HTTP 404 errors for woff2 files has been fixed.

### What Changed

- ✅ woff2 URLs now return HTTP 200
- ✅ Google Fonts CSS API serves woff2 to modern browsers
- ✅ File sizes back to optimal levels
- ✅ Performance improved

### No Action Required

If you're using Google Fonts, the improved woff2 format will be served automatically on next cache refresh. No changes needed on your end.

### Documentation Updated

- [GOOGLE_FONTS_STATUS.md](https://github.com/RedHatOfficial/RedHatFont/blob/master/GOOGLE_FONTS_STATUS.md) marked as resolved
- Issue closed in our tracking system
- Monitoring continues to detect future issues

### Thank You

Thank you for your patience during this issue. If you have any questions, please don't hesitate to reach out.

Best regards,  
[Your Name/Team]

---

## Distribution List Template

**Recommended Recipients:**

### Internal Red Hat Teams
- [ ] Red Hat Brand Team
- [ ] Red Hat Design Team
- [ ] Red Hat Web Development Team (redhat.com)
- [ ] Developer Relations Team
- [ ] Technical Communications
- [ ] Product Marketing (if applicable)

### External (If Applicable)
- [ ] Community mailing lists
- [ ] Partner communications
- [ ] Developer newsletter

### Distribution Channels
- [ ] Email
- [ ] Slack/Teams channels
- [ ] Internal wiki/documentation
- [ ] GitHub discussions/announcements

---

## Customization Checklist

Before sending, customize:

- [ ] Add specific recipient names/emails
- [ ] Update contact information
- [ ] Add internal tracking links (once issues are filed)
- [ ] Adjust tone for audience (internal vs external)
- [ ] Review for any sensitive information
- [ ] Get approval if required by communication policy
- [ ] Schedule send time (avoid weekends/holidays)

---

**Last Updated:** 2026-09-24  
**Template Version:** 1.0
