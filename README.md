# CoFold Summit Website

Static conference website for the **CoFold Summit**, an annual gathering on open-source co-folding methods in structural biology and drug discovery. Organized by the OpenFold Consortium and hosted by OMSF.

Deployed at **cofold.org** via GitHub Pages.

---

## Tech Stack

- Plain HTML + CSS — no build step, no framework
- [Bootstrap 5.1.3](https://getbootstrap.com/) for grid and components
- [Font Awesome 5](https://fontawesome.com/) for icons
- Google Fonts: Abril Fatface (headings), Nunito Sans (body)
- Hosted on GitHub Pages (see `CNAME`)

---

## File Structure

```
cofold/
├── index.html              # Entire site (single page)
├── custom.css              # All custom styles and theme variables
├── CNAME                   # GitHub Pages custom domain
└── assets/
    ├── images/
    │   ├── speaker-placeholder.svg   # Fallback shown when a speaker photo is missing
    │   ├── omsf-teal.svg             # OMSF logo (teal, sourced from omsf/omsf.github.io)
    │   ├── omsf.png                  # OMSF logo (original green, kept for reference)
    │   ├── sponsor-amd.png           # AMD sponsor logo
    │   ├── sponsor-apheris.png       # Apheris sponsor logo
    │   └── sponsor-sandbox.png       # SandboxAQ sponsor logo
    ├── speakers/
    │   └── firstname-lastname.jpg    # Speaker headshots (conference photos)
    ├── venue/
    │   ├── hero-bg.jpg               # Hero section background (group waving photo)
    │   ├── group-photo.jpg           # Featured group photo in gallery
    │   ├── group-photo-2.jpg         # Alternate group photo
    │   ├── venue1-3.jpg              # Venue/courtyard photos
    │   ├── session1-2.jpg            # Session-in-progress photos
    │   └── networking.jpg            # Reception/networking photo
    └── openFold-logo/                # OpenFold brand assets (black/blue/white, png/svg)
```

---

## Updating for Next Year's Summit

### Changing the Year / Location

Search `index.html` for the current year (`2026`) and city (`Barcelona`) and update all occurrences. Key spots:

- Hero badge: `May 2026 · Barcelona, Spain`
- About section paragraph: `The 2026 CoFold Summit featured...`
- Agenda subtitle
- Gallery group photo alt text
- Footer copyright year

### Adding / Replacing Speakers

1. Drop the headshot into `assets/speakers/` using the naming convention `firstname-lastname.jpg` (lowercase, hyphens, no spaces).
2. In `index.html`, find the speaker's `<img>` tag and update the `src` to match.
3. Each speaker card follows this pattern:

```html
<div class="col-sm-6 col-md-4 col-lg-3">
  <div class="speaker-card h-100 text-center p-4">
    <div class="speaker-photo-md mx-auto mb-3">
      <img src="./assets/speakers/firstname-lastname.jpg" alt="Full Name"
           onerror="this.onerror=null;this.src='./assets/images/speaker-placeholder.svg'">
    </div>
    <h5 class="mb-1">Full Name</h5>
    <p class="text-muted small mb-0">Affiliation</p>
    <a href="https://www.linkedin.com/in/handle/" target="_blank" rel="noopener"
       class="linkedin-link" aria-label="Full Name on LinkedIn">
      <i class="fab fa-linkedin"></i>
    </a>
  </div>
</div>
```

The `onerror` attribute automatically falls back to `speaker-placeholder.svg` if a photo file is missing — so it's safe to add a speaker card before the photo is ready.

### Adding Talk Titles Back

Talk titles were removed for 2026 (titles weren't available in time). To add them back for a future year, insert this line inside each speaker card, between the affiliation and the LinkedIn link:

```html
<p class="talk-title">"Talk Title Here"</p>
```

The `.talk-title` CSS class is already defined in `custom.css` (blue, italic).

### Updating the Agenda

The agenda is a standard HTML `<table>` inside the `#agenda` section. Each session block starts with a full-width header row:

```html
<tr>
  <td colspan="4" class="fw-bold text-white"
      style="background:linear-gradient(90deg,#1a3a5c,#2f9ddb);...">
    Session N — Title
  </td>
</tr>
```

Row types are styled via CSS classes:
| Class | Used for |
|---|---|
| `row-talk` | Individual speaker talks |
| `row-panel` | Panel discussion rows |
| `row-break` | Coffee breaks and lunch |
| `row-opening` | Session chair welcome rows |

### Updating Sponsor Logos

Drop new logo files into `assets/images/` and update the image `src` attributes in the **Sponsored By** section near the bottom of `index.html`. Current sponsors: AMD, Apheris, SandboxAQ.

### Updating the Hero Background

Replace `assets/venue/hero-bg.jpg` with the new photo. The image is displayed with `object-fit: cover` and a dark overlay — portrait or landscape both work, but photos with a clear focal point in the upper half look best (controlled by `background-position: center top` in `custom.css`).

### Updating Organizer Photos

Organizer headshots follow the same naming convention as speakers and live in `assets/speakers/`. Current organizers and their files:

| Person | File |
|---|---|
| Woody Sherman | `woody-sherman.jpg` |
| Mallory Tollefson | `mallory-tollefson.jpg` |
| Felicitas Von Peter | `felicitas-von-peter.svg` (OMSF icon placeholder — replace with photo when available) |
| Karmen Condic-Jurkic | `karmen-condic-jurkic.jpg` |

---

## Styling Notes

All theme colors are defined as CSS custom properties at the top of `custom.css`:

```css
:root {
  --cf-blue:  #2f9ddb;   /* Primary blue — buttons, accents, links */
  --cf-dark:  #0d1b2a;   /* Near-black — navbar, hero background */
  --cf-navy:  #1a3a5c;   /* Navy — gradient headers */
  --cf-light: #f8f9fa;   /* Off-white — alternate section backgrounds */
  --cf-text:  #3a3a3a;   /* Body text */
}
```

The base font size is set to `20px` on `html` and `body`, which scales all `rem`-based values throughout both this stylesheet and Bootstrap. To adjust the overall text size, change these two values together in `custom.css`.

---

## Deployment

The site deploys automatically to **cofold.org** via GitHub Pages whenever changes are pushed to the `main` branch. No build step is needed — just push and the live site updates within a minute or two.
