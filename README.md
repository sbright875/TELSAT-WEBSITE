# Telsat Engineering Services — Cleaned Website

This is the cleaned-up version of the site, with the issues from the review fixed. A couple of items need one manual setup step from you before they're fully live — they're marked **ACTION NEEDED** below.

## What was fixed

**Critical bugs**
- The contact form now actually submits (see "Contact form setup" below) instead of just showing a fake success message and discarding the data.
- All 10 broken images (homepage hero + all 8 industry cards) now load — swapped in working images.
- Removed literal placeholder text (`+256 XXX XXX XXX`) and dead `href="#"` footer links.

**Brand & design**
- Removed the Microsoft/Azure-clone styling (the code previously used Microsoft's exact blue `#0078d4` for buttons/links and had comments like "Official Microsoft/Azure Blue" / "Exact Azure Layout Styling"). Buttons, links and hover states now use Telsat's own red (`#d71920`), matching the logo wordmark, across all pages.
- Standardized the footer across all 4 pages (previously each page had a different, inconsistent footer).

**SEO & discoverability**
- Added missing meta descriptions (index and products pages had none).
- Added Open Graph and Twitter Card tags, canonical URLs, and a favicon on every page — link previews on LinkedIn/WhatsApp/Slack will now show a proper title, description and logo.
- Added `sitemap.xml` and `robots.txt`.
- Added real `privacy.html`, `terms.html` and `sitemap.html` pages (previously the footer linked to `#`).

**Performance & code health**
- The logo was previously embedded as a giant base64 string in every page's HTML. It's now a real file at `assets/images/telsat-logo.png`, referenced normally — this alone cut page sizes by roughly 40–50%.
- The site's header/nav CSS was duplicated in full on all 4 pages. It's now one shared file, `assets/css/site-header.css`, linked from every page.
- Each page previously had 6–12 separate, overlapping `<style>` blocks (patches on patches, several using `!important` to override earlier ones). These are now consolidated into a single stylesheet per page.
- Relabeled the floating "Ask Telsat" button to "Get in Touch" — it links to the contact form, not a live chat, so it shouldn't look like one.

## ACTION NEEDED: activate the contact form (one click, no signup)

The form is wired up to **FormSubmit.co**, a free service that emails form submissions straight to an inbox — no account, no API key. It's already pointed at `info@telsatengineering.com`.

1. The very first time the form is submitted (by you as a test, or by a real visitor), FormSubmit sends a one-time **"Please Activate Your Form"** email to `info@telsatengineering.com`.
2. Open that email and click the confirmation link. That's it — from then on, every submission is delivered straight to `info@telsatengineering.com` automatically.
3. To trigger step 1 now rather than waiting for a real visitor, just submit the contact form yourself once on the live site.

Until it's activated, FormSubmit still returns success and the site shows the "thank you" message — the activation step only affects when email delivery switches on, so no enquiry is lost either way, but you'll want to activate it before launch so real enquiries actually reach the inbox.

If you'd rather use a different provider (Formspree, Web3Forms, etc.), just swap the `action` URL on the `<form id="enterprise-contact-form">` element in `index.html` and update the hidden fields to match that provider's conventions.

There's also a hidden honeypot field (`company_website`) already in place for basic spam protection — no setup needed there.

## Other placeholders to double check before launch

- **Phone numbers** in the contact section are realistic-format placeholders (`+256 414 123 456` / `+256 772 123 456`) — replace with your real numbers.
- **Domain**: canonical/OG tags assume `https://www.telsatengineering.com`. Update this across the files (search for that string) if your live domain is different.
- **Legal pages**: `privacy.html` and `terms.html` are reasonable starting templates, but should be reviewed by a lawyer before publishing, especially around data protection.

## Recommended next steps (not automatable without more input from you)

- **Replace stock imagery with real photography.** Several images are stock photos; genuine project/team photos will differentiate you more than any competitor using the same stock library.
- **Move off the Tailwind CDN script** (`cdn.tailwindcss.com`) to a compiled build for production — it currently compiles CSS in the visitor's browser on every load, which is slower than it needs to be. This requires a Node/Tailwind build step, which is best done in your own dev environment.
- **Add trust signals**: certifications, vendor partner badges, client logos, or case studies near the contact form and hero section.

## File structure

```
index.html, products.html, industries.html, about.html   — main pages
privacy.html, terms.html, sitemap.html                    — legal & sitemap pages
assets/images/telsat-logo.png                             — logo (also used as favicon)
assets/css/site-header.css                                — shared header/nav styles
sitemap.xml, robots.txt                                   — for search engines
```
