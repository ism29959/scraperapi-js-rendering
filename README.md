# Web Scraping API for JavaScript: How to Handle JS-Rendered Pages Without Losing Your Mind — ScraperAPI Explained, All Plans Compared, and Which One to Pick (Free Trial Included)

If you've ever written a scraper, pointed it at a site, and gotten back a blank `<div>` where the product data was supposed to be — welcome to the club. That's JavaScript rendering biting you. The page looks perfectly normal in a browser, but your script is seeing the skeleton: just the initial HTML shell before the JS fires and populates everything.

This is the single most common wall developers hit when scraping modern websites. And it's not going away. More sites are React, Vue, Next.js, or Angular than not. Lazy loading, infinite scroll, API-driven content — the whole internet seems to have decided that serving raw HTML is too straightforward.

So what do you actually do about it?

---

## Why JavaScript Rendering Breaks Your Scraper (And Why It's Not Your Fault)

Here's the thing: a regular HTTP request — the kind `requests` or `curl` or `fetch` makes — grabs the HTML document the server sends back. That's it. It doesn't run any JavaScript. Which means if a website loads its product prices, reviews, user data, or literally any content via a JS call after page load, you're never going to see it through a basic request.

The traditional solution was to spin up a headless browser — Puppeteer, Playwright, Selenium — and let it actually run the page the way Chrome would. That works. It also adds a whole layer of infrastructure to babysit: browser instances to manage, memory to watch, timeouts to tune, and detection systems on the target site that are specifically built to notice when you're running automated Chrome.

The alternative is using a **web scraping API for JavaScript** rendering — something that handles all of that headless browser infrastructure on its side and just hands you the rendered HTML when it's done. You stay in clean, simple API call territory. They deal with browsers, proxies, retries, and anti-bot countermeasures.

That's exactly what [ScraperAPI](https://www.scraperapi.com/?fp_ref=coupons) does. One line of code, one parameter, and you're pulling fully rendered page content without ever managing a browser yourself.

---

## What ScraperAPI Actually Is (No Fluff Version)

[ScraperAPI](https://www.scraperapi.com/?fp_ref=coupons) is a proxy-backed web scraping API that handles the messy parts of scraping — proxy rotation, headless browser execution, CAPTCHA solving, retries, and bot detection bypass — and returns the HTML (or structured data) you actually need. It routes requests through a pool of 40+ million IPs across 50+ countries.

The JavaScript rendering piece is the feature most developers come here for: you add `render=true` to your request, and ScraperAPI spins up a headless Chromium instance, loads the page fully, executes all the scripts, waits for the content, and returns the complete rendered HTML. You don't install a browser. You don't manage sessions. You send an API request and get back a fully loaded page.

Here's what that actually looks like:

javascript
// Node.js — scraping a JS-rendered page with ScraperAPI
import fetch from 'node-fetch';

const API_KEY = 'YOUR_API_KEY';
const TARGET_URL = 'https://example.com/dynamic-content';

const url = `http://api.scraperapi.com/?api_key=${API_KEY}&render=true&url=${encodeURIComponent(TARGET_URL)}`;

const response = await fetch(url);
const html = await response.text();
console.log(html);


That's the whole thing. No Puppeteer install, no browser binary management, no proxy configuration. The `render=true` flag does the heavy lifting on ScraperAPI's infrastructure.

You can also use the proxy mode if you're already running Puppeteer or Playwright and just want the anti-bot and proxy capabilities without switching paradigms:

javascript
// Proxy mode with axios — routes through ScraperAPI for protection
import axios from 'axios';

axios.get('http://example.com/', {
  proxy: {
    host: 'proxy-server.scraperapi.com',
    port: 8001,
    auth: {
      username: 'scraperapi.render=true',
      password: 'YOUR_API_KEY'
    },
    protocol: 'http'
  }
}).then(response => {
  console.log(response.data);
});


---

## What JavaScript Rendering Costs in Credits

This is the part that catches developers off guard, so it's worth spelling out clearly before you pick a plan.

ScraperAPI prices by API credits. A standard request to a plain webpage costs **1 credit**. When you add JavaScript rendering (`render=true`), that adds **10 credits** per request. But that's just the base multiplier — the target domain also affects cost:

| Target Type | Base Cost | With `render=true` | With `premium=true` + `render=true` |
|---|---|---|---|
| Standard page | 1 credit | 11 credits | 25 credits |
| E-commerce (Amazon) | 5 credits | 15 credits | 25 credits |
| SERP (Google, Bing) | 25 credits | 35 credits | — |
| Social (LinkedIn) | 30 credits | 40 credits | — |
| Cloudflare-protected | +10 credits | +10 extra | — |

So if you're scraping a typical e-commerce catalog that's React-rendered — think product pages where the prices and inventory load via JS — you're looking at roughly 15 credits per request instead of 1. That changes how far a plan's credit budget actually takes you.

ScraperAPI provides a Domain Multiplier tool in the dashboard and a `/account/urlcost` endpoint so you can check any URL's exact cost before you start burning through credits at scale. **Highly recommend running a few test URLs through that before committing to any plan.**

The `wait_for_selector` parameter is a useful companion to `render=true` for pages where content loads with a delay — it tells the browser to wait until a specific CSS selector appears before returning the response. No extra credit cost for that one.

---

## ScraperAPI Plans — Full Comparison

Here's every current plan on the platform, including the newer Professional and Advanced growth tiers announced in May 2026. All plans include JS rendering capability, automatic proxy rotation, CAPTCHA bypass, geo-targeting (scope varies by tier), custom sessions, automatic retries, and unlimited bandwidth.

| Plan | Monthly Price | Annual (10% off) | Credits/Month | Concurrent Threads | Geotargeting | PAYG | Get Started |
|---|---|---|---|---|---|---|---|
| **Free** | $0 | — | 1,000 | 5 | — | ❌ |  [Start Free](https://www.scraperapi.com/?fp_ref=coupons) |
| **Hobby** | $49/mo | $44.10/mo | 100,000 | 20 | US & EU | ❌ |  [Get Hobby Plan](https://www.scraperapi.com/?fp_ref=coupons) |
| **Startup** | $149/mo | $134.10/mo | 1,000,000 | 50 | US & EU | ❌ |  [Get Startup Plan](https://www.scraperapi.com/?fp_ref=coupons) |
| **Business** | $299/mo | $269.10/mo | 3,000,000 | 100 | Global | ❌ |  [Get Business Plan](https://www.scraperapi.com/?fp_ref=coupons) |
| **Scaling** ⭐ | $475/mo | $427.50/mo | 5,000,000 | 200 | Global | ✅ |  [Get Scaling Plan](https://www.scraperapi.com/?fp_ref=coupons) |
| **Professional** | $975/mo | $877.50/mo | 10,500,000 | 300 | Global | ✅ |  [Get Professional Plan](https://www.scraperapi.com/?fp_ref=coupons) |
| **Advanced** | $1,975/mo | $1,777.50/mo | 21,500,000 | 500 | Global | ✅ |  [Get Advanced Plan](https://www.scraperapi.com/?fp_ref=coupons) |
| **Enterprise** | Custom | Custom | 22M+ | 500+ | Global | ✅ |  [Contact Sales](https://www.scraperapi.com/?fp_ref=coupons) |

A few things this table doesn't make obvious:

**Geotargeting scope matters more than it sounds.** The Hobby and Startup plans are locked to US and EU proxies. If you need to scrape a site that serves different content by country — prices, product availability, localized listings — you need at least Business for global geo-targeting. Country-level targeting (`country_code=jp` for Japan, `country_code=br` for Brazil, etc.) is free once you're on a plan that supports it.

**Pay-as-you-go only unlocks at Scaling.** On Hobby, Startup, and Business, when you hit your credit ceiling mid-month, you're done until renewal — or you upgrade. Starting from the Scaling plan, PAYG overflow kicks in automatically, so a spike in scraping jobs doesn't kill your pipeline. There's a spending cap you can configure to prevent surprise bills.

**Professional and Advanced are the new growth tiers.** ScraperAPI introduced these in May 2026 specifically for teams that had outgrown the 5M-credit Scaling plan but didn't want to jump straight to a custom Enterprise arrangement. Professional includes a 250K credit bonus and Advanced includes 500K — limited-time offers worth factoring in if you're in that volume range.

**The free plan is a real free plan, not a trial.** 1,000 credits per month, 5 concurrent connections, permanent. Enough to build and test a small project, not enough for anything production-scale. New signups also get a separate 7-day trial at 5,000 credits to stress-test against real targets before choosing a paid plan.

---

## How ScraperAPI Handles JavaScript-Heavy Sites: The Technical Picture

The `render=true` parameter routes your request through a headless Chromium instance. That browser loads the page, executes all JavaScript, waits for the DOM to settle, and then the HTML is captured and returned. This handles:

- **Single-page applications (SPAs)** built in React, Vue, Angular, Svelte — the ones where navigating the site never actually triggers a new page load
- **Lazy-loaded content** — images, product data, review widgets that only appear after the user "scrolls into view"
- **API-driven pages** — where the frontend JS makes fetch calls to internal APIs and populates the DOM from the response
- **Infinite scroll** — ScraperAPI lets you combine `render=true` with `wait_for_selector` to wait for the final loaded state before capturing

For pages where content appearance timing is unpredictable, `wait_for_selector` is the tool to reach for:

javascript
// Wait for the product grid to load before capturing
const url = `http://api.scraperapi.com/?api_key=${API_KEY}&render=true&wait_for_selector=.product-grid&url=${encodeURIComponent(TARGET_URL)}`;


This tells ScraperAPI to hold the Chromium instance open until `.product-grid` appears in the DOM — no arbitrary `setTimeout` guesswork needed.

For large-scale JavaScript scraping jobs — hundreds of thousands of URLs — the **async mode** is worth using. Instead of waiting synchronously for each rendered response (which can take several seconds per page), you submit jobs to the async endpoint and poll for results when they're ready. ScraperAPI handles retries internally for up to 24 hours:

javascript
// Submit an async rendering job
import axios from 'axios';

const job = await axios.post('https://async.scraperapi.com/jobs', {
  apiKey: 'YOUR_API_KEY',
  url: TARGET_URL,
  apiParams: { render: 'true' }
});

console.log('Job ID:', job.data.id); // Poll this ID for the result


---

## Who Each Plan Is Actually For

Rather than repeating the feature table, here's the honest version of who ends up on each tier based on real usage patterns:

**Free / Free Trial** — Developers in the early "does this actually work for my target?" phase. Run the trial against your real target URLs, watch the credit consumption, and use that data to pick a paid plan. Don't guess.

**Hobby ($49/mo)** — Side projects, personal tools, small monitoring scripts. If your scraping target is mostly plain pages with occasional JS rendering, 100K credits at this price is reasonable. Amazon + rendering = 15 credits per request, so your effective limit there is roughly 6,600 product pages per month. Fine for a price tracker that checks 200 products daily; tight for anything bigger.

**Startup ($149/mo)** — Small SaaS products, freelancers with a handful of clients, agencies running regular data collection jobs. 1M credits is a significant step up. Still limited to US/EU geo, which rules it out for globally distributed scraping.

**Business ($299/mo)** — The first plan with global geo-targeting, which is the real differentiator. If your scraping needs country-level targeting outside the US/EU, this is where you start. 3M credits, 100 concurrent threads, unlimited analytics history in the dashboard.

**Scaling ($475/mo)** — The sweet spot for teams running production-scale pipelines. 5M credits, 200 concurrent threads, and — crucially — pay-as-you-go overflow so credit spikes don't bring your jobs to a halt mid-run.

**Professional / Advanced ($975–$1,975/mo)** — High-volume teams that need 10M+ credits per month and don't want the overhead of negotiating a custom Enterprise deal. The new bonus credit offers on these tiers (250K and 500K respectively) are worth the look if you're already planning to sign up at this scale.

**Enterprise (Custom)** — 22M+ credits per month, fully negotiated pricing, custom SLAs. If you're at this scale, you probably already know you need to talk to their sales team directly.

---

## ScraperAPI vs. Other JS-Rendering Scraping APIs

The **web scraping API for JavaScript** space has gotten more crowded. Here's where ScraperAPI actually sits relative to the alternatives most developers compare it against:

**ScraperAPI vs. ScrapingBee** — Both start at $49/month and have similar developer experiences. ScrapingBee has an official Python SDK; ScraperAPI doesn't (raw requests only). ScrapingBee's JS rendering costs 5x credits per request; ScraperAPI's `render=true` adds 10 flat credits. Which is cheaper depends on your mix of base domain costs.

**ScraperAPI vs. Bright Data** — Not really the same tier. Bright Data starts around $499/month and is aimed at enterprises where success rates on highly protected sites are non-negotiable. ScraperAPI is the better starting point for most developers; Bright Data is where you go if you've exhausted it.

**ScraperAPI vs. Scrape.do** — Scrape.do undercuts ScraperAPI on entry price ($29/mo), but that Hobby tier actually strips out JS rendering — you need the Pro plan at $99/mo to get it back. Factor that in when comparing sticker prices.

**ScraperAPI vs. Oxylabs** — Oxylabs has OxyCopilot (AI-assisted code generation from prompts) and structured JSON output for specific platforms. More feature-rich, more complex to set up, costs scale faster. ScraperAPI wins on simplicity and predictability for straightforward HTML+JS scraping.

The honest summary: for most developers who need a **web scraping API for JavaScript rendering** without wanting to manage their own headless browser fleet, ScraperAPI is a solid, well-documented default — especially in the $49–$299/month range. The complexity ceiling is low, the integration is genuinely a few lines of code, and the free trial lets you validate before committing.

---

## What Real Users Say

ScraperAPI holds a **4.5/5 on Trustpilot** (43+ reviews) with 93% five-star ratings, and **4.4/5 on G2** (16 reviews). The recurring themes in positive reviews are the same: clean documentation, quick onboarding, proxy rotation that "just works" without tuning.

The main criticism that shows up consistently isn't about reliability — it's about credit math being non-obvious. The sticker number of credits on a plan and your actual effective monthly scrape count can be very different things once you factor in rendering multipliers, domain multipliers, and any anti-bot bypass costs. Running the cost estimator against your real targets before signing up is genuinely the most important thing you can do before choosing a plan.

> "Proxy rotation was seamless. It saved me hours of debugging session management and IP block issues." — 12-year web data consultant on Trustpilot

---

## Quick Start: Using ScraperAPI for JS Rendering in 3 Steps

**Step 1 — Sign up and grab your API key.** 👉 [Start the free trial here — 5,000 credits, no credit card required](https://www.scraperapi.com/?fp_ref=coupons). Your API key is in the dashboard immediately after signup.

**Step 2 — Test your target URL's credit cost.** Before running anything at scale, check the actual per-request cost for your specific target:


https://api.scraperapi.com/account/urlcost?api_key=YOUR_API_KEY&url=YOUR_TARGET_URL&render=true


This tells you exactly how many credits one successful request to that URL costs with rendering enabled.

**Step 3 — Make your first rendered scrape.** For Node.js:

javascript
import fetch from 'node-fetch';

const result = await fetch(
  `http://api.scraperapi.com/?api_key=YOUR_API_KEY&render=true&url=${encodeURIComponent('https://your-target.com')}`
);

const html = await result.text();
console.log(html); // Fully rendered HTML, JS executed


For Python:

python
import requests

response = requests.get(
    'http://api.scraperapi.com/',
    params={
        'api_key': 'YOUR_API_KEY',
        'render': 'true',
        'url': 'https://your-target.com'
    }
)

print(response.text)  # Fully rendered HTML


If the content you need only appears after a specific element loads:

python
response = requests.get(
    'http://api.scraperapi.com/',
    params={
        'api_key': 'YOUR_API_KEY',
        'render': 'true',
        'wait_for_selector': '.your-content-container',
        'url': 'https://your-target.com'
    }
)


---

## Frequently Asked Questions

**Does every JavaScript page require `render=true`?**
Not necessarily. Some pages send all content in the initial HTML response and use JS only for UI interactions. Try without `render=true` first — if you get the data you need, save the extra credits. Add it only when you see blank content or missing data in the response.

**What about geotargeting with JS rendering?**
Geo-targeting (`country_code` parameter) works alongside `render=true` at no extra credit cost. So you can render a page as-seen from a Japanese IP address just by combining both parameters. Global geo requires at least the Business plan.

**Can I use `render=true` with async mode?**
Yes. Async mode supports all the same parameters as synchronous mode. For large JavaScript-rendered scraping jobs, async is actually the better path — it removes the timeout pressure on long-running renders and ScraperAPI handles retries automatically.

**What happens if a render fails?**
ScraperAPI only charges credits for successful requests (HTTP 200 or 404 responses). A failed render doesn't burn your credits — you're only paying for the data actually delivered.

**Is there a cap on how long the headless browser waits?**
There's an internal retry and wait logic built into ScraperAPI's render pipeline. The `wait_for_selector` parameter gives you explicit control over waiting for content appearance. For unusual pages where content takes a very long time to load, the async endpoint is the right approach since it has a much longer timeout ceiling than synchronous requests.

---

## The Bottom Line on Picking a Plan

The biggest mistake people make when choosing a web scraping API for JavaScript rendering is looking at the raw credit count and treating it like a request count. Those two numbers are the same only for basic, unprotected, non-JS pages. Add `render=true`, and you've added 10 credits per request. Add Amazon as a target, and you've added 5 more. You can do the math before signing up — ScraperAPI's cost estimator exists precisely for this.

If you're just getting started, 👉 [claim the 7-day free trial with 5,000 credits](https://www.scraperapi.com/?fp_ref=coupons), point it at your actual targets with `render=true` enabled, and let the dashboard tell you your real per-request cost. That number tells you exactly which plan fits — and whether scraping that specific site is even economically viable at the volume you're planning.

The annual billing discount is automatic — 10% off, no coupon needed, just switch from monthly to yearly at checkout.

For personal projects and small tools, Hobby at $49/mo handles a surprising amount of ground. For production workloads with global geo needs, Business at $299/mo is the logical entry point. For teams that need PAYG overflow so unexpected traffic spikes don't break anything, Scaling at $475/mo is where that safety net kicks in.

Whatever you're building, the right starting move is the same: 👉 [try it free, test against your real targets, then decide](https://www.scraperapi.com/?fp_ref=coupons).
