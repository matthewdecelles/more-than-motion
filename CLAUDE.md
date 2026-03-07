# More Than Motion Intensive - Landing Page

## What This Is
A single-page landing page for MTMI's In-Studio Intensives program. The entire site is one file: `index.html`. No frameworks, no build step, no dependencies.

## Live URL
https://more-than-motion.vercel.app

## How To Run Locally
Just open `index.html` in a browser. No server needed.

## How To Deploy
```bash
npx vercel --prod
```
If Vercel CLI isn't installed, it will prompt to install automatically. Just say yes.

## Site Structure
Everything is in `index.html`:
- HTML structure
- CSS styles (in a `<style>` tag)
- JavaScript (in a `<script>` tag at the bottom)

## Page Sections (in order)
1. **Urgency bar** — fixed gold banner at top: "ONE STUDIO PER CITY. APPLY NOW."
2. **Hero** — headline, subtext, multi-step application form
3. **Credits banner** — trust badges (Beyonce, Justin Bieber, Tate McRae, Nicki Minaj, DWTS, SYTYCD)
4. **Photo gallery** — 4 real photos from MTMI events (hosted on Squarespace CDN)
5. **2026 Tour dates** — 4 cities, 3 sold out (social proof)
6. **Video/Instagram embed** — embedded Instagram post (can be swapped for YouTube)
7. **Benefits** — 4-card grid: Elite Faculty, We Handle Everything, On-Camera Experience, You Profit
8. **How it works** — 3 steps: Apply, We Contact You, We Show Up
9. **Faculty** — grid of guest artists and faculty members
10. **Testimonial** — studio owner quote
11. **FAQ** — accordion with 4 questions
12. **Final CTA** — bottom application form
13. **Footer**
14. **Sticky mobile CTA** — appears when hero scrolls out of view

## Multi-Step Form
The application form has 4 steps:
1. First name + last name
2. Email
3. Phone number
4. Tell us about your studio

On submit, data goes to:
- **Email**: FormSubmit.co sends to info@morethanmotionintensive.com
- **Google Sheets**: Optional — needs Apps Script URL configured (see HANDOFF-FOR-JORDAN.md)

## Design System
- **Colors**: Dark theme with gold accents. Gold = `#D4A843`
- **Fonts**: General Sans (headings), Inter (body) — loaded from Google Fonts
- **Animations**: Subtle fade-up on scroll using IntersectionObserver
- **Mobile**: Fully responsive, optimized for phone screens

## Key CSS Variables
```
--gold: #D4A843
--gold-light: #E8C96A
--gold-dark: #B8922F
--black: #0a0a0a
--white: #ffffff
```

## Facebook Pixel
Pixel code is in the `<head>` but needs a real Pixel ID. Search for `[YOUR_PIXEL_ID]` and replace with the actual ID (3 places).

Events tracked:
- PageView (on load)
- Lead (form step 1 complete)
- CompleteRegistration (form submitted)

## Google Sheets Setup
Search for `window.GOOGLE_SHEETS_URL` in the script section. Replace with the deployed Apps Script URL. Full setup instructions in HANDOFF-FOR-JORDAN.md.

## Making Changes
- To change any text, just find and edit it in the HTML
- To swap photos, change the `src` URLs in the gallery section
- To swap the Instagram embed for a YouTube video, replace the `<blockquote>` block with an `<iframe>` (instructions are in a code comment above that section)
- To add/remove FAQ items, copy/modify the `.faq-item` blocks
- To add/remove faculty, copy/modify the `.faculty-card` blocks
- To update tour dates, edit the `.tour-card` blocks
- Always deploy after changes: `npx vercel --prod`

## Important Files
- `index.html` — the entire landing page
- `CLAUDE.md` — this file (instructions for Claude)
- `HANDOFF-FOR-JORDAN.md` — setup instructions for Jordan
- `strategy.md` — growth playbook (ad hooks, call scripts, follow-up sequences)

## Contact
- Jordan: info@morethanmotionintensive.com
- Cassie: cassie@morethanmotionintensive.com
- Instagram: @morethanmotionintensive
- Main site (Squarespace): https://www.morethanmotionintensive.com
