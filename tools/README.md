# tools

## og-card.html

Source for `assets/og-card.png`, the 1200x630 social preview card used by
`/get`. It is HTML rather than an image editor so the type stays on-brand:
Inter for Latin and Cairo for Arabic, the same pairing `lib/main.dart` picks
per locale in the app. Arabic needs a real text engine — a naive image
generator draws the letters unjoined and left-to-right.

Regenerate after editing (adjust the paths for your machine):

    chrome --headless --disable-gpu --disable-lcd-text --hide-scrollbars \
      --allow-file-access-from-files --force-color-profile=srgb \
      --force-device-scale-factor=2 --virtual-time-budget=8000 \
      --window-size=1200,630 --screenshot=og-card-2x.png       "file:///absolute/path/to/sadarah-site/tools/og-card.html"

Pass an absolute `file://` URL — headless Chrome reads a bare relative path as
a hostname and renders a DNS error page instead.

Then downsample 2400x1260 -> 1200x630 (Lanczos). Rendering at 2x and scaling
down is what keeps the text crisp; `--disable-lcd-text` avoids the red/blue
subpixel fringing that a normal screenshot bakes into the file.

Bump the `?v=` on the `og:image` URL in `get/index.html` whenever the image
changes — WhatsApp, Facebook and X cache preview images per URL.
