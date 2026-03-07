# More Than Motion - Landing Page Handoff

Hi Jordan! Here's everything you need to use and manage your new landing page.

## What You Have

A high-converting landing page for MTMI In-Studio Intensives. It lives at:
**https://more-than-motion.vercel.app**

Right now, every form submission emails **info@morethanmotionintensive.com** with the applicant's name, email, phone, and studio info.


## 3 Things You Need To Set Up

### 1. Activate Email Notifications (2 minutes)

The first time someone submits the form, you'll get a confirmation email at **info@morethanmotionintensive.com** from FormSubmit.co. **Click the confirmation link** in that email. After that, every new application goes straight to your inbox automatically.

Each email includes:
- Name
- Email
- Phone
- About their studio


### 2. Set Up Google Sheets Tracking (10 minutes)

This logs every application to a Google Sheet so you can track everything in one place.

**Step 1:** Create a new Google Sheet. Name the columns in Row 1:
```
A1: Timestamp | B1: Name | C1: Email | D1: Phone | E1: About Studio
```

**Step 2:** Go to Extensions > Apps Script

**Step 3:** Delete everything in the editor and paste this:

```javascript
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

**Step 4:** Click Deploy > New Deployment
- Type: Web app
- Execute as: Me
- Who has access: Anyone
- Click Deploy
- Authorize it when prompted (click through any "unsafe" warnings - it's your own script)
- Copy the URL it gives you

**Step 5:** In your landing page code (index.html), find this line near the bottom:
```
var sheetsURL = window.GOOGLE_SHEETS_URL;
```
Replace it with your actual URL:
```
var sheetsURL = 'https://script.google.com/macros/s/YOUR_ID_HERE/exec';
```

Deploy again and you're done. Every application will appear as a new row in your sheet.


### 3. Set Up Facebook Pixel (5 minutes)

The pixel code is already in the page - you just need to add your Pixel ID.

**Step 1:** Go to Meta Events Manager (business.facebook.com > Events Manager)

**Step 2:** Copy your Pixel ID (it's a long number like 123456789012345)

**Step 3:** In index.html, find these 3 lines and replace `[YOUR_PIXEL_ID]` with your actual ID:
```
fbq('init','[YOUR_PIXEL_ID]');
```
and
```
src="https://www.facebook.com/tr?id=[YOUR_PIXEL_ID]&ev=PageView&noscript=1"
```

The pixel already tracks these events:
- **PageView** - when someone lands on the page
- **Lead** - when someone enters their name (step 1)
- **CompleteRegistration** - when someone submits the full application

These events let you build retargeting audiences and track ad conversions.


## How To Use This With Your Squarespace Site

Your current site is on Squarespace. You have two options:

### Option A: Link To It (Easiest)
Just add a link/button on your Squarespace site that points to:
`https://more-than-motion.vercel.app`

Use this for your ads - send ad traffic directly to this URL. Keep your main Squarespace site as-is for organic visitors.

### Option B: Replace Your "MTMI In Studio" Page
In Squarespace, you can redirect your /services-6-1 page to the Vercel landing page:
1. Go to Settings > Advanced > URL Mappings
2. Add: `/services-6-1 -> https://more-than-motion.vercel.app 301`

### Option C: Use a Custom Domain
If you want this page on something like `apply.morethanmotionintensive.com`:
1. In your domain registrar, add a CNAME record:
   - Name: `apply`
   - Value: `cname.vercel-dns.com`
2. In Vercel (vercel.com), go to the project settings > Domains > Add `apply.morethanmotionintensive.com`


## How To Edit The Page

The entire page is one file: **index.html**

### To edit text:
Open index.html in any text editor (even TextEdit on Mac works). Search for the text you want to change and update it.

Common things to edit:
- **Headline:** Search for "Earn $2,000+"
- **Subtext:** Search for "We bring elite faculty"
- **Faculty names:** Search for "Kaycee Rice", "Phil Wright", etc.
- **Testimonial:** Search for "Sarah Mitchell"
- **FAQ answers:** Search for "faq-a"
- **Banner text:** Search for "ONE STUDIO PER CITY"

### To add photos:
1. Put your image files in the same folder as index.html
2. In the code, find the gallery section (search for "gallery-grid")
3. Replace the image filenames with yours:
```html
<img src="your-photo-name.png" alt="description" loading="lazy">
```

### To deploy changes:
If you have Vercel CLI installed, run:
```
npx vercel --prod
```
Or drag-and-drop the folder to vercel.com/new


## Content From Your Current Site To Add

Your Squarespace site has great content that could strengthen this landing page. Consider adding:

- **2026 Tour dates** (Lincoln NE - Sold Out, Santa Cruz CA - Sold Out, Seattle WA - Open, Tucson AZ - Sold Out) - "Sold Out" dates are powerful social proof
- **Real photos** from your Squarespace gallery to replace placeholder images
- **Video content** if you have highlight reels or testimonial videos
- **More testimonials** from studio owners
- **Your mission statement** about serving "dancers around the world"
- **The journal session, on-camera video shoot, and Q&A** details are great differentiators


## File List

```
index.html          - The entire landing page (all code in one file)
group-energy.png    - Gallery photo placeholder
studio-dance.png    - Gallery photo placeholder
floor-move.png      - Gallery photo placeholder
hero-collage.png    - Gallery photo placeholder
strategy.md         - Growth playbook with ad scripts, follow-up sequences, etc.
```

## Questions?

Text Matt or email info@morethanmotionintensive.com
