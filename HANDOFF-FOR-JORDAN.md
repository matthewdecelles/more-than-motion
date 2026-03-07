# MTMI Landing Page - Everything You Need

Hi Jordan! Matt built you a landing page for the In-Studio Intensives. This document walks you through everything step by step. You don't need to be technical - just follow along.


## Your Landing Page Is Already Live

**https://more-than-motion.vercel.app**

You can start sending traffic to this URL right now. The form works - when someone fills it out, you'll get an email at info@morethanmotionintensive.com.


---


## STEP 1: Activate Email Notifications (2 minutes)

The form sends applications to your email, but it needs a one-time confirmation.

1. Go to the live site: https://more-than-motion.vercel.app
2. Fill out the form yourself with test info and submit it
3. Check your inbox at **info@morethanmotionintensive.com** for an email from FormSubmit.co
4. Click the confirmation link in that email
5. Done! Every future application will arrive in your inbox automatically

Each email will include: Name, Email, Phone, and what they wrote about their studio.


---


## STEP 2: Add Your Facebook Pixel (5 minutes)

The pixel code is already built into the page - you just need to plug in your Pixel ID so Meta can track who visits and who applies.

1. Go to business.facebook.com > Events Manager
2. Find your Pixel ID (it's a long number, like 123456789012345)
3. You'll need to edit the code file (see "How To Make Changes" below)
4. In the file, press Cmd+F and search for `[YOUR_PIXEL_ID]`
5. You'll find it in 3 places. Replace `[YOUR_PIXEL_ID]` with your actual number in all 3 spots
6. Save and redeploy (instructions below)

What the pixel tracks (already set up):
- **Someone visits the page** - so you can retarget them
- **Someone starts the form** - so you know they're interested
- **Someone submits the form** - so you can track conversions from your ads


---


## STEP 3: Set Up Google Sheets Tracking (10 minutes, optional)

This is optional but recommended. It logs every application to a Google Sheet so you can see them all in one place and track who you've followed up with.

**Create the Sheet:**
1. Go to sheets.google.com and create a new spreadsheet
2. In Row 1, type these column headers:
   - A1: `Timestamp`
   - B1: `Name`
   - C1: `Email`
   - D1: `Phone`
   - E1: `About Studio`

**Add the Script:**
3. In your Google Sheet, click **Extensions** (in the top menu) > **Apps Script**
4. It opens a code editor. Delete everything that's already there
5. Copy and paste this entire block:

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

6. Click the blue **Deploy** button > **New deployment**
7. Next to "Select type", click the gear icon and choose **Web app**
8. Set "Execute as" to **Me**
9. Set "Who has access" to **Anyone**
10. Click **Deploy**
11. It will ask you to authorize - click through the warnings (it's your own script, it's safe)
12. It will show you a URL that starts with `https://script.google.com/macros/...` - **copy that URL**

**Connect It to the Landing Page:**
13. Open the index.html file (see "How To Make Changes" below)
14. Press Cmd+F and search for `window.GOOGLE_SHEETS_URL`
15. Replace that whole line:
    - Old: `var sheetsURL = window.GOOGLE_SHEETS_URL;`
    - New: `var sheetsURL = 'https://script.google.com/macros/s/YOUR_URL_HERE/exec';`
    (paste the URL you copied in step 12)
16. Save and redeploy


---


## How To Use This With Your Squarespace Site

Your Squarespace site stays exactly as it is. This landing page is separate - use it for:
- **Ad traffic** - Point your Facebook/Instagram ads to https://more-than-motion.vercel.app
- **Link in bio** - Use the Vercel URL in your Instagram bio for "Apply for In-Studio"
- **Squarespace button** - Add a button on your Squarespace site that links to the Vercel URL

You don't need to touch your Squarespace site at all. This is a separate page designed specifically for converting ad traffic into applications.


---


## How To Make Changes

You have two options: use AI to help you, or edit manually.

### Option A: Use Claude Code (Recommended - Easiest)

Claude Code is an AI that can edit the site for you. You just tell it what you want in plain English.

**First-time setup (10 minutes):**
1. Open the **Terminal** app on your Mac (search for "Terminal" in Spotlight)
2. Install Claude Code by pasting this and pressing Enter:
   ```
   npm install -g @anthropic-ai/claude-code
   ```
   (If it says npm is not found, first install Node.js from https://nodejs.org - download the LTS version, install it, then try again)

3. Download your project files by pasting this and pressing Enter:
   ```
   cd ~/Desktop && git clone https://github.com/matthewdecelles/more-than-motion.git
   ```
   This creates a folder called "more-than-motion" on your Desktop.

4. Go into the folder:
   ```
   cd ~/Desktop/more-than-motion
   ```

5. Start Claude Code:
   ```
   claude
   ```

6. It will ask you to log in the first time. Follow the prompts.

**Making changes:**
Once Claude Code is running, just type what you want in plain English. Examples:

- "Change the headline to say 'Bring MTMI To Your Studio'"
- "Add a new FAQ question: 'What ages is this for?' with the answer 'Dancers ages 10-18'"
- "Change the testimonial name to Jessica Park from Spark Dance Studio"
- "Swap the Instagram embed for this YouTube video: https://youtube.com/watch?v=xxxxx"
- "Add a new faculty member named Sam Nelson as a Guest Artist"
- "Remove the tour dates section"
- "Deploy the site"

Claude will make the changes and can deploy them for you. Just talk to it like you would a person.

### Option B: Edit Manually

1. Open the "more-than-motion" folder on your Desktop
2. Right-click **index.html** > Open With > TextEdit (or any text editor)
3. Use Cmd+F to find the text you want to change
4. Edit it, save the file
5. To deploy, open Terminal and run:
   ```
   cd ~/Desktop/more-than-motion && npx vercel --prod
   ```


---


## How To Deploy After Making Changes

Every time you make changes, you need to deploy so the live site updates.

**Option 1: From Claude Code** - Just type "deploy the site" and Claude will do it.

**Option 2: From Terminal** - Open Terminal and run:
```
cd ~/Desktop/more-than-motion && npx vercel --prod
```
The first time, it will ask you to log in to Vercel (free account). After that, it just works.

**Option 3: Drag and Drop** - Go to vercel.com/new in your browser and drag the entire "more-than-motion" folder onto the page. It will deploy automatically.


---


## What's In The Folder

```
index.html              - Your entire landing page (the only file that matters)
CLAUDE.md               - Tells Claude Code about your site (don't delete this)
HANDOFF-FOR-JORDAN.md   - This document you're reading
strategy.md             - Growth playbook with ad scripts and follow-up sequences
```


---


## Quick Reference: Common Edits

| What you want to change | Search for this in index.html |
|------------------------|-------------------------------|
| Main headline | `Earn $2,000+` |
| Subtext under headline | `We bring elite faculty` |
| Banner at top | `ONE STUDIO PER CITY` |
| Faculty names | `Kaycee Rice` or `Phil Wright` etc. |
| Testimonial quote | `MTMI handled everything` |
| Testimonial name | `Sarah Mitchell` |
| FAQ questions | `faq-q` |
| FAQ answers | `faq-a` |
| Tour dates | `tour-card` |
| Gallery photos | `gallery-grid` |
| Form heading | `Apply For Your Studio` |
| Facebook Pixel ID | `[YOUR_PIXEL_ID]` |
| Google Sheets URL | `GOOGLE_SHEETS_URL` |


---


## Need Help?

- Text Matt
- Or if you're using Claude Code, just ask it - it knows everything about this site
