# Organic Rays — static website

Premium, responsive, B2B-first Indian coffee website. Built with plain HTML, CSS and JavaScript; no build step or paid theme required.

## Project contents

- `index.html` — Home
- `coffee.html` — Coffee categories
- `origins.html` — Indian coffee-growing regions
- `quality.html` — Sourcing and quality approach
- `about.html` — Brand story
- `partnerships.html` — B2B export partnerships
- `contact.html` — Google Forms enquiry page
- `404.html`, `robots.txt`, `sitemap.xml`, `_headers`
- `assets/` — shared stylesheet, navigation script, site configuration and a simple brand mark

## Before publishing — 15-minute checklist

1. **Confirm your brand assets.** The site currently uses a typographic Organic Rays mark, not your original uploaded logo. Replace the `O` circle in the header with your approved logo if desired.
2. **Connect Google Forms.**
   - Create a Google Form and publish it so anyone you intend to receive enquiries from can respond.
   - Suggested fields: Full name; Company; Business email; Country; WhatsApp (optional); Buyer type; Product interest (green Arabica / green Robusta / roasted coffee / other); estimated quantity and unit; packaging; destination port; target timeline; specification/document upload link (optional); message.
   - Avoid requiring respondents to sign in unless that is intentional.
   - In Google Forms choose More (⋮) → Embed HTML. Copy the URL inside the iframe `src` attribute.
   - Copy the responder URL from the published form.
   - Paste both into `assets/site-config.js`:
     ```js
     window.ORGANIC_RAYS_CONFIG = {
       googleFormEmbedUrl: "https://docs.google.com/forms/d/e/YOUR_FORM_ID/viewform?embedded=true",
       googleFormResponderUrl: "https://docs.google.com/forms/d/e/YOUR_FORM_ID/viewform"
     };
     ```
   - Save, commit and push. Google Forms collects responses in your Google account; configure response notifications in Forms.
3. **Verify the mailbox.** The site uses `hello@organicrays.com`. Confirm that this address exists and can receive mail before launch.
4. **Verify all commercial claims.** Do not add origin availability, stock, certifications, grades, capacity, export history, lead times, MOQ or private-label capability until documented and confirmed.
5. **Replace the coffee photos if desired.** Current hero/section photography loads from Unsplash over HTTPS. For best brand control, use licensed original photography and update the CSS image URLs.
6. **Test all pages on mobile and desktop**, plus the quote form and email link.

## Local preview

Open `index.html` in a browser. For a local server, from this folder run:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000`.

## Deploy to Cloudflare Pages using GitHub

1. Create a GitHub repository, for example `organic-rays-website`.
2. Upload the contents of this folder to the repository root (so `index.html` is at the root).
3. In Cloudflare Dashboard, open **Workers & Pages → Create application → Pages → Connect to Git**.
4. Select the GitHub repository and configure:
   - Production branch: `main`
   - Framework preset: `None`
   - Build command: `exit 0`
   - Build output directory: `/` (repository root; if the UI requires a relative folder, use `.`)
5. Deploy. Cloudflare will provide a `*.pages.dev` preview URL. Test it before adding the production domain.
6. In the Pages project open **Custom domains → Set up a domain** and add `www.organicrays.com`. Add `organicrays.com` as well if you want the apex domain to work.

## Connect your GoDaddy domain safely

Recommended full DNS setup for both apex and www:

1. Add `organicrays.com` as a site/zone in Cloudflare and let Cloudflare scan existing DNS records.
2. **Before changing nameservers, compare DNS records.** Preserve all existing email records, especially MX, SPF, DKIM and DMARC TXT records. Also preserve any verification records used by your email provider.
3. In Cloudflare, confirm the email records are present and correct. Do not proxy mail records; mail-related DNS records should be DNS-only.
4. Cloudflare will give you two authoritative nameservers. In GoDaddy, open the domain's DNS/nameserver settings and replace the current nameservers with the exact two Cloudflare nameservers shown in your Cloudflare account.
5. Wait for nameserver activation. Domain registration stays at GoDaddy; this changes DNS hosting only.
6. In Cloudflare Pages → your project → Custom domains, add `organicrays.com` and `www.organicrays.com`. Follow the dashboard's prompts. Choose one canonical host (recommended `www`) and configure a redirect from the other host if desired.
7. Test `https://www.organicrays.com`, `https://organicrays.com`, email sending/receiving, and the Google Form.

**Important:** Do not change nameservers until you have copied and checked all existing DNS records. A missing MX/TXT record can interrupt your existing business email. Cloudflare Pages custom apex domains require the domain to be on Cloudflare DNS; the Pages dashboard will guide the domain setup.

## SEO launch checklist

- Verify the canonical host (www or apex) and ensure the other redirects to it.
- Add the domain property in Google Search Console and verify ownership.
- Submit `https://www.organicrays.com/sitemap.xml`.
- Check page titles/descriptions, spelling, contact email and internal links.
- Add real, descriptive image alt text if you replace the decorative backgrounds with `<img>` elements.
- Add Google Analytics only if you want analytics and have configured an appropriate privacy notice/consent approach for your target markets.

## Notes

- This is a static lead-generation site, not an ecommerce store or order-management system.
- The Google Form is not pre-connected because the form ID must come from your own Google account.
- The website does not claim Organic Rays is certified organic or holds any export certifications.
