# Maintenance Guide — Editing Your Website

This guide explains how to update the everyday content on the Next Location website **without needing to be a developer**. Almost everything you'll want to change lives in one folder: **`src/data/`**.

### Before you start — two golden rules
1. **Keep the punctuation.** Each piece of text sits inside `"quotes"` and lines end with a `,` (comma). Change the words *between* the quotes, but leave the quotes and commas in place.
2. **Save, then check.** After editing, look at the site (`npm run dev` → <http://localhost:3000>). If a page breaks, you almost certainly removed a quote or comma — undo your last change and try again.

> Tip: edit in [VS Code](https://code.visualstudio.com/). It highlights matching quotes and warns you about mistakes before you even save.

---

## 1. Change the phone number, WhatsApp, or email

These come from your settings file, **not** from the code.

1. Open **`.env.local`** (if it doesn't exist, copy `.env.example` and rename the copy to `.env.local`).
2. Edit these lines:
   ```
   NEXT_PUBLIC_PHONE=+8801712345678
   NEXT_PUBLIC_WHATSAPP_NUMBER=+8801712345678
   NEXT_PUBLIC_EMAIL=info@nextlocation.com.bd
   ```
3. Save. Restart the preview (`Ctrl + C`, then `npm run dev`).
4. When deploying, also update these in **Vercel → Settings → Environment Variables**.

The phone, WhatsApp, and email automatically update everywhere on the site (header, footer, contact page, listing buttons).

---

## 2. Add, edit, or remove a property listing

**File:** `src/data/properties.ts`

Each property is a block that looks like this:

```ts
{
  id: "nl-1010",
  slug: "uttara-sector-7-family-apartment-for-sale",
  title: "Uttara Sector 7 Family Apartment",
  purpose: "sale",            // "sale" or "rent"
  category: "residential",    // "residential", "commercial", or "land"
  type: "Apartment",          // e.g. Apartment, Duplex, Office Space, Residential Plot
  status: "available",        // "available", "under-contract", "sold", "rented"
  price: 18500000,            // a plain number in Taka — NO commas, NO ৳ symbol
  isMonthly: false,           // true ONLY for rentals (price is then per month)
  area: "Uttara",             // neighbourhood
  city: "Dhaka",
  addressLine: "Sector 7",    // optional extra address detail
  areaSqft: 1650,             // size in square feet
  bedrooms: 3,                // leave out for land/offices if not relevant
  bathrooms: 3,
  parking: 1,
  description: "A bright, well-laid-out family apartment...",
  amenities: ["Lift", "Generator", "Parking", "Security"],
  images: ["/images/properties/property-placeholder.svg"],
  featured: true,             // true = also show on the homepage
  listedAt: "2026-06-10",     // date listed (YYYY-MM-DD)
},
```

**To add a property:** copy an entire existing block (from `{` to `},`), paste it just below, and change the values. **Give it a new, unique `id` and `slug`** (the slug becomes its web address, so use lowercase words separated by hyphens).

**To remove a property:** delete its whole block (from `{` through `},`).

**Prices:** type the number only. `18500000` shows on the site as **৳ 1,85,00,000** automatically.

---

## 3. Add or edit an area guide

**File:** `src/data/areas.ts`

Each area looks like this:

```ts
{
  slug: "uttara",
  name: "Uttara",
  city: "Dhaka",
  tagline: "A planned, family-friendly township in the north.",
  overview: "Uttara is a well-organised, self-contained township...",
  propertyTypes: ["Apartments", "Plots", "Retail"],
  lifestyle: "Wide roads, parks, schools, and shopping...",
  connectivity: "Served by the metro rail and close to the airport...",
  buyerProfile: "Families and investors seeking space and value...",
  investmentNotes: "Steady demand with metro-driven upside...",
  priceGuide: "৳ 80 Lakh – 3 Cr (apartments)",
  image: "/images/areas/area-placeholder.svg",
  featured: true,
},
```

Copy a block to add a new area; change the `slug` to something unique. Delete a block to remove an area.

---

## 4. Add or edit a blog / insights article

**File:** `src/data/blog.ts`

Articles are built from simple "blocks" so you never write raw HTML:

```ts
{
  slug: "buying-your-first-apartment-in-dhaka",
  title: "Buying Your First Apartment in Dhaka",
  excerpt: "A short one- or two-sentence summary shown in previews.",
  category: "Buying",
  author: "Next Location",
  date: "2026-06-12",            // YYYY-MM-DD
  cover: "/images/blog/blog-placeholder.svg",
  wordCount: 900,                // rough word count → sets the "X min read"
  featured: true,                // true = eligible for the homepage
  content: [
    { type: "paragraph", text: "Your opening paragraph goes here." },
    { type: "heading", text: "A section title" },
    { type: "paragraph", text: "More text under that heading." },
    { type: "list", items: ["First point", "Second point", "Third point"] },
    { type: "quote", text: "A highlighted pull-quote." },
  ],
},
```

The four block types you can use inside `content` are:
- `{ type: "paragraph", text: "..." }` — a normal paragraph
- `{ type: "heading", text: "..." }` — a section heading
- `{ type: "list", items: ["...", "..."] }` — a bulleted list
- `{ type: "quote", text: "..." }` — a highlighted quote

Copy a whole article block to add a new one (use a unique `slug`). Order doesn't matter — articles are sorted by date automatically.

---

## 5. Update leadership / team members

**File:** `src/data/team.ts`

```ts
{
  id: "partner-5",
  name: "Mr. Example Name",
  role: "Partner",
  bio: "A short professional summary.",
  image: "/images/team/team-placeholder.svg",
  initials: "EN",   // shown in the circle avatar
},
```

Change names, roles, and bios here. The `initials` appear in the circular avatar (use 2 letters).

---

## 6. Edit services, FAQs, values, or the process steps

- **Services** (the four pillars and their details): `src/data/services.ts`
- **Frequently asked questions:** `src/data/faq.ts`
- **Company info, vision, mission, core values, the 5-step process, statistics:** `src/data/site.ts`
- **Client testimonials:** `src/data/testimonials.ts`
- **Legal pages** (Privacy, Terms, Cookies, Disclaimer, Anti-Fraud): `src/data/legal.ts`
- **Footer links:** `src/data/footer.ts`
- **Header / navigation menu:** `src/data/navigation.ts`

Each follows the same copy-a-block pattern. Edit the text inside the quotes.

---

## 7. Replace placeholder images with real photos

The site ships with tasteful placeholder graphics so it looks finished right away. To use real images:

1. Put your image files in the matching folder inside **`public/images/`**:
   - Property photos → `public/images/properties/`
   - Area photos → `public/images/areas/`
   - Team photos → `public/images/team/`
   - Article covers → `public/images/blog/`
   - The big homepage banner → `public/images/hero/`
2. In the relevant data file, change the image path to your new file. For example, if you added `gulshan-apartment.jpg` to `public/images/properties/`, set:
   ```ts
   images: ["/images/properties/gulshan-apartment.jpg"],
   ```
   (Always start the path with `/images/...` — leave out the word `public`.)

**Recommended sizes:** property/area/article images look best around **1200 × 800 pixels**; the homepage banner around **1600 × 1200**. JPG or PNG both work. Keep files reasonably small (under ~500 KB) so pages load fast.

You can list **multiple images** for a property — they appear as a gallery:
```ts
images: [
  "/images/properties/gulshan-apartment-1.jpg",
  "/images/properties/gulshan-apartment-2.jpg",
],
```

### Replacing the logo
The logo is `public/logo-placeholder.svg`. Replace that file with your own (keep the same filename), or add a new file and update the reference in `src/components/common/logo.tsx`.

---

## 8. Add or improve Bengali translations

**File:** `src/locales/bn.ts`

This file only needs the phrases you want translated — anything left out automatically shows in English. To translate something, find its English key in `src/locales/en.ts`, then add the Bengali version in `bn.ts` under the same structure. For example, to translate the "Contact" menu item:

```ts
nav: {
  contact: "যোগাযোগ",
},
```

You can expand the Bengali coverage over time, one phrase at a time, without touching any code.

---

## 9. Connecting the forms to your inbox

Out of the box, the contact / valuation / inquiry / buying-agent forms **validate** input and **record submissions in the server log**, returning a friendly success message. To actually receive submissions by email or in a CRM, a developer can add a few lines to these files:

- `src/app/api/contact/route.ts`
- `src/app/api/inquiry/route.ts`
- `src/app/api/valuation/route.ts`

Each already has a clearly marked spot (a `TODO (maintainer)` comment) showing exactly where to plug in an email service (such as Resend or SendGrid), a database, or a Slack/webhook notification. The validated form data is right there, ready to send.

---

## 10. Publishing your changes

- **Previewing locally:** save your files; the browser at <http://localhost:3000> refreshes automatically.
- **Going live:** upload your changed files to GitHub. Vercel rebuilds and republishes the site within a couple of minutes — no other steps needed.
- **Sanity check before publishing (optional):** run `npm run build`. If it ends without red errors, your changes are safe to publish.

---

## Troubleshooting

| Problem | Most likely fix |
| --- | --- |
| A page shows an error after I edited content | You removed a `"` quote or `,` comma. Undo your last edit. |
| My new property/area/article doesn't appear | Check it has a **unique** `slug`, and that the block ends with `},`. |
| The phone/email didn't update | Edit `.env.local` (not the code), then restart `npm run dev`. On the live site, update the variables in Vercel too. |
| My image isn't showing | Confirm the file is in `public/images/...` and the path in the data file starts with `/images/` (no `public`). |
| `npm run dev` won't start | Run `npm install` again, then retry. Make sure Node.js is installed (`node -v`). |

---

Questions about anything beyond content edits (new page types, payment integration, the future property platform) are developer tasks — but the content above is fully yours to manage. *Be with us, we will care for you.*
