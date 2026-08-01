# Trade Show Exhibitor Lead Scoring for n8n - Free Apify to Google Sheets Workflow

A complete n8n workflow that fetches a public trade-show exhibitor directory through the Apify actor you configure, normalizes the companies, scores ICP fit, and appends every scored exhibitor to Google Sheets.

Free to download and use. There are no disabled nodes or upgrade stubs; the workflow is complete on its own.

**Download:** [`workflow/trade-show-exhibitor-lead-scoring-free.json`](workflow/trade-show-exhibitor-lead-scoring-free.json)

## What it actually does

1. Starts on demand when an exhibitor directory is ready.
2. Calls the trade-show or exhibitor-directory actor you configure in Apify.
3. Normalizes the actor output, removes blank and duplicate companies within the run, and caps the batch at 25.
4. Scores each exhibitor against your ICP criteria and gives a short reason.
5. Appends every scored exhibitor to the `Exhibitors` tab in Google Sheets.

The workflow logs low scores too, leaving you with a complete event research sheet rather than only a hidden shortlist.

## What you need

Three credentials:

| # | Credential | Used for |
|---|---|---|
| 1 | Apify API token via Header Auth | Running the exhibitor-directory actor and retrieving its dataset |
| 2 | OpenAI-compatible API key via Header Auth | Scoring the normalized exhibitors |
| 3 | Google Sheets OAuth account | Appending the scored exhibitor rows |

You also need an n8n Cloud or compatible self-hosted instance.

## Setup

1. Import `workflow/trade-show-exhibitor-lead-scoring-free.json` into n8n.
2. Open **Your settings (EDIT ME)** and enter the trade-show URL, exhibitor-directory URL, your ICP description, and your fit criteria.
3. Open **Fetch exhibitor list (Apify)**. Replace `YOUR-USERNAME~YOUR-ACTOR` with your actor ID.
4. Replace the empty `{}` request body with that actor's own documented input parameters.
5. Connect the three credentials listed above.
6. Create a Google Sheet with a tab named `Exhibitors`, add the exact header row below, and paste the sheet URL into **Log scored exhibitors (Google Sheets)**.
7. Run the workflow once and inspect the appended rows.

Exact sheet headers:

```text
processedAt companyName contactName contactEmail website boothOrListingDetail sourceUrl tradeShowUrl exhibitorDirectoryUrl icpScore reason
```

### Which Apify actor?

Use any suitable trade-show or exhibitor-directory actor, provided you supply that actor's own input parameters. Actor input bodies are not interchangeable, so the empty `{}` body is intentionally not presented as universal.

The output normalizer is actor-agnostic. It maps common exhibitor field aliases without depending on a specific actor ID. If your chosen actor uses different output names, extend the aliases in **Normalize and dedupe exhibitors**.

## Paid edition

The [Competitive Intel Pack paid edition](https://willowridge7.gumroad.com/l/n8n-competitive-intel-pack) adds the Salesforce Lead delivery workflow and the buyer setup package. This free workflow remains fully usable without it.

## Licence

Free to use and modify for your own business or your clients' businesses, including agency deployments.

**Not open source.** You may not resell, redistribute, sublicense, or repackage the workflow itself as your own product. See [LICENSE.txt](LICENSE.txt).

## Honest status

This repository was published recently. It has no users, no reviews, and no results to claim. Nothing here is a customer-success or performance claim; inspect the workflow and judge it on what it does.

Built by [Rook Data Tools](https://apify.com/rook-data-tools).

## Related

Other free workflows and guides we publish:

- [n8n-ai-lead-scoring](https://github.com/willowridge1234/n8n-ai-lead-scoring) — Free workflow — score scraped leads against your ICP, log to Google Sheets
- [n8n-review-intent-lead-scoring](https://github.com/willowridge1234/n8n-review-intent-lead-scoring) — Free workflow — score G2/Capterra reviewers by switching intent
- [n8n-lead-scoring-guide](https://github.com/willowridge1234/n8n-lead-scoring-guide) — Guide — which signals predict a good lead, and how to tell if scoring works
- [chamber-association-lead-lists](https://github.com/willowridge1234/chamber-association-lead-lists) — Guide — building B2B lead lists from chamber & association directories
- [memberclicks-directory-export-guide](https://github.com/willowridge1234/memberclicks-directory-export-guide) — Guide — exporting a public MemberClicks member directory
- [new-liquor-license-data-guide](https://github.com/willowridge1234/new-liquor-license-data-guide) — Guide + tool — building a lead list from public liquor-licence records
- [chicago-food-service-license-data-guide](https://github.com/willowridge1234/chicago-food-service-license-data-guide) — Guide + tool — building a lead list from Chicago food-service licence records
- [wild-apricot-directory-export-guide](https://github.com/willowridge1234/wild-apricot-directory-export-guide) — Guide — exporting a public Wild Apricot member directory
