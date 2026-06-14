# Next Location — Website

A production-ready website for **Next Location**, a Bangladesh-based real estate, property management, and consultancy firm. Built with Next.js 15, TypeScript, and Tailwind CSS. Bilingual (English / বাংলা), dark-mode ready, fully responsive, and search-engine optimised.

This README is written so that **someone with no coding experience** can get the site running and deployed. Follow it top to bottom.

---

## What you need (one-time setup)

1. **A computer** (Windows, Mac, or Linux).
2. **Node.js** — the engine that runs the site. Download the **LTS** version from <https://nodejs.org> and install it (click through the installer with default options).
   - To confirm it worked: open a terminal (Command Prompt on Windows, Terminal on Mac) and type `node -v`. You should see a version number like `v20.x` or `v22.x`.
3. **A code editor** (optional but recommended): [Visual Studio Code](https://code.visualstudio.com/) is free and friendly.

---

## Running the site on your computer

1. **Open a terminal** inside this project folder.
   - Easiest way: open the folder in VS Code, then choose **Terminal → New Terminal** from the menu.
2. **Install the building blocks** (only needed the first time, or after updates):
   ```bash
   npm install
   ```
   This downloads everything the site needs. It can take a minute or two.
3. **Start the site in preview mode:**
   ```bash
   npm run dev
   ```
4. Open your web browser and go to **<http://localhost:3000>**. You'll see the site. It will redirect to `http://localhost:3000/en` (the English version). The Bengali version is at `http://localhost:3000/bn`.
5. Leave the terminal running while you browse. To stop, click the terminal and press **Ctrl + C**.

Any change you save to the project will refresh the browser automatically.

---

## Settings you should fill in (important)

The site reads its phone number, email, WhatsApp number, and more from a settings file. A template is provided as **`.env.example`**.

1. Make a copy of `.env.example` and name the copy **`.env.local`**.
2. Open `.env.local` in your editor and fill in the real values. The most important ones:

   | Setting | What it is | Example |
   | --- | --- | --- |
   | `NEXT_PUBLIC_SITE_URL` | Your live website address | `https://nextlocation.com.bd` |
   | `NEXT_PUBLIC_PHONE` | Phone number (with country code) | `+8801712345678` |
   | `NEXT_PUBLIC_WHATSAPP_NUMBER` | WhatsApp number (with country code) | `+8801712345678` |
   | `NEXT_PUBLIC_EMAIL` | Contact email | `info@nextlocation.com.bd` |
   | `NEXT_PUBLIC_FACEBOOK_URL` | Facebook page link (optional) | `https://facebook.com/...` |
   | `NEXT_PUBLIC_INSTAGRAM_URL` | Instagram link (optional) | `https://instagram.com/...` |
   | `NEXT_PUBLIC_LINKEDIN_URL` | LinkedIn link (optional) | `https://linkedin.com/...` |
   | `CONTACT_FORM_TARGET_EMAIL` | Where form submissions should be sent | `info@nextlocation.com.bd` |

   > The site **will still run** even if you leave these blank — it uses safe placeholders — but real visitors should see real details, so fill them in before going live.

3. Save the file. If the preview (`npm run dev`) is running, stop it (Ctrl + C) and start it again so the new settings load.

You never have to touch `process.env` or any code — everything is read through one tidy settings layer.

---

## Putting the site on the internet (deploying to Vercel)

The site is designed for **Vercel**, which is free to start and made by the same team as Next.js.

### Step 1 — Put the code on GitHub
1. Create a free account at <https://github.com>.
2. Create a new, empty repository (call it `next-location`).
3. Upload this project to it. (GitHub's website has an "upload files" option, or use GitHub Desktop for a click-based experience.)

### Step 2 — Connect Vercel
1. Create a free account at <https://vercel.com> and choose **"Continue with GitHub."**
2. Click **"Add New… → Project,"** then pick your `next-location` repository.
3. Vercel automatically detects Next.js. You don't need to change the build settings.
4. Under **Environment Variables**, add the same values you put in `.env.local` (copy each name and value). At minimum add `NEXT_PUBLIC_SITE_URL`, `NEXT_PUBLIC_PHONE`, `NEXT_PUBLIC_WHATSAPP_NUMBER`, and `NEXT_PUBLIC_EMAIL`.
5. Click **Deploy**. After a minute or two, your site is live on a `*.vercel.app` address.

### Step 3 — Use your own domain (e.g. nextlocation.com.bd)
1. In your Vercel project, go to **Settings → Domains**.
2. Type your domain and follow the on-screen instructions (it tells you exactly what to change at your domain registrar).
3. Once it verifies, your site is live on your real address with HTTPS handled automatically.

### Updating the live site later
Every time you upload a change to GitHub, Vercel rebuilds and republishes automatically. No extra steps.

---

## Checking everything builds (optional)

Before deploying, you can confirm the site compiles cleanly:

```bash
npm run build
```

If it finishes without red errors, you're good. To preview the finished build locally:

```bash
npm run start
```

---

## Where things live (quick map)

```
src/
├─ app/                 The pages (home, about, services, listings, etc.)
├─ components/          Reusable building blocks (buttons, cards, forms, sections)
├─ data/                ★ YOUR CONTENT lives here — properties, areas, team, blog, FAQs
├─ lib/                 Behind-the-scenes helpers (formatting, SEO, validation)
├─ locales/             English + Bengali wording
└─ types/               Technical definitions (rarely touched)
public/                 Images, logo, icons
.env.example            Template for your settings
MAINTENANCE.md          ★ How to edit content day-to-day (read this!)
```

**To change wording, prices, listings, team members, or articles, you'll almost always be editing files in `src/data/`.** See **MAINTENANCE.md** for step-by-step instructions written for non-developers.

---

## Good to know

- **Bilingual:** English (`/en`) and Bengali (`/bn`). A language switcher sits in the header.
- **Dark mode:** visitors can switch themes; their choice is remembered.
- **Forms:** the contact, valuation, property-inquiry, and buying-agent forms validate input and show success/error messages. By default they log submissions on the server — see MAINTENANCE.md to connect them to your email or a CRM.
- **Images:** the site ships with on-brand placeholder graphics so it looks complete immediately. Replace them with real photos any time (instructions in MAINTENANCE.md).
- **Self-hosted fonts:** fonts are bundled with the site (no Google Fonts request), which is faster and privacy-friendly.
- **SEO:** every page has proper titles, descriptions, social-share cards, structured data, a sitemap, and a robots file — all generated automatically.

---

## Need a hand?

If something doesn't work:
1. Make sure Node.js is installed (`node -v` shows a version).
2. Re-run `npm install`.
3. Stop and restart `npm run dev`.
4. If a page shows an error after editing content, check that file in `src/data/` for a missing comma or quote — that's the most common cause.

Built with care for Next Location — *Dhaka, Bangladesh.*
