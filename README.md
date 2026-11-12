# Hiring Signals — who is hiring, for what, and how fast

[![Run on Apify](https://img.shields.io/badge/Run%20on-Apify-00a76f?style=for-the-badge)](https://apify.com/jobdata_labs/hiring-signals)

> **Hosted version:** run it in the cloud, no install, pay per result: **[Hiring Signals: Company Hiring Activity & Growth Tracker](https://apify.com/jobdata_labs/hiring-signals)**

Get a **hiring activity report for each company on your list**: open roles, new roles in the last 7 and 30 days, which teams and countries are growing, remote share, seniority mix — and **what changed since your last check**. Built for sales teams, investors, recruiters and market researchers who use hiring as a buying or growth signal.

Data comes from the **official public job-board APIs** of 8 applicant tracking systems (Greenhouse, Lever, Ashby, SmartRecruiters, Workable, Recruitee, Personio, Teamtailor). No LinkedIn scraping, no logins, no proxies — stable and compliant.

## One row per company

```json
{
  "company": "Stripe",
  "openJobs": 762,
  "newJobsLast7Days": 74,
  "newJobsLast30Days": 245,
  "medianPostingAgeDays": 49,
  "remoteSharePct": 14.7,
  "topFunctions": [{ "name": "engineering", "count": 288 }, { "name": "sales", "count": 159 }],
  "topDepartments": [{ "name": "Account Executives (EMEA)", "count": 46 }],
  "topLocations": [{ "name": "Dublin", "count": 60 }, { "name": "Singapore", "count": 49 }],
  "seniorityMix": [{ "name": "lead / manager", "count": 261 }],
  "hiringScore": 63,
  "openJobsChange": 12,
  "newJobsSincePreviousCheck": 31,
  "closedJobsSincePreviousCheck": 19,
  "recentJobs": [{ "title": "Account Executive, Benelux", "location": "Dublin", "url": "..." }]
}
```

- **hiringScore (0–100)** combines team size, recent posting velocity and growth since your previous check, to rank accounts quickly.
- **Functions** (engineering, sales, data & AI, marketing, customer, …) and **seniority** are inferred from job titles.
- **Change tracking**: schedule the Actor weekly and every report shows new and closed roles since the last run.

## Use cases

- **Sales prospecting / intent data:** a company hiring 10 data engineers is buying data tools. Prioritize accounts by hiringScore and the functions you sell to.
- **Investors & market research:** compare hiring velocity across a portfolio or competitors.
- **Recruiting agencies:** spot companies scaling teams you place candidates in.
- **Automations:** send weekly changes to Google Sheets, Slack or your CRM with Apify integrations.

## Input

A list of companies: direct ATS URLs (`https://jobs.lever.co/palantir`), shorthands (`greenhouse:stripe`) or a company's own careers page (the embedded ATS is auto-detected; robots.txt respected).

## Pricing

Pay per event: **one fee per company report**. Failed inputs are not charged.

## Notes

- Only companies whose openings are on one of the 8 supported ATS can be analyzed. Need ATS Jobs Monitor's full job lists instead? See [ATS Jobs Monitor](https://apify.com/jobdata_labs/ats-jobs-monitor).
- No personal data is collected.

---

## Run it via API

```bash
curl -X POST "https://api.apify.com/v2/acts/jobdata_labs~hiring-signals/run-sync-get-dataset-items" \
  -H "Authorization: Bearer $APIFY_TOKEN" -H "Content-Type: application/json" \
  -d '{"companies": ["greenhouse:stripe", "https://jobs.ashbyhq.com/notion", "https://bunq.recruitee.com"]}'
```

```js
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('jobdata_labs/hiring-signals').call({
    "companies": [
        "greenhouse:stripe",
        "https://jobs.ashbyhq.com/notion",
        "https://bunq.recruitee.com"
    ]
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
```

## Use it from AI agents (MCP)

```json
{
  "mcpServers": {
    "hiring-signals": {
      "url": "https://mcp.apify.com?tools=jobdata_labs/hiring-signals",
      "headers": { "Authorization": "Bearer <YOUR_APIFY_TOKEN>" }
    }
  }
}
```

## More tools by jobdata_labs

All tools: [apify.com/jobdata_labs](https://apify.com/jobdata_labs) · [SEO Audit Crawler](https://apify.com/jobdata_labs/seo-audit-crawler) · [Sitemap Change Monitor](https://apify.com/jobdata_labs/sitemap-change-monitor) · [RSS Feed Monitor](https://apify.com/jobdata_labs/rss-feed-monitor) · [Tech Stack & DNS Detector](https://apify.com/jobdata_labs/tech-stack-dns-detector)
