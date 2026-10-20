# Eleven Motors landing page: developer notes

Static page. No build step. Upload the whole folder (keep `index.html` next to `assets/`).

- `index.html`: the page (HTML, CSS and JS in one file)
- `assets/img`, `assets/video`: all photos, posters and compressed videos (about 4.4 MB total)
- `LEADS_SETUP.md`: how to connect forms to a Google Sheet and email (do this before launch)

## Before going live
1. Set `CONFIG.leadEndpoint` in the script at the bottom of `index.html` (see `LEADS_SETUP.md`).
2. Nothing else needs editing day to day. The page shows no prices or availability on purpose (they change daily). Every "Check availability" button opens `https://elevenmotorske.com/vehicles` (set in `CONFIG.vehicles`). The `CARS` list only holds example model names and photos.
3. Confirm opening hours with the client (site says 9am to 5pm, Google Business Profile says 7:30am).
4. Add Google Analytics / Tag Manager. The page already pushes `lead`, `whatsapp_click`, `open_test_drive` to `dataLayer`.
5. Add `<link rel="canonical">` for the final page URL.

## Fonts
Body: Sofia Sans (Google Fonts). Headings: Newsreader as a stand-in for the main site's licensed "tobiasMedium".
To use the real font, add an `@font-face` for it; it is already first in the `--serif` stack.
