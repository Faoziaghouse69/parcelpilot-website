# WORKLOG — ParcelPilot one-page site

One line per slice: what I did -> the command I ran -> what it actually printed.

- Listed the picture folder -> `ls -la Images` -> `logo.jpg`, `logo-dark.jpg`, `Profile.jpg`, `working.jpg`, `speaking.jpg`, `Shot-1.jpg`..`Shot-3.jpg`, `shot-4.jpg`..`shot-6.jpg` (all 11 present; `Images` and `images` are the same folder on this Mac).
- Read the brief's contact block requirement -> searched all project docs (`grep`, `textutil` on both `.docx`) -> no `CONTACT DETAILS` block anywhere; asked the member for WhatsApp, email, name, city, why. Booking link already held.
- Got exact pixel sizes -> `sips -g pixelWidth -g pixelHeight Images/*.jpg` -> speaking/shot-1 1376x768; working/shot-4 896x1200; the rest 1024x1024.
- Created a portable copy of the artwork -> `mkdir -p parcelpilot/images && cp ...` -> 11 lowercase jpg files.
- Built the page -> wrote `parcelpilot/index.html` (one file, inline CSS, inline SVG icons, Fraunces + Inter from Google Fonts).
- Rendered and screenshotted real -> `node /tmp/kilo/shot.js` -> `desktop overflow-check {"scrollW":1440,"clientW":1440,"bodyW":1440}`, `mobile overflow-check {"scrollW":375,"clientW":375,"bodyW":375}` (no sideways scroll at either width).
- Found and fixed a real layout bug -> section screenshots showed the problem/how/about images as narrow vertical slices -> cause: the `height` HTML attribute acted as a CSS presentational hint; added `height:auto` and re-rendered -> all three images now sit at the right size (`desktop-02.png`, `desktop-06.png`, `desktop-08.png`).
- Verified contact links -> `webfetch https://cal.com/...` -> `AI Automation Discovery call | FAOZIA GHOUSE | Cal.com`; `webfetch https://wa.me/97455655253` -> `Chat on WhatsApp with +974 5565 5253`.
- Checked single price and slots -> `grep` -> `Rs 25,000 count: 1`, `[CLIENT QUOTE]` is the only bracket slot.
- Removed the client-quote block (member: first project) -> `grep -c "CLIENT QUOTE" index.html` -> `0`; re-rendered -> `mobile overflow-check {"scrollW":375,"clientW":375,"bodyW":375}`, about section still reads correctly.
