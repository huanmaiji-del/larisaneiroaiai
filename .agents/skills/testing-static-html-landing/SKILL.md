# Testing Static HTML Landing Pages

Use this skill when testing this repository's single-file static landing page.

## Devin Secrets Needed

None. The site is public/static and does not require login, API keys, or admin credentials for the landing-page checks.

## Setup

1. Confirm the repo has a single `index.html` at the repository root.
2. For a local preview, run from the repo root:
   ```bash
   python3 -m http.server 4173 --directory .
   ```
3. For deployed PR previews, open the public preview URL if one has been provided.
4. Validate static HTML edits with:
   ```bash
   python3 - <<'PY'
   from html.parser import HTMLParser
   from pathlib import Path
   HTMLParser().feed(Path('index.html').read_text(encoding='utf-8'))
   print('HTML parsed OK')
   PY
   git diff --check
   ```

## Browser E2E Checklist

1. Open the preview in Chrome at a desktop viewport.
2. Verify the header, hero copy, primary CTA, secondary CTA, and main visual are present.
3. Click primary anchor CTAs and header nav links; assert they scroll to the exact expected section headings.
4. Verify pricing cards show the expected plan names, prices, badges, and buttons.
5. Resize to a mobile-width viewport and verify desktop navigation collapses/vanishes, the logo and buy CTA remain visible, and cards stack vertically.
6. Record GUI testing with annotations. If `wmctrl` is unavailable for maximizing/resizing Chrome, `xdotool getactivewindow windowsize <w> <h> windowmove 0 0` can be used as a fallback.

## Reporting

- Post one PR comment with concise pass/fail bullets and preview URL.
- Include screenshots for desktop hero, desktop pricing/sections, and mobile pricing.
- Mention clearly if CI is not configured or if purchase/Discord links are still placeholders.
