# REPORT — ParcelPilot one-page site

Built at `parcelpilot/index.html` (self-contained: `parcelpilot/images/` holds the artwork).

## Status per part

- Contact details gathered before building: DONE
  - evidence: the brief and every project document were searched for a `CONTACT DETAILS` block and none exists; all contact fields were listed and the member answered.
- Pictures listed and placed: DONE
  - evidence: `ls Images` -> all 11 present. Copy -> `parcelpilot/images/` -> 11 files. Every `<img>` has `width`, `height` and alt text.
- Header, hero, problem, services, how it works, about, contact, footer: DONE
  - evidence: rendered at 1440 and 375; screenshots `desktop-00..11.png`, `mobile-00..11.png`.
- Contact links real: DONE
  - evidence: `webfetch https://cal.com/faoziaghouse69/ai-automation-discovery-call` -> `AI Automation Discovery call | FAOZIA GHOUSE | Cal.com`.
  - evidence: `webfetch https://wa.me/97455655253` -> `Chat on WhatsApp with +974 5565 5253`.
  - evidence: `mailto:faoziaghouse@gmail.com?subject=ParcelPilot%20small%20build%20enquiry` is present in the file (a `mailto:` opens the member's own app; it cannot be fetched).
- Phone layout, no sideways scroll: DONE
  - evidence: `mobile overflow-check {"scrollW":375,"clientW":375,"bodyW":375}`.
- Price written once: DONE
  - evidence: `grep -o "Rs 25,000 a project\." index.html | wc -l` -> `1`.
- Client quote: N/A — the member said this is their first project, so the quote block was removed and nothing was invented in its place.
  - evidence: `grep -c "CLIENT QUOTE" index.html` -> `0`.

## What broke and how I fixed it

1. **The `height` attribute was overriding my CSS.** The problem, how-it-works and about images rendered at their intrinsic 1024/1200 px height and `object-fit:cover` cropped them to narrow vertical slices. Read the screenshots, guessed the presentational-hint cause, added `height:auto` to those three rules, re-rendered -> correct sizes. One change, tested with the exact render command.
2. **Header logo showed a white box** on the linen background. Added `mix-blend-mode:multiply` scoped to the header logo only (not the footer, where `logo-dark` sits on navy).
3. **The about photo was ~24% wide**, not "about a third". Changed the about grid to `1.35fr .65fr` -> ~30% of the content width.
4. **Mobile hero photo was too washed out.** Lightened the top of the scrim so the speaking photo reads, kept the lower half opaque behind the text.

## Claims ledger

- "The site is built and renders" -> `node shot.js` produced desktop + mobile screenshots; looked at every section. Verified.
- "No sideways scroll at 375 and 1440" -> overflow-check output above. Verified.
- "Booking link is live" -> webfetch returned the Cal.com page title. Verified.
- "WhatsApp link is live" -> webfetch returned `Chat on WhatsApp with +974 5565 5253`. Verified.
- "Price appears once" -> grep output above. Verified.
- "Two fonts from Google Fonts" -> `<link>` for Fraunces + Inter is in the head. Verified.
- The figures `157`, `$100,000`, `$384,000`, `$15,600` are visible inside `working.jpg` and `shot-4.jpg`. Those numbers are in the member's own supplied photographs, not written by me and not editable here. The page itself states no result, testimonial, client count, response time or timeline.

## Answer to requirement 1 (details used exactly)

- Booking link (held): `https://cal.com/faoziaghouse69/ai-automation-discovery-call`
- WhatsApp as typed: `0097455655253`. Used in the link as `https://wa.me/97455655253` — the `00` international prefix was dropped, because `wa.me` needs country code + digits only (brief, requirement 9). WhatsApp itself confirms the result: `+974 5565 5253`.
- Email: `faoziaghouse@gmail.com`
- Name on the page: `Faozi`
- City: `Qatar and Bengaluru` (about section). The brief's fixed hero line keeps "Qatar and India".
- Why I started: `To help ease the jobs at clinics`
- Client quote: none — this is the member's first project; the quote block was removed at their request.

If the WhatsApp number should read differently, tell me the exact digits and I will change the one link on line 397.

## What I would tell the next person

- Do not deploy this folder as the project root: the `fwai-starter` folder holds `key.txt` and `composio-key.txt`. Deploy `parcelpilot/` on its own.
- The artwork was copied to lowercase `parcelpilot/images/` so paths are case-safe on a Linux host; the originals in `Images/` are untouched.
- Only image `height` attributes needed `height:auto` in CSS when overriding with `aspect-ratio`; watch for this with any new picture.
