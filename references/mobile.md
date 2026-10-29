# Mobile mode

Rules for mobile app screens and flows. Read with the main SKILL.md.

## Platform first

Pick one and stay with it. Do not mix iOS and Android patterns.

- **iOS:** calm top area, tab bar, native-feeling sheets, restrained chrome.
- **Android:** firmer structure, clear app bar, bottom navigation, Material-like
  sheets and lists.
- **Neutral:** universal patterns, little platform-specific ornament.

Write the choice in `style.md`.

## Screen count and flow

- One screen per image. A flow gets several screens, never one board.
- Onboarding = several screens. Auth = sign in, sign up and recovery when useful.
  "An app" = a real set (e.g. first screen, home, detail, one secondary task).
- Screens must form a believable path: onboarding → auth → home, browse → detail →
  cart → checkout → done. For each screen ask: what tap leads here?
- Vary each screen's top area, image-to-text balance, density and CTA place. Keep
  the product system the same.

## Phone mockup

- By default show each screen in a clean phone frame: iPhone-style for iOS and
  neutral, Android-style for Android. Drop the frame only if the user asks.
- Same device, same size and same position in every image. Even margins on all
  sides; the phone never touches the edge. Soft shadow only.
- The screen content is the star, not the device.
- Several phones in one image: same size, equal gaps, cleanly aligned.

## Real app, not a website in a phone

- Respect the status bar, top bar, bottom navigation, home indicator and gesture
  areas. Nothing important there.
- Use familiar navigation: tab bar for main sections, push for drill-down, sheets
  for side tasks, segmented controls for local switches. Do not overload the tab
  bar.
- One clear main action per screen.

## Text size

Text must never feel small at normal viewing size. If it does, the screen is not
done: cut content, add space, enlarge text, or split it into another screen.

## Richer is fine, messy is not

Mobile screens may be layered and expressive, as long as they stay clean.

- **Texture:** soft grain, paper, light noise, frosted or foggy gradients, blurred
  photo layers. It supports the mood and never hurts text.
- **Image behind text:** fade to transparent, bottom gradient, side mask or soft
  blur so the text stays easy to read. No raw photo under text.
- **Small accents:** a few clean marks — thin orbit lines, dotted arcs, tiny arrows,
  fine grid, small badges. Pick two kinds and use them sparingly.
- **Icons:** a consistent, custom-feeling set with one stroke or fill logic. Not
  plain Lucide-style defaults.

## Style choices

Pick one of each and write it in `style.md`.

- **Theme:** clean light · deep dark · soft wellness neutral · monochrome · rich
  accent · editorial luxe · playful color · calm productivity.
- **Type:** system-like sans · refined grotesk · expressive display + clean body ·
  soft humanist sans · sharp product sans.
- **Structure:** list-led · card-led · overview dashboard · media-led · profile-led
  · shop browse/detail · chat-led · calm wellness blocks.
- **Images:** editorial photos · lifestyle · soft illustration · tactile abstract ·
  product shots · photo + vector · moody backdrops · light collage.
- **Palette:** monochrome + one accent · warm neutral + dark contrast · cool
  mineral + bright accent · cream / charcoal / muted accent · dark + warm accent ·
  soft wellness · bright but balanced · muted with one bold hit.

Pick up to 4 signature components and reuse them, e.g. hero metric card, stat
strip, collection grid, media carousel, profile header, segmented control, bottom
sheet, product card stack, progress ring, chat bubbles, settings groups, sticky
mini player, checkout summary.

## First screen and onboarding

- First screen: one focal point, 1–3 short lines, one clear action. No wall of
  text, no stack of overlapping cards, no "website hero in a phone".
- Onboarding screens must differ in layout, not just icon and headline. Short copy,
  no motivational filler, no early rating prompts.

## By category

- **Fintech:** trust, calm space, clear numbers and transactions, no chart spam.
- **Health / fitness:** clear metrics and progress, airy, optimistic images.
- **Productivity:** list and task clarity, simple navigation, minimal visuals.
- **Social:** profile and feed rhythm, strong media, clear create vs browse.
- **Shop:** strong product photos, fixed card ratios, clean checkout.
- **Wellness / lifestyle:** soft materials, calm type, tactile backgrounds.

## Mobile AI tells

Besides the main 5 mistakes, avoid: huge corner radius on everything, a home screen
of 12 fighting widgets, cloned screens in a flow, empty giant cards, random avatar
rows, decorative toggles, and filler like "smarter than ever" or fake brands like
Quantix and VeloPay.
