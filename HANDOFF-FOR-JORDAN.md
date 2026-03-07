# MTMI Landing Page - Everything You Need

Hi Jordan! Matt built you a high-converting landing page for the In-Studio Intensives. This document walks you through everything step by step. You don't need to be technical - just follow along.


## Your Landing Page Is Already Live

**https://more-than-motion.vercel.app**

You can start sending traffic to this URL right now. The form works - when someone fills it out, you'll get an email at info@morethanmotionintensive.com.


---


## SETUP CHECKLIST

Do these in order. Total time: about 30 minutes.


### 1. Activate Email Notifications (2 minutes)

The form sends applications to your email, but it needs a one-time confirmation.

1. Go to the live site: https://more-than-motion.vercel.app
2. Fill out the form yourself with test info and submit it
3. Check your inbox at **info@morethanmotionintensive.com** for an email from FormSubmit.co
4. Click the confirmation link in that email
5. Done! Every future application lands in your inbox automatically

Each email includes: Name, Email, Phone, and what they wrote about their studio.


---


### 2. Put The Landing Page On Your Domain (10 minutes)

Right now the page lives at more-than-motion.vercel.app. Let's put it on your actual domain so it feels like part of your site. The best approach is a subdomain like:

**apply.morethanmotionintensive.com**

This keeps your Squarespace site untouched and gives the landing page its own clean URL on your domain.

**Step 1: Add the subdomain in your domain registrar**

Your domain is probably managed through Squarespace Domains, Google Domains, GoDaddy, or Namecheap. Find where you manage DNS records and add:

- **Type:** CNAME
- **Name/Host:** `apply`
- **Value/Points to:** `cname.vercel-dns.com`

(If you're not sure where your domain is managed, check Squarespace: Settings > Domains > click your domain > DNS Settings)

**Step 2: Add the domain in Vercel**

1. Go to https://vercel.com and create a free account (or log in)
2. You should see the "more-than-motion" project
3. Click on it > Settings > Domains
4. Type in `apply.morethanmotionintensive.com` and click Add
5. It may take a few minutes to verify - Vercel will show a green checkmark when it's ready

Now your landing page lives at **apply.morethanmotionintensive.com** and you can use that URL in all your ads and links.


---


### 3. Set Up Facebook Pixel On EVERYTHING (10 minutes)

You want the same Pixel tracking visitors across your entire Squarespace site AND the landing page. This way Meta can see the full picture - someone browses your site, sees an ad later, clicks to the landing page, and applies. One Pixel tracks it all.

**First, find your Pixel ID:**
1. Go to business.facebook.com > Events Manager
2. Your Pixel ID is a long number like `123456789012345` - copy it

**Add the Pixel to your Squarespace site (covers all your Squarespace pages):**
1. In Squarespace, go to **Settings** > **Marketing** > **Facebook Pixel & Conversions API**
2. Paste your Pixel ID
3. Click Save
4. Done - every page on your Squarespace site now has the Pixel

**Add the Pixel to the landing page:**
1. Open the index.html file (see "How To Make Changes" below)
2. Press Cmd+F and search for `[YOUR_PIXEL_ID]`
3. You'll find it in **3 places**. Replace `[YOUR_PIXEL_ID]` with your actual Pixel ID number in all 3 spots
4. Save and redeploy (see "How To Deploy" below)

What the landing page pixel tracks (already built in):
- **PageView** - someone visits the page (for retargeting)
- **Lead** - someone starts filling out the form
- **CompleteRegistration** - someone submits the full application (for conversion tracking)


---


### 4. Set Up Google Sheets Tracking (10 minutes, optional but recommended)

This logs every application to a Google Sheet so you can track everything in one place - who applied, when, and whether you've followed up.

**Create the Sheet:**
1. Go to sheets.google.com and create a new spreadsheet
2. Name it something like "MTMI Studio Applications"
3. In Row 1, type these column headers:
   - A1: `Timestamp`
   - B1: `Name`
   - C1: `Email`
   - D1: `Phone`
   - E1: `About Studio`
   - F1: `Followed Up?` (this one is for you to track manually)

**Add the Script:**
4. In your Google Sheet, click **Extensions** (top menu bar) > **Apps Script**
5. A new tab opens with a code editor. Delete everything that's already there
6. Copy and paste this entire block:

```
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = JSON.parse(e.postData.contents);
  sheet.appendRow([
    new Date(),
    data.Name || '',
    data.Email || '',
    data.Phone || '',
    data['About Studio'] || ''
  ]);
  return ContentService.createTextOutput('OK');
}
```

7. Click the blue **Deploy** button (top right) > **New deployment**
8. Click the gear icon next to "Select type" and choose **Web app**
9. Set "Execute as" to **Me**
10. Set "Who has access" to **Anyone**
11. Click **Deploy**
12. It will ask you to authorize - click "Review permissions", pick your Google account, click "Advanced" > "Go to (project name)", then "Allow"
13. You'll see a URL that starts with `https://script.google.com/macros/...` — **copy that entire URL**

**Connect It to the Landing Page:**
14. Open the index.html file
15. Press Cmd+F and search for `window.GOOGLE_SHEETS_URL`
16. Replace that line:
    - Delete: `var sheetsURL = window.GOOGLE_SHEETS_URL;`
    - Type: `var sheetsURL = 'PASTE_YOUR_URL_HERE';`
    (paste the URL you copied between the quote marks)
17. Save and redeploy

Now every application automatically appears as a new row in your spreadsheet.


---


## How To Use This With Your Squarespace Site

Your Squarespace site stays exactly as it is. Nothing changes there. Here's how to connect them:

**For ads:** Point all Facebook/Instagram ad traffic to `apply.morethanmotionintensive.com` (or the Vercel URL until you set up the subdomain)

**On your Squarespace site:** Add a button or menu link that says "Apply for In-Studio" and link it to your landing page URL

**In your Instagram bio:** Add the landing page URL as your "Apply" link

**The Pixel ties it all together:** Because the same Pixel ID is on both your Squarespace site and the landing page, Meta sees the full visitor journey across both.


---


## How To Make Changes

You have two options: use AI to help you, or edit manually.

### Option A: Use Claude Code (Recommended)

Claude Code is an AI assistant that can edit your site for you. You talk to it in plain English and it makes the changes.

**First-time setup (10 minutes):**

1. Open the **Terminal** app on your Mac (press Cmd+Space, type "Terminal", press Enter)

2. Install Node.js if you don't have it:
   - Go to https://nodejs.org
   - Click the big green "LTS" download button
   - Open the downloaded file and follow the installer

3. Install Claude Code - paste this into Terminal and press Enter:
   ```
   npm install -g @anthropic-ai/claude-code
   ```

4. Download your project files - paste this into Terminal and press Enter:
   ```
   cd ~/Desktop && git clone https://github.com/matthewdecelles/more-than-motion.git
   ```
   This creates a folder called "more-than-motion" on your Desktop.

5. Go into the folder and start Claude:
   ```
   cd ~/Desktop/more-than-motion && claude
   ```

6. It will ask you to log in the first time. Follow the prompts.

**Once Claude Code is running, just tell it what you want:**

- "Change the headline to say 'Bring MTMI To Your Studio'"
- "Add a new FAQ: 'What ages is this for?' with answer 'Dancers ages 10-18'"
- "Replace the testimonial with a quote from Jessica Park at Spark Dance Studio"
- "Swap the Instagram embed for this YouTube video: [paste URL]"
- "Add a new faculty member named Sam Nelson as a Guest Artist"
- "Remove the tour dates section"
- "Add my Facebook Pixel ID: 123456789"
- "Deploy the site"

Claude already knows everything about your site. Just talk to it like a person.

**To come back later and make more changes:**
1. Open Terminal
2. Paste: `cd ~/Desktop/more-than-motion && claude`
3. Tell it what you want to change


### Option B: Edit Manually

1. Open the "more-than-motion" folder on your Desktop
2. Right-click **index.html** > Open With > TextEdit (or any text editor)
3. Use Cmd+F to search for the text you want to change
4. Edit it and save the file
5. Deploy (see below)


---


## How To Deploy After Making Changes

Every time you make a change, you need to deploy so the live site updates.

**From Claude Code:** Just type "deploy the site" and it handles everything.

**From Terminal:**
```
cd ~/Desktop/more-than-motion && npx vercel --prod
```

**Drag and drop:** Go to vercel.com/new in your browser and drag the entire "more-than-motion" folder from your Desktop onto the page.


---


## Quick Reference: Common Edits

| What you want to change | Search for this in index.html |
|------------------------|-------------------------------|
| Main headline | `Earn $2,000+` |
| Subtext under headline | `We bring elite faculty` |
| Top banner text | `ONE STUDIO PER CITY` |
| Faculty names | `Kaycee Rice`, `Phil Wright`, etc. |
| Testimonial quote | `MTMI handled everything` |
| Testimonial person | `Sarah Mitchell` |
| FAQ questions/answers | `faq-q` and `faq-a` |
| Tour dates/cities | `tour-card` |
| Gallery photos | `gallery-grid` |
| Form heading | `Apply For Your Studio` |
| Facebook Pixel ID | `[YOUR_PIXEL_ID]` (3 places) |
| Google Sheets URL | `GOOGLE_SHEETS_URL` |


---


## What's In The Folder

| File | What it is |
|------|-----------|
| index.html | Your entire landing page (this is the one that matters) |
| CLAUDE.md | Tells Claude Code about your site (don't delete) |
| HANDOFF-FOR-JORDAN.md | This document |
| strategy.md | Growth playbook with ad hooks, call scripts, follow-up sequences |


---


## Need Help?

- Text Matt
- Or if you're in Claude Code, just ask it - it knows everything about this site
