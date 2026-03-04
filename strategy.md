# MORE THAN MOTION INTENSIVE — COMPLETE GROWTH PLAYBOOK

---

## 1. THE OFFER (New Positioning)

**Old positioning:** "We do dance intensives for studios."
That's a commodity. Nobody fills out a form for that.

**New positioning:**
> "We're selecting ONE studio in [City] to receive a $1,000+ credit toward a fully produced dance intensive. We handle everything — faculty, logistics, planning, payments. Your dancers get elite training from industry professionals, and you walk away with profit in your pocket. Studios are applying now. Spots close [date]."

### Why This Works (Hormozi Value Equation)

| Lever | How We Hit It |
|-------|--------------|
| **Dream Outcome** | Your studio becomes #1 in town, dancers get elite training, you make money doing nothing |
| **Perceived Likelihood** | Proof — 150+ studios served, famous faculty, real testimonials |
| **Time Delay** | Low — one application, one call, it's done |
| **Effort & Sacrifice** | Near zero — Jordan handles literally everything |

---

## 2. LANDING PAGE SETUP & CUSTOMIZATION

The landing page is built as a single HTML file (`index.html`). Here's how to customize it:

### Placeholders to Replace

Search the file for `[` brackets — every placeholder is marked. Here's the full list:

| Placeholder | Replace With | Where |
|------------|-------------|-------|
| `[YOUR_PIXEL_ID]` | Your Facebook/Meta Pixel ID (appears 3 times) | `<head>` section |
| `[YOUR_URL_HERE]` | Your landing page URL | Open Graph meta tag |
| `[YOUR_OG_IMAGE_URL_HERE]` | Link to your social share image (1200x630px) | Open Graph meta tag |
| `[YOUR_FORMSPREE_ID]` | Your Formspree form endpoint ID | `<script>` section near bottom |
| `[150+]` | Actual number of studios served | Proof bar |
| `[10K+]` | Actual number of dancers trained | Proof bar |
| `[Top 2]` | Your strongest industry credential | Proof bar |
| `[Faculty Name]` (x3) | Real faculty names | Faculty section |
| `[Notable Credit]` (x3) | Their biggest credits (e.g., "Beyonce World Tour") | Faculty section |
| `[JD]`, `[KR]`, `[MT]` | Faculty initials (or replace div with `<img>` tags) | Faculty avatars |
| `[Replace with real testimonial...]` | Actual studio owner quote | Testimonial section |
| `[Studio Owner Name]` | Real name | Testimonial section |
| `[Studio Name], [City, State]` | Real studio and location | Testimonial section |

### Adding Faculty Photos

Replace the faculty avatar `<div>` with an `<img>` tag:
```html
<!-- Before -->
<div class="faculty-avatar">[JD]</div>

<!-- After -->
<img src="faculty-jordan.jpg" alt="Jordan Davis" class="faculty-avatar"
     style="object-fit:cover">
```

### Adding the Video

Replace the `.video-box` div with an actual embed:
```html
<!-- YouTube -->
<iframe width="100%" style="aspect-ratio:16/9;border-radius:12px;border:1px solid rgba(255,255,255,.08)"
  src="https://www.youtube.com/embed/YOUR_VIDEO_ID"
  frameborder="0" allow="accelerometer;autoplay;clipboard-write;encrypted-media;gyroscope;picture-in-picture"
  allowfullscreen loading="lazy"></iframe>

<!-- Vimeo -->
<iframe src="https://player.vimeo.com/video/YOUR_VIDEO_ID"
  width="100%" style="aspect-ratio:16/9;border-radius:12px;border:1px solid rgba(255,255,255,.08)"
  frameborder="0" allow="autoplay;fullscreen;picture-in-picture"
  allowfullscreen loading="lazy"></iframe>
```

### Adding Jordan's Thank-You Video

In the success state at the bottom of the form, replace the `.video-placeholder` div with an embed (same pattern as above).

### Hosting Options

1. **Squarespace** — Add a "Code Block" and paste the full HTML
2. **Carrd.co** — Use the "Embed" element
3. **Standalone** — Upload `index.html` to any web host (Netlify, Vercel, even GitHub Pages — all free)
4. **Custom domain** — Point your domain to whichever host you choose

**Recommended:** Netlify (free). Drag and drop the file, get a URL in 30 seconds. Then connect your custom domain.

---

## 3. FORM BACKEND SETUP (Formspree)

1. Go to [formspree.io](https://formspree.io) and create a free account
2. Click "New Form" and name it "Studio Applications"
3. Copy the form ID (looks like `xabcdefg`)
4. In `index.html`, search for `[YOUR_FORMSPREE_ID]` and replace with your ID
5. That's it — every application will email you immediately with the applicant's name, email, phone, and pitch

**Free tier:** 50 submissions/month. If you need more, upgrade ($8/mo for 1,000).

---

## 4. CAL.COM SETUP (Calendar Booking)

The landing page has a placeholder calendar mock. Here's how to replace it with a real Cal.com booking widget:

### Step 1: Create Your Account
1. Go to [cal.com](https://cal.com) and sign up (free)
2. Connect your Google Calendar (or Apple/Outlook)
3. Set your availability (e.g., Mon-Fri 10am-4pm)

### Step 2: Create an Event Type
1. Click "Event Types" → "New Event Type"
2. Name: "Studio Intensive Call"
3. Duration: 15 minutes
4. Description: "Quick call with Jordan to customize your studio's intensive"
5. Set your available hours
6. Enable "Requires confirmation" if you want to screen bookings

### Step 3: Get the Embed Code
1. Go to your event type → click "Embed"
2. Choose "Inline Embed"
3. Copy the embed code

### Step 4: Replace the Placeholder
In `index.html`, find the `<div class="cal-placeholder">` section in Step 5 of the form. Replace the entire div with Cal.com's embed code. Wrap it in a container to maintain styling:

```html
<!-- Replace the entire cal-placeholder div with this -->
<div style="margin-top:16px;border-radius:12px;overflow:hidden">
  <!-- Paste Cal.com inline embed code here -->
</div>
```

### Step 5: Style It
Add this CSS to make Cal.com match the dark theme:
```html
<style>
  /* Cal.com dark theme override */
  :root {
    --cal-brand: #D4A843 !important;
  }
</style>
```

---

## 5. FACEBOOK/META PIXEL SETUP

1. Go to [Meta Business Suite](https://business.facebook.com) → Events Manager
2. Click "Connect Data Sources" → "Web" → "Meta Pixel"
3. Name it "More Than Motion" and create
4. Copy your Pixel ID (a number like `123456789012345`)
5. In `index.html`, replace all 3 instances of `[YOUR_PIXEL_ID]`

### Events Being Tracked

The page automatically fires these pixel events:

| Event | When | Why |
|-------|------|-----|
| `PageView` | Page loads | Track all visitors |
| `Lead` | Step 1 completed (name entered) | Track form starts |
| `CompleteRegistration` | Step 4 completed (application submitted) | Track full applications |
| `Schedule` | Call booked | Track bookings |

This lets you create custom audiences and optimize ads for "CompleteRegistration" events.

---

## 6. THANK-YOU / CONFIRMATION EXPERIENCE

After they book a call, the page shows:

1. **Checkmark animation** — visual confirmation it worked
2. **"You're All Set!"** heading — removes any doubt
3. **Jordan's video placeholder** — record a 30-second selfie video saying:
   > "Hey! I just got your application — I'm SO excited. I'm going to review everything and I'll see you on our call. In the meantime, check out what we've been doing on Instagram. Can't wait to talk!"
4. **Instagram follow button** — links to @morethanmotionintensive

**This page alone will dramatically increase call show rates.** The video makes Jordan a real person, not a form.

---

## 7. JORDAN'S CALL SCRIPT

### Opening — Build Rapport (2 min)
> "Hey [Name]! Thanks for applying — I was looking at your studio and I love what you guys are doing. Tell me a little about your studio and your dancers."

### Discovery — Understand Their Situation (5 min)
- "How many dancers do you have?"
- "Have you done intensives before? How did those go?"
- "What's the biggest thing you want for your dancers right now?"
- "If we could put on the perfect intensive for your studio, what would that look like?"

### Present the Vision — Paint the Picture (5 min)
> "Based on what you're telling me, here's what I'm thinking..."

Walk them through the customized intensive:
- Faculty picks that match their style
- Format (1 day vs 2-3 days)
- What the experience would look like
- Drop faculty names and credits
- "Your dancers are going to be posting about this for months. The other studios in [area] are going to notice."

### Handle the Money Conversation (3 min)
> "Here's the best part — you're not paying for this out of pocket. Your dancers pay for the intensive, we handle all the payment collection, and you walk away with profit."

- "Studios our size typically make between $1,000 and $5,000 depending on format and number of dancers."
- "The $1,000 credit we're offering right now comes off the top, so your margins are even better."

### Close — Create Urgency (2 min)
> "We're only doing this with one studio in [City], and I've had a few other applications come in. I'd love to lock this in for you — what dates would work best for your studio?"

If they hesitate:
> "Totally understand — what questions do you have?"

Then answer and re-close.

---

## 8. FOLLOW-UP TEXT SEQUENCES

### If They Apply But Don't Answer the Call

**1 hour later:**
> "Hey [Name]! It's Jordan from More Than Motion. Just saw your application — super excited about your studio. When's a good time for a quick 10-min call?"

**24 hours later:**
> "Hey! Didn't want you to miss this — we're finalizing our [City] studio pick this week. Let me know if you have 10 minutes today or tomorrow."

**48 hours later:**
> "Last reach out! We're making our final decision for [City] soon. If you're still interested, shoot me a time and I'll make it work."

### After the Call (If They Don't Close on the Spot)

**Same day:**
> "So great talking with you! I'm going to hold your spot for a few days — just let me know when you're ready to lock in dates."

**2 days later:**
> "Hey [Name] — quick heads up, I've been getting more applications from studios in [City/area]. I'd love to work with you guys first. Want to hop on a quick call to finalize?"

---

## 9. AD HOOKS & CREATIVE

### Set 1 — The Exclusive Offer (Target: Studio Owners)

1. "We're picking ONE dance studio in [City] and giving them $1,000 toward a full intensive. Is it yours?"
2. "One studio in [City] is about to get an unfair advantage. Apply before your competitor does."
3. "We're looking for ONE studio in [City] to partner with. We bring the faculty, handle everything, and you make money. Apply free."
4. "Your competitor in [City] just saw this ad too. The question is who applies first."

### Set 2 — The Dancer Angle (Target: Competitive Dancers 15-22)

1. "Tag your studio owner — this could be YOUR studio's chance to train with [Faculty Name]."
2. "Imagine getting to train with [Faculty Name] at YOUR home studio. We're making it happen for one studio in [City]."
3. "If your studio got picked for this, you'd literally never want to leave. Send this to your studio owner."
4. "POV: Your studio owner applied and now [Famous Faculty] is coming to teach at YOUR studio."

### Set 3 — The Results/Proof Angle

1. "This is what happens when we bring our faculty into a studio for one day..." [cut to highlight reel]
2. "This studio made $3,000 and their dancers had the best experience of their year. Here's how." [testimonial clip]
3. "Studio owners: what if you could make money AND give your dancers elite training without doing any of the work?"

### Set 4 — Problem/Agitation

1. "Tired of planning intensives yourself, hiring faculty, chasing payments, and barely breaking even? We do all of that — and you profit."
2. "If your studio's intensive looks the same every year, your dancers are going to notice. Let us change that."
3. "Other studios in your area are leveling up. Are you?"

### Ad Setup Recommendations
- **Platform:** Meta (Instagram + Facebook)
- **Budget:** $200/week per city to start
- **Targeting for Set 1:** Interest-based (dance studio owners, dance education) + geo-targeted to specific metro area
- **Targeting for Set 2:** Age 15-22, interests in competitive dance, dance teams + geo-targeted
- **Format:** Reels/Stories (vertical video) for dancer angle, Feed for studio owner angle
- **Optimization:** Optimize for "CompleteRegistration" conversion event once you have 50+ page views

---

## 10. OPEN GRAPH IMAGE

Create a 1200x630px image for link sharing. It should include:
- Dark background matching the site
- "We're Picking ONE Studio in Your City" headline
- The gold accent color
- More Than Motion branding

**Tools:** Canva (free) with a custom 1200x630 template. Export as PNG.

Upload it to your hosting and replace `[YOUR_OG_IMAGE_URL_HERE]` in the HTML.

---

## 11. EXECUTION PRIORITY (Do This In Order)

### Week 1: Foundation
- [ ] **Set up Cal.com** — Create account, connect calendar, set availability, create "Studio Intensive Call" event type
- [ ] **Set up Formspree** — Create account, create form, get endpoint ID
- [ ] **Set up Meta Pixel** — Create pixel in Business Suite, copy ID
- [ ] **Customize the landing page** — Replace all placeholders with real content
- [ ] **Record Jordan's thank-you video** — 30 seconds, selfie-style, genuine excitement
- [ ] **Replace the Cal.com placeholder** — Swap mock calendar with real embed
- [ ] **Host the page** — Upload to Netlify/Vercel/Squarespace, connect domain
- [ ] **Test everything** — Submit a test application, verify email notification, test booking flow on mobile

### Week 2: Launch
- [ ] **Run Ad Set 1** — Exclusive offer angle targeting studio owners in ONE city, $200/week, geo-targeted
- [ ] **Set up follow-up text templates** — Copy sequences into phone notes for quick access
- [ ] **Call every application within 1 hour** — Speed to lead matters more than anything
- [ ] **Track results** — How many views, applications, calls booked, calls completed, studios closed

### Week 3: Optimize
- [ ] **Launch Ad Set 2** — Dancer angle, same city, $200/week
- [ ] **Add real testimonials** — After first successful intensive, get a video testimonial from the studio owner
- [ ] **Review metrics** — Cost per application, application-to-call rate, call-to-close rate
- [ ] **Adjust ads** — Kill underperformers, scale winners

### Week 4+: Scale
- [ ] **Duplicate for City #2** — Same page, same ads, new geo-target
- [ ] **Build an ad creative library** — Record content at every intensive for future ads
- [ ] **Consider automation** — Once volume justifies it, add CRM (HubSpot free) or Zapier for auto-texts

---

## 12. KEY METRICS TO TRACK

| Metric | Target | How to Track |
|--------|--------|-------------|
| Cost per page view | < $1 | Meta Ads Manager |
| Page view → Application rate | > 15% | Formspree submissions / Pixel PageViews |
| Application → Call booked rate | > 60% | Manual tracking |
| Call booked → Call show rate | > 80% | Manual tracking (Jordan's video helps here) |
| Call → Close rate | > 40% | Manual tracking |
| Cost per closed studio | < $200 | Total ad spend / studios closed |

---

*Built for More Than Motion Intensive. Execute in order. Don't overthink it — speed beats perfection.*
