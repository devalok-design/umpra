# Umpra — Coming Soon

Umpra is a premium wellness brand. This is the pre-launch "Coming Soon" landing page.

**Live site:** [https://umpra.com](https://umpra.com)

---

## Google Sheets Waitlist Setup

The waitlist form collects email addresses and sends them to a Google Sheet. Here's how to set it up:

1. Go to [Google Sheets](https://sheets.google.com) and create a new spreadsheet. Name it something like "Umpra Waitlist".

2. In the menu bar, click **Extensions > Apps Script**.

3. Delete any code already in the editor and paste this:

   ```javascript
   function doPost(e) {
     var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
     var data = JSON.parse(e.postData.contents);
     sheet.appendRow([new Date(), data.email]);
     return ContentService
       .createTextOutput(JSON.stringify({ result: "success" }))
       .setMimeType(ContentService.MimeType.JSON);
   }
   ```

4. Click **Deploy > New Deployment** (top right).

5. Next to "Select type", click the gear icon and choose **Web app**.

6. Set **Execute as** to **Me**.

7. Set **Who has access** to **Anyone**.

8. Click **Deploy**.

9. Google will ask you to authorize. Click through the prompts — if you see a warning screen, click **Advanced** then **Go to [your project name]** to continue.

10. After deploying, you'll see a **Web App URL**. Copy it.

11. Open `index.html` in a text editor. Near the top of the `<script>` block (around line 710), find this line:

    ```javascript
    const WAITLIST_ENDPOINT = "YOUR_GOOGLE_SCRIPT_URL";
    ```

12. Replace `YOUR_GOOGLE_SCRIPT_URL` with the URL you copied. Keep the quotes. It should look something like:

    ```javascript
    const WAITLIST_ENDPOINT = "https://script.google.com/macros/s/ABC123.../exec";
    ```

13. Save the file. The waitlist form will now send submissions to your Google Sheet.

---

## Deploying to GitHub Pages

1. Go to your repository on GitHub.
2. Click **Settings** (top menu) > **Pages** (left sidebar).
3. Under **Source**, select **Deploy from a branch**.
4. Set **Branch** to `main` and folder to `/ (root)`.
5. Click **Save**.
6. Your site will be live at `https://devalok-design.github.io/umpra/` within a few minutes.

---

## Custom Domain (umpra.com)

### In GitHub

1. In the same **Settings > Pages** section, enter `umpra.com` under **Custom domain** and click **Save**.

### In GoDaddy DNS Settings

Add these DNS records:

**A records** (for the apex domain `umpra.com` — all four are required):

| Type | Name | Value |
|------|------|-------|
| A    | @    | `185.199.108.153` |
| A    | @    | `185.199.109.153` |
| A    | @    | `185.199.110.153` |
| A    | @    | `185.199.111.153` |

**CNAME record** (for `www`):

| Type  | Name | Value |
|-------|------|-------|
| CNAME | www  | `devalok-design.github.io` |

### After DNS is set

- The `CNAME` file in this repo tells GitHub Pages which custom domain to use — it's already set up, don't delete it.
- DNS changes can take up to 24 hours to take effect.
- Once the domain resolves, go back to **Settings > Pages** and check **Enforce HTTPS**.

---

## Customization

- **Brand colors:** Edit the CSS custom properties in the `:root` block at the top of `index.html` (around line 65). The main ones are `--color-primary`, `--color-secondary`, and `--color-surface`.

- **Copy/text:** All the text content is in the HTML sections of `index.html` — the hero tagline, teaser lines, waitlist card heading, and footer.

- **Logo:** The logo is an inline SVG inside the `.hero-logo` div in the hero section. Replace the `<svg>` element with your own, or swap in an `<img>` tag pointing to a logo file.
