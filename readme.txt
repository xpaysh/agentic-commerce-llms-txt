=== LLMs.txt for WooCommerce ===
Contributors: xpay
Tags: llms.txt, woocommerce, chatgpt, ai search, generative engine optimization
Requires at least: 6.0
Tested up to: 7.0
Requires PHP: 7.4
Stable tag: 1.0.0
License: GPLv2 or later
License URI: https://www.gnu.org/licenses/gpl-2.0.html

Get recommended by ChatGPT, Claude and Perplexity. Commerce-aware /llms.txt for your WooCommerce store — auto-refreshed, free forever.

== Description ==

**A shopper asks ChatGPT: *"Where can I buy a waterproof bike light under $50?"***

If your store sells one, you want to be the answer. To stand a chance, ChatGPT, Claude, Perplexity and Google's AI Mode need a file called `/llms.txt` at your domain root — a clean, machine-readable summary of what you sell. Most WooCommerce stores don't have one yet, and the generic plugins that do are built around blog posts and pages. They have no idea what a product, a price, or a variation is.

This plugin fixes that. In 30 seconds.

**35 plugins on WordPress.org generate `/llms.txt`. One reads your catalog.**

= What you get =

* **A `/llms.txt` file** built from your live WooCommerce catalog — top-selling products, real prices, real images, real links. The format AI shopping agents are converging on.
* **A `/llms-full.txt` file** with your full catalog, one section per product, for AI agents that want everything in one fetch.
* **Daily auto-refresh.** When you add products, change prices, or update stock, your files update themselves. No schedules to wire up. No buttons to press.
* **Version history with one-click rollback.** Every refresh is kept so you can compare and restore. Pin a version when you've got it just right.
* **Free forever.** No tier-gates. No upsells. No nags.

= Why this is built for WooCommerce, not WordPress =

Generic llms.txt plugins summarise your blog posts and pages. AI shopping agents need **products** — with a price and an image per item — to actually recommend you. Without that, your store turns into prose, and the agent recommends a competitor whose data is cleaner.

This plugin reads your live WooCommerce catalog and emits exactly what AI shoppers expect:

* **Real prices**, including "from" prices for variable products (no $0 placeholders that drop you out of carousels)
* **Real images**, including products with size/colour variations
* **WooCommerce visibility honoured** — hidden, shop-only and search-only products stay out by default
* **A per-product *Exclude from llms.txt* checkbox** on every product edit screen, in case you want to keep a specific item private
* **Smart description fallback** — pulls from Yoast SEO, Rank Math, AIOSEO, SEOPress or Slim SEO if you've already written one; falls back to your WooCommerce short description otherwise
* **Safe take-over of an existing `/llms.txt`** — if you already have one (from another plugin or hand-rolled), we back it up to `wp-content/uploads/lltxt-backups/` first, then take over. Restore your version any time from the Files tab — the backup is always preserved

= Built by the team behind Agentic Commerce for WooCommerce =

We build AI-shopping infrastructure for WooCommerce stores. We see, every day, which catalogs AI shoppers pick up and which they skip. We built this so any WooCommerce store — yours included — gets the same treatment for free.

**You can't win the race if you don't show up.**

== External services ==

This plugin keeps a version history of your `/llms.txt` and `/llms-full.txt` at xpay.sh so you can compare versions and roll back to any prior one with a single click. This is **on by default** and disclosed in a dismissible admin notice on activation. Turn it off any time in **Settings → LLMs.txt → Privacy**.

**Service:** xpay.sh LLMs.txt version-history API
**Base URL:** `https://llmstxt-api.xpay.sh` (filterable via the `lltxt_backend_base_url` filter or option)
**Privacy policy:** https://xpay.sh/privacy
**Terms of service:** https://xpay.sh/terms

**What's sent, when, and why:**

* `POST /v1/llms-txt/snapshot` — After every refresh (daily auto + on-demand). Sends the rendered `/llms.txt` and `/llms-full.txt` bodies (the same bodies served publicly from your domain), plus your site slug, WordPress/WooCommerce/plugin version strings, and a sha256 of a random local key as `X-Xpay-Api-Key`. Keeps the version history.
* `GET /v1/llms-txt/versions` and `GET /v1/llms-txt/version/{id}` — When you open the Version Control tab. Lists or fetches prior versions.
* `POST /v1/llms-txt/recommend` — When you click *Get recommendation*. Returns a merged best-version body.
* `POST /v1/llms-txt/pin` — When you pin or unpin a version.
* `DELETE /v1/llms-txt/merchant` — When you click *Delete my data*, or on plugin uninstall (if sync was on).

**What is NOT sent:** no order data, no customer data, no admin email, no analytics, no raw API key. The file bodies sent to us are the same bodies you serve publicly at `yourstore.com/llms.txt`.

== Installation ==

1. Install from **Plugins → Add New** in your WordPress admin, or upload the ZIP at **Plugins → Add New → Upload Plugin**.
2. Activate.
3. Visit `https://yourstore.com/llms.txt` — your products are live.

That's it. Settings live at **Settings → LLMs.txt** if you want to tune which products are featured.

== Frequently Asked Questions ==

= Will this actually get my products into ChatGPT? =

`/llms.txt` is the file AI shopping agents look for when they want to recommend products. Without one, you're invisible to them. With one — and especially a commerce-aware one — you join the answer set. The rest is up to your product quality, your prices and the AI's match logic, but at least you're in the running. You can't win the race if you don't show up.

= I already have a /llms.txt — what happens to it? =

Your file is preserved. On activation we save your original to a timestamped backup inside your WordPress uploads folder, then take over `/llms.txt` so your products are immediately AI-ready. **Restore your original any time** with one click from the Files tab → *Restore my version*. The backup is never deleted, even on plugin uninstall — your file is yours.

= Does it slow my store down? =

No. Files are generated by a background job (daily, or whenever you click Regenerate), stored as plain static files in your webroot, and served by your web server — not by WordPress on every request. Storefront speed is untouched.

= Does it work with WP Engine / Flywheel / hardened hosts? =

Yes. The plugin tries multiple write strategies so it works on WP Engine, Flywheel, WP VIP and most managed hosts where direct file access is restricted. If a file can't be written, you'll see the error and a fix in the Diagnostics tab.

= Does it work with my SEO plugin? =

Yes. The plugin reads your existing product meta descriptions from Yoast SEO, Rank Math, AIOSEO, SEOPress or Slim SEO — whichever you have. Nothing in your SEO plugin's setup needs to change.

= I want to keep one specific product out of /llms.txt. How? =

Edit the product. In the right-hand sidebar there's an *LLMs.txt for AI Shoppers* box with an *Exclude this product* checkbox. Tick it, save, done. The next refresh will drop it.

= How is this different from other llms.txt plugins? =

Every other llms.txt plugin on the wp.org repository walks your **blog posts and pages**. This one walks your **WooCommerce catalog** — products, prices, stock, images, variations. AI shopping agents need product data to recommend products. That's the whole point.

= Is it really free forever? =

Yes. No paid tier, no premium upsell, no "pro version" lurking in the admin. The version-history sync to xpay.sh is also free. You can turn it off in **Settings → LLMs.txt → Privacy** if you'd rather not use it.

== Screenshots ==

1. Your live `/llms.txt` — a card-ready product summary AI shoppers can read at a glance.
2. The Files tab — preview each file and regenerate on demand.
3. Version Control — every prior version, one-click restore and pin.
4. The per-product *Exclude from llms.txt* checkbox on every product edit screen.
5. Privacy tab — version-history sync toggle and delete-my-data button.

== Changelog ==

= 1.0.0 =
* Commerce-aware `/llms.txt` and `/llms-full.txt` generation for WooCommerce — daily auto-refresh, per-product exclusion, SEO-plugin description fallback, managed-host compatibility.
* Version Control with one-click restore and pin; non-destructive take-over of any existing `/llms.txt`.

== Upgrade Notice ==

= 1.0.0 =
Install and your products are in front of ChatGPT, Claude and Perplexity in 30 seconds.
