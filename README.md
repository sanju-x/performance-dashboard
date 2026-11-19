# AM Motors — Stock & Trend Analysis dashboard

A single-page dashboard (`index.html`) with seven pages: Forecast & Insights, Model · Variant · Colour, Stock, IBND, WS & Retail Target, Pending Bookings, Data. All data as of 13 Nov 2026 is built into `index.html`; nothing needs a server or build step.

## Files

| File | What it does |
|---|---|
| `index.html` | The whole dashboard: page, styles, code and data |
| `_headers` | Cloudflare Pages headers: no search indexing, no caching of the data page |
| `robots.txt` | Tells search engines not to crawl the site |
| `README.md` | This file |

## ⚠️ Before you publish: keep it private

The dashboard contains business data: VINs, chassis numbers, booking numbers, DSE / BSH names, stock and sales figures. A Cloudflare Pages site is **public to anyone with the link** unless you lock it. Do both:

1. Make the GitHub repository **Private**.
2. Turn on **Cloudflare Access** for the site (step 4 below) so only your team's email addresses can open it.

## 1. Put the files on GitHub

1. Sign in at github.com → **New repository**.
2. Name: `am-motors-dashboard` · Visibility: **Private** · Create.
3. On the new repo page click **uploading an existing file**.
4. Unzip this folder and drag in **all four files** (`index.html`, `_headers`, `robots.txt`, `README.md`) — the files themselves, not the folder.
5. Click **Commit changes**.

## 2. Create the Cloudflare Pages site

1. Sign in at dash.cloudflare.com → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**.
2. Authorise GitHub and pick the `am-motors-dashboard` repository.
3. Build settings:
   - Framework preset: **None**
   - Build command: *(leave empty)*
   - Build output directory: `/`
4. **Save and Deploy**. After about a minute you get a link like `https://am-motors-dashboard.pages.dev`.

*No GitHub?* In step 1 choose **Upload assets** instead of Connect to Git and drop in the unzipped folder.

## 3. (Optional) Your own address

Pages project → **Custom domains** → **Set up a custom domain** → e.g. `stock.ammotors.in`, then follow the DNS prompt.

## 4. Lock it with Cloudflare Access (recommended)

1. Pages project → **Settings** → **Access policy** → **Enable** (or Zero Trust → Access → Applications → Add → Self-hosted, with your pages.dev and custom domain).
2. Policy: **Allow** → **Emails** → add your team's email addresses (or **Emails ending in** `@yourcompany.com`).
3. Login method: **One-time PIN** (people get a code by email). Save.

Now only the listed people can open the dashboard; everyone else sees a Cloudflare login page.

## 5. Updating the data later

- **Stock and IBND:** open the Stock or IBND page and use **Load reports** (or drag `stock_report.xlsx` / `ibnd_report.xlsx` onto the page). The data is kept in that browser only.
- **Everything else** (sales, bookings, plan, indent, dispatch, targets, incentive, TVP): ask Claude to rebuild the dashboard from the new reports, then on GitHub open `index.html` → ✏️ **Edit** → replace it (or **Add file → Upload files** with the new `index.html`) → **Commit**. Cloudflare redeploys automatically within a minute.

## Notes

- Excel export buttons download `.xlsx` files directly on your own site.
- Excel export and "Load reports" load the SheetJS library from cdnjs.cloudflare.com, so the browser needs internet access.
- Keyboard shortcuts: keys 1–7 switch pages.
