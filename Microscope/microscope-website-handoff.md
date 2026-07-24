# Microscope Legal and Support Pages — Website Handoff

## Routes

| Route | Source |
| --- | --- |
| `/apps/microscope/privacy` | `microscope-privacy.md` |
| `/apps/microscope/support` | `microscope-support.md` |
| `/apps/microscope/terms` | `microscope-terms.md` |

## Presentation

- Use the existing `sahilsatralkar.com` header, footer, typography, color, and responsive content container.
- Keep the legal pages quiet and readable; do not add promotional banners, newsletter forms, analytics, or third-party embeds.
- Render headings with semantic HTML in the same hierarchy as the source Markdown.
- Render email addresses as `mailto:` links and external references as normal HTTPS links.
- Show the effective date near the title on Privacy and Terms.
- Add a small related-links footer connecting Privacy, Support, and Terms.
- Preserve readable line length and sufficient contrast in both Light and Dark appearances.
- Add page titles and descriptions:
  - Privacy: `Microscope Privacy Policy`
  - Support: `Microscope Support`
  - Terms: `Microscope Terms of Use`
- Set each canonical URL to the public route in its source document.
- Return a real `200` page at each route without requiring JavaScript, authentication, or cookies.

## Content and compliance checks

- Confirm the public provider name before publication. The drafts deliberately use “we” rather than assuming a company or legal entity.
- If the pages themselves introduce analytics, hosting logs beyond ordinary security operations, contact forms, or cookies, update the website-level privacy disclosure before launch.
- Have the Terms reviewed for the applicable business entity and jurisdictions before treating them as legal advice.
- Update the effective date if publication occurs after July 25, 2026.
- Do not change the Apple legal destinations:
  - Standard EULA: `https://www.apple.com/legal/internet-services/itunes/dev/stdeula/`
  - Apple Media Services Terms: `https://www.apple.com/legal/internet-services/itunes/`
  - Apple Privacy Policy: `https://www.apple.com/legal/privacy/`

## App follow-up after deployment

The app currently uses placeholder `example.com` Privacy and Support URLs. After all three pages return `200` in production:

1. Set the in-app Privacy URL to `https://sahilsatralkar.com/apps/microscope/privacy`.
2. Set the in-app Support URL to `https://sahilsatralkar.com/apps/microscope/support`.
3. Set the in-app Terms URL to `https://sahilsatralkar.com/apps/microscope/terms`.
4. Verify links from onboarding, Settings, and the paywall on a device.
5. Use the same Privacy and Support URLs in App Store Connect metadata.

