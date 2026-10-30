# Saffron & Clay — Sri Lankan Restaurant Website

A multi-page restaurant website for **Saffron & Clay**, a fictional Sri Lankan kitchen in Colombo.
Built with **HTML, CSS and vanilla JavaScript** from the approved Figma UI design (v1.0, 27 Oct 2026).
Accounts, cart, orders and contact messages are stored in the browser with **localStorage**.

> **Demo project.** All names, prices, people and figures are fictional. localStorage is not secure
> authentication and no real payments or messages are sent.

**Live site (GitHub Pages):** `https://<your-username>.github.io/saffron-clay-restaurant/` *(after you enable Pages — see below)*

---

## Pages

| Page | File | What it does |
|---|---|---|
| Home | `index.html` | Hero, category shortcuts, popular dishes, weekday-offer countdown, story, animated counters, testimonials carousel, live opening status, map, footer |
| Login | `login.html` | Email + password, show/hide password, remember me, error/success messages, continue as guest, redirect to Home |
| Sign Up | `signup.html` | Full name, email, optional phone, password + confirm, strength meter, terms checkbox, duplicate-account check |
| About | `about.html` | Introduction, mission / vision, interactive history timeline, executive chef profile, kitchen team |
| Contact | `contact.html` | Contact details, opening hours, message form with validation and character counter, map, social links, FAQ accordion |
| Menu | `menu.html` | 42 dishes rendered from a JS array · search · category · price range · dietary · spice level · availability · sorting · pagination · "No products found" |
| Food details | `food-details.html?id=1` | One reusable page for every dish: gallery, price, ingredients, portion, spice, dietary info, availability, quantity selector, add to cart, tabs, related dishes, invalid-ID handling |
| Services | `services.html` | Services (online ordering, delivery, takeaway, dine-in, catering), delivery conditions, editable cart, totals, promo code, delivery/pickup checkout form, order confirmation |
| Cart *(extra)* | `cart.html` | Cart table, quantity changes, remove, clear, totals, promo code, dessert suggestions, empty state |
| Order confirmation *(extra)* | `order-confirmation.html?ref=…` | Order reference, simulated status tracker, items, delivery details and totals |
| My account *(extra)* | `account.html` | Profile, order history, favourites, saved messages, logout (login required) |

The checkout form lives on the **Services** page (as in the approved design), at `services.html#checkout`.

## localStorage keys

| Key | Contents | Written by |
|---|---|---|
| `restaurantUsers` | Demo accounts `{ name, email, phone, salt, passwordHash }` — the password itself is never stored | Sign Up |
| `currentUser` | Signed-in session (in `localStorage` with *Remember me*, otherwise `sessionStorage`) | Login / Logout |
| `restaurantCart` | `[{ id, name, quantity }]` — prices are always read from the product data | Menu, Details, Cart, Services |
| `restaurantOrders` | Demo order records | Checkout → Confirmation |
| `contactMessages` | Submitted contact messages | Contact |
| `restaurantFavourites` | Favourite dish IDs | ♡ buttons |
| `restaurantPromo` | Applied promo code | Cart / Services |

Invalid or corrupted stored data is ignored safely (see `js/storage.js`), so the site never crashes on bad data.

**Demo promo codes:** `SAFFRON10` (10% off) · `WELCOME500` (LKR 500 off orders over LKR 3,000).
**Delivery:** LKR 350, free over LKR 5,000. Pickup is free.

## Run it in VS Code

1. Open the `Restaurant_Website` folder in VS Code (**File → Open Folder…**).
2. Install the recommended **Live Server** extension when VS Code asks (or search *Live Server* by Ritwick Dey).
3. Right-click `index.html` → **Open with Live Server**. The site opens at `http://127.0.0.1:5500/index.html`.

No build step and no internet connection are needed — fonts and images are bundled.
You can also simply double-click `index.html` to open it in a browser.

Optional: with Node.js installed, `npm start` serves the folder at `http://localhost:5500`.

## Project structure

```
Restaurant_Website/
├── index.html  login.html  signup.html  about.html  contact.html
├── menu.html  food-details.html  services.html  cart.html
├── order-confirmation.html  account.html
├── css/
│   ├── fonts.css          # @font-face for the bundled fonts
│   └── style.css          # design tokens + all components + responsive rules
├── js/
│   ├── data.js            # products (42), categories, chefs, testimonials, hours
│   ├── storage.js         # safe localStorage helpers: Auth, Cart, Orders, Messages…
│   ├── common.js          # header, footer, icons, toasts, product card, search
│   ├── cart-ui.js         # shared cart list + order summary
│   └── home.js  auth.js  about.js  contact.js  menu.js
│       food-details.js  services.js  cart.js  confirmation.js  account.js
├── images/                # SVG illustrations (dishes, chefs, map, logo)
├── fonts/                 # Playfair Display + DM Sans (SIL Open Font License)
├── tools/make_art.py      # script that generated the SVG dish illustrations
├── tests/e2e-test.js      # automated browser test of the main flows
├── .vscode/               # Live Server settings + Chrome launch configs
└── .github/workflows/pages.yml   # auto-deploy to GitHub Pages
```

## Put it on GitHub

```bash
cd Restaurant_Website
# the folder is already a Git repository with commit history
git remote add origin https://github.com/<your-username>/saffron-clay-restaurant.git
git branch -M main
git push -u origin main
```

Then on GitHub: **Settings → Pages → Build and deployment → Source: GitHub Actions**.
Every push to `main` publishes the site automatically (see the **Actions** tab).
Copy the repository link into `GitHub_Link.txt` in the submission folder.

## Testing

Manual checks performed:

- Sign up validation (required fields, email format, password match, duplicate email) and login / logout
- Every menu filter on its own and combined, sorting, pagination, URL keeps the filters on refresh
- Add to cart from Menu, Details and Cart suggestions; badge updates on every page
- Cart survives a page refresh; quantity changes update totals; delivery fee and promo codes
- Checkout validation, delivery vs pickup, order saved, cart cleared, confirmation page
- Invalid product IDs / order references show a friendly message
- Corrupted localStorage values do not break any page
- Layout at 1440 px, 1024 px, 768 px and 390 px — no horizontal scrolling

Automated test (optional, needs Node.js):

```bash
npm install
npx playwright install chromium
npm test        # 55 checks
```

## Technologies

HTML5 · CSS3 (custom properties, grid, flexbox, media queries) · JavaScript (ES6, no frameworks) ·
localStorage / sessionStorage · Git & GitHub · GitHub Actions (Pages) · Figma (UI design)

## Credits

- Fonts: [Playfair Display](https://fonts.google.com/specimen/Playfair+Display) and [DM Sans](https://fonts.google.com/specimen/DM+Sans), SIL Open Font License.
- Icons: hand-drawn SVG paths in a Lucide-style 24 px grid (from the project style guide).
- Illustrations: generated SVG artwork (`tools/make_art.py`) matching the UI design.
