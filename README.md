# ScraperAPI Premium Proxy: 10, 25, 30 or 75 Credits per Request — What That Costs on Each Plan, When the Flag Is Worth Turning On, and Which Tier Fits Your Volume (Full Pricing Table)

`premium=true` bills **10 API credits for every successful request**. Add JavaScript rendering (`render=true`) and the same request costs **25 credits**. The higher tier, `ultra_premium=true`, costs **30 credits**, or **75 with rendering**. Every paid plan can send requests through these pools, and the standard pool — millions of proxies from more than a dozen ISPs, per ScraperAPI's own documentation — is described as sufficient for "the vast majority of scraping jobs."

The cost is where most decisions get made, so that's where this starts. Below: the full plan lineup with current prices, the per-request premium unit cost on each tier, the two parameters that cannot be combined, the header rule that silently breaks requests, and the billing behaviour that only shows up in the FAQ.

## Quick picks before the details

Most people testing premium proxies land on **Hobby at $49/month**: 100,000 credits, which is roughly **10,000 premium requests** at 10 credits each, with 20 concurrent threads. If premium requests are the main workload, **Business at $299/month** changes the math hard: 3,000,000 credits buys about 300,000 premium requests, dropping the unit cost from $0.0049 to roughly **$0.001 per request**.

👉 [Compare all ScraperAPI plans and current prices](https://scraperapi.com/pricing?fp_ref=coupons)

## All ScraperAPI plans, including the ones you'll probably skip

Prices below are the official monthly rate and the annual rate as displayed (billed annually, shown as a monthly equivalent). All figures in USD.

| Plan | Monthly price | Annual (per month, billed annually) | API credits | Concurrent threads | Link |
| --- | --- | --- | --- | --- | --- |
| Hobby | $49 | $44.10 | 100,000 | 20 | [View Hobby pricing](https://scraperapi.com/pricing?fp_ref=coupons) |
| Startup | $149 | $134.10 | 1,000,000 | 50 | [View Startup pricing](https://scraperapi.com/pricing?fp_ref=coupons) |
| Business | $299 | $269.10 | 3,000,000 | 100 | [View Business pricing](https://scraperapi.com/pricing?fp_ref=coupons) |
| Scaling (marked most popular) | $475 | $427.50 | 5,000,000 | 200 | [View Scaling pricing](https://scraperapi.com/pricing?fp_ref=coupons) |
| Professional | $975 | $877.50 | 10,500,000 | 300 | [View Professional pricing](https://scraperapi.com/pricing?fp_ref=coupons) |
| Advanced | $1,975 | $1,777.50 | 21,500,000 | 500 | [View Advanced pricing](https://scraperapi.com/pricing?fp_ref=coupons) |
| Enterprise | Custom (let's talk) | Custom | 22,000,000+ | 500+ | [See Enterprise options](https://scraperapi.com/pricing?fp_ref=coupons) |

Two differences hide outside the credit column, and they matter more than the price gap between Startup and Business suggests:

| Plan | Geotargeting | Analytics dashboard | Running past your credits |
| --- | --- | --- | --- |
| Hobby | US & EU only | Last 30 days | Auto-upgrade (opt-in) |
| Startup | US & EU only | Last 30 days | Auto-upgrade (opt-in) |
| Business | Country-level | Unlimited | Auto-upgrade (opt-in) |
| Scaling | Country-level | Unlimited | Auto-upgrade, or pay-as-you-go |
| Professional | Country-level | Unlimited | Auto-upgrade, or pay-as-you-go |
| Advanced | Country-level | Unlimited | Pay-as-you-go |
| Enterprise | Country-level | Unlimited | Pay-as-you-go |

If your premium proxy work involves targeting a specific country outside the US or EU, Hobby and Startup cannot do it. Country-level geotargeting starts at Business. The same applies to the analytics window: 30 days of history on the two cheapest plans, unlimited from Business up.

One display quirk worth knowing: the pricing page lists "Pay as you go" under every tier, but the FAQ restricts it to **Scaling, Professional, Advanced and Enterprise**. Treat the FAQ as the accurate range. Auto-upgrade, the opt-in setting that bumps you to the next plan when credits run out, is available on Hobby through Professional.

## Premium vs Ultra Premium: the parameters side by side

|  | `premium=true` | `ultra_premium=true` |
| --- | --- | --- |
| Credits per successful request | 10 | 30 |
| With `render=true` | 25 | 75 |
| Who can use it | All paid plans | Paid plans only |
| Caching | Standard behaviour | Requests cached by default |
| Custom headers | Forwarded when `keep_headers=true` | **Discarded**, even with `keep_headers=true` |
| Can be combined with the other flag | No | No |

The mutual exclusion is stated plainly in the docs: "These two parameters are mutually exclusive, so they cannot be used at the same time." Sending both does not give you a super-pool; it gives you a malformed request.

The header rule is the more expensive mistake. If `ultra_premium=true` is set, ScraperAPI discards every custom header, including the ones you asked to keep with `keep_headers=true`. Any target that authenticates through a custom header, a bearer token, or a specific `Accept-Language` will behave differently once ultra premium is on. Test with `premium=true` first if your request depends on headers at all.

Ultra premium requests are also cached by default to improve performance. If you are polling a price or a stock level, that default matters to how fresh your data is.

## What a premium request actually costs on each plan

Divide the credit allowance by 10 and you get the number of premium requests a plan covers if every single credit went to premium traffic. Divide the price by that number and you get the effective unit cost.

| Plan | Credits | Premium requests (at 10 credits) | Cost per premium request (monthly) | Cost per premium request (annual) |
| --- | --- | --- | --- | --- |
| Hobby | 100,000 | 10,000 | $0.0049 | $0.00441 |
| Startup | 1,000,000 | 100,000 | $0.00149 | $0.00134 |
| Business | 3,000,000 | 300,000 | ≈$0.000997 | ≈$0.000897 |
| Scaling | 5,000,000 | 500,000 | $0.00095 | $0.000855 |
| Professional | 10,500,000 | 1,050,000 | ≈$0.000929 | ≈$0.000836 |
| Advanced | 21,500,000 | 2,150,000 | ≈$0.000919 | ≈$0.000827 |

The curve flattens fast. Hobby to Business is roughly a 5x improvement in unit cost. Business to Advanced is another 8% and $1,676 a month. If you are choosing between the top three tiers purely on premium proxy economics, you are optimising the wrong decimal.

Rendering changes the picture at the low end. At 25 credits per premium-plus-render request, Hobby covers about **4,000 requests** ($0.01225 each), Startup about **40,000** ($0.003725 each), and Business about **120,000** (≈$0.00249 each). At the ultra tier, 30 credits per request means Business covers about 100,000 requests (≈$0.00299 each); with rendering at 75 credits, that falls to about 40,000 (≈$0.007475 each).

These are theoretical figures. In practice premium calls get mixed with 1-credit standard pages and with per-domain surcharges, so your blended cost sits somewhere below the numbers above.

👉 [Pick the tier that matches your monthly premium volume](https://scraperapi.com/pricing?fp_ref=coupons)

## Per-domain costs stack on top, and ScraperAPI doesn't publish the combined number

Separate from the proxy flags, certain targets carry their own credit price: a standard page is 1 credit, Amazon is 5, Google and Bing including subdomains are 25, LinkedIn is 30, and sites behind Cloudflare, Datadome or PerimeterX add 10 credits per request when ScraperAPI bypasses them.

The documentation gives four explicit premium figures (10, 25, 30, 75) and does not state what a premium request to Amazon or Google costs in total. Anyone quoting you a combined number is doing arithmetic the vendor hasn't published. Check the exact cost for your URL with the **Domain Cost Estimator** in the dashboard, and set `max_cost` on a scrape so a single unexpectedly expensive request gets refused rather than billed.

## When premium is actually necessary

ScraperAPI's own framing is that the standard pool handles "the vast majority" of jobs and the residential and mobile pool exists "for the difficult-to-scrape sites." The practical version of that:

- **You are getting blocked on a target that serves residential or mobile traffic only.** Datacenter IP ranges are the first thing many sites filter, and no amount of retrying fixes a pool-level block.
- **You need a consumer-facing session that looks like a real device.** Mobile-first sites, app APIs and regional retailers fall here.
- **Standard requests return challenge pages rather than content.** If every response is a CAPTCHA or an interstitial, the extra 9 credits buys you a response instead of nothing.
- **A single failed request costs more than 10 credits of your time.** At Business pricing, a premium request is about a tenth of a cent. Engineering hours spent debugging a blocked pipeline are not.

What premium does not fix: a target that requires country-level geotargeting on a Hobby or Startup plan (upgrade to Business), or a request that depends on custom headers being forwarded while ultra premium is enabled (drop to `premium=true`).

Because the flag is per request, you don't have to choose between "cheap" and "works" for the whole account. Route only the hard domains through `premium=true` and leave everything else on the standard pool at 1 credit. A pipeline with 90% easy pages and 10% hostile ones costs a fraction of one where every call carries the multiplier.

## Three ways to send a premium request

**API request.** Add the flag to the query string:


https://api.scraperapi.com?api_key=API_KEY&premium=true&url=https://example.com/


**Async request.** POST to `https://async.scraperapi.com/jobs` with the flag inside `apiParams`:

json
{
  "apiKey": "API_KEY",
  "url": "https://example.com/",
  "apiParams": { "premium": "true" }
}


**Proxy mode.** The flag lives in the proxy username:


http://scraperapi.premium=true:API_KEY@proxy-server.scraperapi.com:8001


Swap `premium=true` for `ultra_premium=true` in any of the three to move to the higher pool, keeping the mutual exclusion and header rules in mind.

## Billing rules that aren't on the pricing page

**Annual pricing is a monthly equivalent, not a total.** The $269.10 figure for Business is what you pay per month when billed annually, which means **$3,229.20 charged once a year** against $3,588 on monthly billing, a saving of $358.80. Hobby works out to $529.20/year versus $588; Startup to $1,609.20 versus $1,788.

**Credits reset, they don't roll over.** Unused credits are gone at renewal. Size your plan to your actual monthly ceiling, not to a peak month.

**Going over your thread limit is free but not queued.** Exceeding concurrent threads returns a 429 asking you to reduce concurrency and retry. The request is turned away rather than queued, and there's no surcharge.

**Enterprise discounts have one carve-out.** Custom volume pricing applies across your usage "with the exception of requests to Ultra Premium which carry their own minimum rate." If your workload is ultra-premium-heavy, the negotiated discount won't apply to those requests at the same rate.

**Free plan and free trial are two different things.** The permanent free plan gives 1,000 credits and a maximum of 5 concurrent connections. The 7-day trial gives 5,000 credits and requires no credit card. If you want to benchmark premium success rates against your own targets before paying, the trial is the larger allowance.

**The refund window is 7 days, no questions asked.** Contact support and it's refunded. Cancellation is free and can be done from the dashboard at any time.

👉 [Start the 7-day trial with 5,000 credits](https://dashboard.scraperapi.com/signup)

## Choosing between the tiers

Premium volume under about 10,000 requests a month: Hobby, and accept the US/EU geotargeting limit. Between 10,000 and 100,000 premium requests, or any need for specific countries: Business, because Startup costs half as much but can't target a country and the unit cost is 50% higher. Past roughly 300,000 premium requests a month, the gap between Business, Scaling and Professional narrows to fractions of a cent and the decision should be driven by concurrency and credit headroom rather than unit price.

Two checks before you enter a card: run a handful of your hardest URLs through the Domain Cost Estimator so the credits-per-request figure you plan around is the real one, and set `max_cost` on production scrapes so a single misconfigured request can't drain a month of credits.

👉 [Check current ScraperAPI pricing and start with the smallest plan that fits](https://scraperapi.com/pricing?fp_ref=coupons)
