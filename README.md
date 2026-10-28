# Khushi — Digital Marketing Portfolio

An editorial, animated one-page portfolio for Khushi (digital marketing and social media, Kolkata). Built with plain HTML, CSS and JavaScript. No framework, build step or dependencies.

## Run it locally

Open `index.html` directly, or serve the folder for a production-like preview:

```powershell
python -m http.server 8080
```

Then visit `http://localhost:8080`.

## Deploy

This is a static site. Upload the whole folder (including `assets/`) to any static host.

- **Netlify** — drag the folder into Netlify Drop. No build command, publish directory is the project root.
- **Vercel** — import the folder or repository. Framework preset: Other. No build command.
- **GitHub Pages** — push the files to a repository, then Settings → Pages → Deploy from branch → root. All paths are relative, so it works from a project subpath.
- **Any hosting/cPanel** — upload the contents to `public_html`.

The enquiry form does not post to a server. It validates the fields and opens WhatsApp with a prefilled message; nothing is stored by the site. If you want enquiries by email instead, connect a form service such as Formspree or Netlify Forms.

## Project map

| Path | Purpose |
| --- | --- |
| `index.html` | All 16 sections, dialogs, hand-written case studies, metrics, packages and contact block |
| `assets/css/styles.css` | Design system, layout, animation and responsive rules |
| `assets/js/content.js` | Editable contact details, projects, showreel and testimonials |
| `assets/js/main.js` | Navigation, reveals, filters, dialogs, counters, form and WhatsApp links |
| `assets/img/` | Supplied client screenshots, portrait and creative artwork |
| `assets/fonts/` | Self-hosted Anton, Instrument Serif and Manrope (woff2) |
| `assets/credits.json` | Image sources and font licence notes |
| `favicon.svg` | KH monogram favicon |

## Editing content

### Contact details

The phone number currently appears in **two kinds of place**:

1. `index.html` — header CTA, contact block, WhatsApp fallback link. Search for `89103`.
2. `assets/js/content.js` — the `contact` object. `whatsappDigits` is what the enquiry form uses to build the WhatsApp message.

Update both and keep the display format and digits consistent. The supplied number `+91 89103 2762` has **nine digits after +91**; confirm the correct 10-digit mobile before publishing.

For the remaining contact fields, edit `contact` in `assets/js/content.js`:

```js
email: "hello@example.com",
instagram: "@yourhandle",
linkedin: "https://www.linkedin.com/in/your-profile",
website: "https://yourwebsite.com"
```

Empty values deliberately show a labelled placeholder ("Add professional email", etc.) instead of a fake link. Social fields accept a bare handle or a full URL. Email must be a full address.

### Projects

Projects live in the `projects` array in `assets/js/content.js`. Cards, filters and the case-study dialog are generated from this data.

- `category` — one or more of `social`, `performance`, `seo`, `creative`, `web`. These match the filter chips in `index.html` (Section 04). Adding a new category also requires a new chip there.
- `stage` — card artwork background: `lavender`, `cobalt`, `ink` or `ivory`.
- `kind` — `client` or `concept`; `kindLabel` is the visible label.
- `thumb`, `thumbW`, `thumbH` — card image and its intrinsic dimensions.
- `media` — array of `{ src, alt, caption }` shown in the case-study dialog. Use relative paths such as `assets/img/your-file.jpg`.
- `results` — leave empty unless the numbers come from an approved client report. `resultNote` explains why results are not shown.

Keep `period` honest. The six client projects currently say **"To be confirmed"** because no engagement dates were supplied.

The four long-form "Selected engagements" articles in Section 11 are **hand-written in `index.html`**, not generated from `content.js`. Update both if a case study changes.

### Testimonials

Add approved quotes to the `testimonials` array in `assets/js/content.js`:

```js
testimonials: [
  {
    quote: "The exact words the client approved.",
    name: "Client name",
    role: "Role",
    business: "Business"
  }
]
```

When the array is non-empty, the carousel replaces the empty state automatically. Publish only with written permission; do not paraphrase or invent quotes.

### Showreel / video

Edit the first item in `videos` in `assets/js/content.js` and set `url`. Supported formats:

- YouTube or YouTube Shorts URL
- Vimeo URL
- Direct `.mp4`, `.webm`, `.ogv` file
- Any embed URL (used in an iframe)

`poster` is the fallback cover image. With `url` empty, the page shows a private-showreel message and a WhatsApp request button rather than claiming a public sample.

### Metrics

Section 05 uses four figures from the supplied Instagram insights screenshots: 44,103,724 views, 13,435,392 accounts reached, 86.4% non-follower share and +48.2% reach growth. The screenshots show a 1 January–31 March reporting window; the year and account are not visible. Confirm both before publishing.

The counters are in `index.html` (search for `data-count`). Each needs the matching visible fallback text so the number still reads correctly without JavaScript:

```html
<span class="metric-value" data-count="44103724">44,103,724</span>
```

Use `data-decimals`, `data-prefix` and `data-suffix` for non-integers. Do not add new performance claims without an approved report. Section 11 is intentionally a results-pending placeholder until reports are cleared for publication.

### Packages

Prices and package names are in Section 15 of `index.html`. The budget select in the contact form is also in `index.html`. Keep the `data-package` values on the "Request proposal" buttons aligned with the select option values. Deliverables and inclusions are intentionally not listed; add them only when confirmed in writing.

### Images and privacy

Client screenshots are used as supplied. Before publishing, confirm client permission and check that no private information (phone numbers, emails, direct messages, customer names) is visible. The screenshots are point-in-time profile views, not growth claims; keep captions accurate.

## Before publishing

- [ ] Confirm the phone number (nine digits after +91 is likely incomplete).
- [ ] Add professional email, Instagram, LinkedIn and website URLs.
- [ ] Confirm client permission for names and screenshots.
- [ ] Confirm project periods, scopes and contributions; current labels say "To be confirmed".
- [ ] Add testimonials only with written approval.
- [ ] Confirm the metric period, account and permission; add no new figures.
- [ ] Add a showreel file/URL, or keep the private-on-request message.
- [ ] Optionally add an `og:image` once the final domain is known.
- [ ] Test the menu, filters, dialogs and WhatsApp form on a phone.

No CV or verified professional history was supplied, so the site deliberately avoids years-of-experience and client-count claims. Add those only when you can substantiate them.

## Design notes

- Palette: warm ivory `#F2EFE7`, cobalt `#2036E8`, lavender `#C7C2F4`, charcoal `#141414`.
- Type: Anton for display, Instrument Serif italic for accents, Manrope for body copy. All fonts are self-hosted.
- Motion: masked headline reveals, scroll-triggered sections, subtle portrait parallax and animated counters. `prefers-reduced-motion` is respected.
- Responsive breakpoints at 1240, 1080, 960, 720 and 420 px.
- Accessibility: skip link, visible focus styles, keyboard-operable menu with focus trap, labelled dialogs, Escape to close, and `aria-live` status for the form.

## Credits

See `assets/credits.json` for image sources and font licence notes. Anton, Instrument Serif and Manrope are licensed under the SIL Open Font License; keep the licence terms with the font files if you redistribute them.
