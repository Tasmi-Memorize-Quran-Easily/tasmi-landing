# tasmi-landing — Build Instructions

This document is the single source of truth for building the public-face static site for Tasmi at **`https://tasmi.cloud`**. It is separate from the backend (`tasmi-auth`) and the iOS app (`tasmi-ios`).

The site exists for three reasons:
1. The **Quran Foundation Request Access form** requires public URLs for Logo, Client URL, Privacy Policy, and Terms of Service.
2. The **Apple App Store** requires a public Privacy Policy URL on submission.
3. It is the public face of Tasmi — a single landing page someone can visit to understand what the app is.

Keep it small. No frameworks. No build step. Plain HTML and CSS that any browser renders directly.

---

## About Tasmi

Tasmi (تسميع) is a Quran memorization companion app for iOS, built for the [Quran Foundation Hackathon (Ramadan 2026)](https://launch.provisioncapital.com/quran-hackathon). The name means *recitation from memory* — the traditional practice of presenting what you've memorized to a teacher for review. Tasmi takes that discipline and turns it into a daily, self-directed habit.

Built by a husband-and-wife team.

---

## Phase 1: Project structure

```
tasmi-landing/
├── index.html       ← landing page
├── privacy.html     ← privacy policy (served at /privacy)
├── terms.html       ← terms of service (served at /terms)
├── styles.css       ← shared styles
├── logo.png         ← app logo, square, at least 512×512
├── favicon.ico      ← browser tab icon
├── README.md
└── .gitignore
```

All files at the root. No `public/`, no `src/`, no `build/`. nginx will serve directly from the project root.

---

## Phase 2: Design principles

- **Clean, readable, calm.** This is a spiritual-practice app — the site should feel like a quiet space, not a SaaS landing page.
- **No frameworks.** No Tailwind CDN, no Bootstrap, no jQuery. Just hand-written HTML and CSS.
- **System font stack.** No custom web fonts unless absolutely needed for Arabic.
- **Max-width container** around 720px for body text — readable line length matters.
- **Mobile-first.** Most visitors will hit this from a phone after seeing the App Store listing.
- **Accessible.** Real semantic HTML (`<main>`, `<article>`, `<nav>`, `<footer>`). Proper heading hierarchy. Alt text on images. Color contrast that passes WCAG AA.

### Color palette

Pick a calm, slightly spiritual palette. Suggested starting point:

- Background: `#fafaf7` (warm off-white)
- Text: `#1a1a1a` (near-black)
- Muted text: `#6b6b6b`
- Accent: `#0f6b5c` (deep teal-green — evokes Islamic geometric art without being cliché)
- Border / dividers: `#e5e5e0`

The team is free to swap these — the principle is *quiet and warm*, not *vibrant and energetic*.

### Typography

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", system-ui, sans-serif;
  font-size: 17px;
  line-height: 1.6;
}
```

For the Arabic word "تسميع" if used in headings, the system font usually renders it well on Apple and modern Android. If it looks broken on testing, add a fallback for Arabic only:

```css
.arabic { font-family: "SF Arabic", "Noto Naskh Arabic", serif; }
```

---

## Phase 3: `index.html` — landing page

Single page. Sections in order:

### Header

- App name **Tasmi** (with Arabic تسميع subtly alongside or above)
- One-line tagline: *A Quran memorization companion*

### Hero / intro (2–3 short paragraphs)

Explain what Tasmi is in plain language. Don't sell — describe.

Sample tone (adjust as needed):

> Tasmi helps you build a Quran memorization habit that lasts beyond Ramadan.
>
> The name comes from the traditional practice of *tasmi'* — reciting what you've memorized to a teacher for review. Tasmi brings that discipline into a daily companion: a structured review system that takes new portions from first reading through long-term retention, so what you memorize stays with you.
>
> Built for the Quran Foundation Hackathon, Ramadan 2026.

### How it works (3–4 short cards or list items)

- **Seven-stage challenges** — a new portion moves through structured stages, from first reading to confident recall.
- **Spaced review** — once memorized, portions return for review at increasing intervals so they don't fade.
- **Synced across devices** — your progress, bookmarks, and streaks follow your Quran Foundation account.
- **Private by design** — no audio recording, no ads, no analytics tracking.

### About the team

One short paragraph: built by a husband-and-wife team for the Quran Foundation Hackathon, Ramadan 2026.

### "Coming soon" / call to action

Not on the App Store yet. A simple line:

> Coming soon to the App Store. For updates, follow the project on GitHub.

Optionally a GitHub link to the org.

### Footer

- Copyright line: © 2026 Tasmi
- Link to `/privacy`
- Link to `/terms`
- Contact email (a real one the team monitors)

---

## Phase 4: `privacy.html` — privacy policy

Plain HTML with the same `styles.css`. Write specifically for what Tasmi actually does — do not paste generic template text. Apple reviewers and Quran Foundation reviewers can both tell.

Sections to cover, in order:

### Introduction
- Effective date.
- What this policy covers.

### Information we collect
- **From Quran Foundation account:** when you sign in, we receive your name, email, and a user identifier from Quran Foundation. We do not receive your password.
- **Memorization progress:** the verses you are working on, your challenge stages, and your review history. Stored locally on your device and synced through your Quran Foundation account.
- **Bookmarks, streaks, goals:** managed through the Quran Foundation user APIs and stored on Quran Foundation servers, linked to your account.

### What we do not collect
- No audio recordings of your recitation.
- No contacts, calendars, photos, or location.
- No advertising identifiers.
- No third-party analytics or tracking SDKs.

### How we use information
- To show you your own memorization progress.
- To sync progress across your devices through your Quran Foundation account.
- We do not sell, rent, or share your data with anyone.

### Third-party services
- **Quran Foundation** — provides authentication and the user data APIs that power sync. Their privacy practices apply to data they store. See `https://quran.foundation/privacy` (or wherever their policy lives — verify and link).
- That's the only third party.

### Data storage and security
- Authentication tokens are stored in the iOS Keychain, encrypted by the OS.
- Local progress data is stored in the app sandbox.
- Synced data lives on Quran Foundation servers.

### Your rights
- **Delete the app:** removes all local data from your device.
- **Delete your Quran Foundation account:** removes synced data. Done through Quran Foundation directly.
- **Access your data:** the app shows everything we have about you. There is no hidden data.

### Children
- Tasmi is suitable for users of all ages.
- We do not knowingly collect data from children under 13 beyond what is required to provide the service.
- Parents can request deletion at any time via the contact email.

### Changes to this policy
- We may update this policy. The effective date at the top will change.
- Material changes will be communicated through the app.

### Contact
- A real email address for privacy questions.

---

## Phase 5: `terms.html` — terms of service

Same `styles.css`. Cover:

### Acceptance
- By using Tasmi, you agree to these terms.

### The service
- Tasmi is a Quran memorization companion. It helps you organize personal memorization and review.
- Tasmi is not a religious authority. It does not replace teachers, scholars, or formal *ijazah*.

### Your account
- Authentication is provided by Quran Foundation. You are responsible for the security of your credentials.

### Acceptable use
- Use Tasmi respectfully and personally.
- Do not attempt to reverse-engineer, abuse the backend, or interfere with service for others.

### Content ownership
- The Qur'anic text, translations, audio recitations, and tafsir are provided through Quran Foundation. All rights to that content belong to their respective owners.
- Your personal memorization data belongs to you.

### Disclaimer
- The service is provided "as-is" without warranty of any kind.

### Limitation of liability
- To the extent permitted by law, we are not liable for indirect, incidental, or consequential damages arising from use of the app.

### Changes to these terms
- We may update these terms. Material changes will be communicated through the app.

### Governing law
- These terms are governed by the laws of Malaysia.

### Contact
- Same email as the privacy policy.

---

## Phase 6: `logo.png`

Square PNG, at least 512×512.

If no real logo exists yet, generate a clean placeholder:
- Solid background in the accent color (`#0f6b5c` teal-green).
- The word "Tasmi" centered, in white, clean sans-serif.
- Or the Arabic "ت" or "تسميع" centered, clean.
- No clip art, no clichés (no mosques, no crescents, no calligraphy stock images).

The logo will appear at small sizes in the Quran Foundation client list — it needs to read clearly at 32×32 px.

Also save a `favicon.ico` (16×16 and 32×32 in one file) — most simple favicon generators handle this from a single PNG.

---

## Phase 7: `styles.css`

One shared stylesheet. Keep it under 200 lines. Suggested skeleton:

```css
:root {
  --bg: #fafaf7;
  --text: #1a1a1a;
  --muted: #6b6b6b;
  --accent: #0f6b5c;
  --border: #e5e5e0;
  --container: 720px;
}

* { box-sizing: border-box; }

html, body {
  margin: 0;
  padding: 0;
  background: var(--bg);
  color: var(--text);
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", system-ui, sans-serif;
  font-size: 17px;
  line-height: 1.6;
}

main {
  max-width: var(--container);
  margin: 0 auto;
  padding: 48px 24px 96px;
}

h1 { font-size: 2rem; margin: 0 0 0.5rem; }
h2 { font-size: 1.4rem; margin: 2.5rem 0 0.5rem; }
h3 { font-size: 1.1rem; margin: 1.5rem 0 0.25rem; }

p { margin: 0 0 1rem; }
a { color: var(--accent); text-decoration: underline; text-underline-offset: 2px; }
a:hover { text-decoration: none; }

.muted { color: var(--muted); }
.arabic { font-family: "SF Arabic", "Noto Naskh Arabic", serif; }

.tagline { color: var(--muted); margin-top: -0.25rem; }

.cards {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
  margin: 24px 0;
}
@media (min-width: 600px) {
  .cards { grid-template-columns: 1fr 1fr; }
}
.card {
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 20px;
  background: white;
}
.card h3 { margin: 0 0 0.25rem; }

footer {
  border-top: 1px solid var(--border);
  margin-top: 64px;
  padding-top: 24px;
  font-size: 0.9rem;
  color: var(--muted);
}
footer a { color: var(--muted); margin-right: 16px; }
```

Adjust freely. The point is *quiet and readable*, not *pixel-perfect to this spec*.

---

## Phase 8: Local preview

No build step needed. Open `index.html` directly in a browser, or run a tiny static server:

```bash
# from project root
python3 -m http.server 8080
```

Visit `http://localhost:8080`.

Test:
- All three pages render.
- Links in the footer work.
- Logo loads.
- Pages look fine on a narrow viewport (drag browser to 375px width).

---

## Phase 9: Deployment

Deploy to the same Ubuntu server as `tasmi-auth`, but on a different nginx vhost serving the root domain `tasmi.cloud`. The nginx config and certbot steps are covered in `INSTRUCTIONS-BACKEND.md` Phase 3 and 4. In short:

```bash
# on the server
sudo mkdir -p /var/www/tasmi-landing
sudo chown -R $USER:www-data /var/www/tasmi-landing
cd /var/www/tasmi-landing
git clone git@github.com:yourusername/tasmi-landing.git .
```

nginx vhost (already in the backend doc, copied here for convenience):

```nginx
server {
    listen 80;
    server_name tasmi.cloud www.tasmi.cloud;
    return 301 https://tasmi.cloud$request_uri;
}

server {
    listen 443 ssl http2;
    server_name tasmi.cloud www.tasmi.cloud;

    ssl_certificate     /etc/letsencrypt/live/tasmi.cloud/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/tasmi.cloud/privkey.pem;

    root /var/www/tasmi-landing;
    index index.html;

    location = /privacy { try_files /privacy.html =404; }
    location = /terms   { try_files /terms.html =404; }
    location /          { try_files $uri $uri/ =404; }
}
```

Then:

```bash
sudo certbot --nginx -d tasmi.cloud -d www.tasmi.cloud
```

Verify:

```bash
curl -I https://tasmi.cloud
curl -I https://tasmi.cloud/privacy
curl -I https://tasmi.cloud/terms
curl -I https://tasmi.cloud/logo.png
```

All four should return 200 with TLS.

---

## Phase 10: Done state

When this document is fully executed:

- `https://tasmi.cloud` renders the landing page over HTTPS.
- `https://tasmi.cloud/privacy` renders the privacy policy.
- `https://tasmi.cloud/terms` renders the terms of service.
- `https://tasmi.cloud/logo.png` returns the logo image.
- All pages are mobile-friendly and pass basic accessibility checks.
- The Quran Foundation Request Access form can be submitted with these URLs.

---

## Out of scope

- Analytics / tracking — intentionally absent
- Newsletter signup — defer
- Blog / changelog — defer
- Multi-language — defer (English only for v1)
- CMS — pure static HTML, edits go through git
- Cookie banner — no cookies are set, so none needed
