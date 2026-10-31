---
name: search-govopps
description: Search GovOpps for U.S. federal contract notices, grants, awards, forecasts, and related people or research specific opportunities. Use when a user asks to find or research government contracting or grant opportunities on GovOpps.
---

# Search GovOpps

GovOpps (https://govopps.us) is a free research preview maintained by Embersilk LLC. It is not affiliated with a government agency. Use available web access to search and follow results; no GovOpps account or API token is needed.

## Search

1. Turn the user's terms into a URL-encoded query at `https://govopps.us/search?q=...`. Start broad, then refine based on the user's needs and the site's available filters.
2. Limit the search with `type=opportunity`, `grant`, `award`, `forecast`, or `person`. Repeat `type` for multiple categories. Add `page=2`, `page=3`, and so on to paginate. Follow the site's next-page links when available.
3. Open relevant result links for details. Report the source links, meaningful dates and status as displayed, and any important uncertainty. Verify deadlines, eligibility, and solicitation details against the original government source before relying on them.

Examples:

- All categories: https://govopps.us/search?q=cybersecurity
- Grants: https://govopps.us/search?q=workforce&type=grant
- Florida contracting notices in NAICS 541512: https://govopps.us/search?q=software&type=opportunity&naics=541512&state=FL

### Opportunity filters

These parameters filter contracting opportunities. Specifying any of them switches the search to opportunity mode, even if other `type` values are present:

| Parameter | Meaning |
| --- | --- |
| `naics` | NAICS code; repeat the parameter or separate codes with commas. |
| `agency` | Agency hierarchy path. |
| `state` | Place-of-performance state code. |
| `zip` | Place-of-performance ZIP prefix. |
| `notice_type` | Notice type, such as `Solicitation` or `Sources Sought`. |
| `deadline_min`, `deadline_max` | Response deadline bounds in `YYYY-MM-DD` format. |
| `set_aside` | Set-aside type. |
| `keyword_mode` | Keyword matching mode; defaults to `relaxed`. |
| `solicitation_number` | Solicitation number. |

`agency`, `state`, `notice_type`, and `set_aside` can be repeated. URL-encode parameter values, and use values shown by the site when unsure of a filter's accepted value.

## Navigate

Browse notices at `/notices`, grants at `/grants`, awards at `/awards`, forecasts at `/forecasts`, documents at `/documents`, people at `/persons`, and prime subcontracting plans at `/subcontracting-plans`. Agency spending pages use `/agencies/<slug>/spending`. The guided contracting search is `/opportunity-finder`.

Detail links use `/opportunity/<notice_id>`, `/grants/<opp_id>`, `/entity/<uei>`, `/award/<internal_id>`, `/forecast/<source>/<forecast_id>`, `/documents/<document_id>`, and `/persons/<person_id>`. Prefer links returned by GovOpps to guessing identifiers.

## Fetch fallback

If the web-fetch tool fails or is blocked (including a Cloudflare challenge or access-denied page returned with HTTP 200), retry the same GovOpps URL once with `curl` through an available shell tool. Quote the URL so query parameters such as `&` are passed intact:

```bash
curl --fail --silent --show-error --location --max-time 30 'https://govopps.us/search?q=software&type=opportunity&naics=541512&state=FL'
```

Read the returned page before reporting results; a Cloudflare challenge or access-denied page is not search content. If `curl` also fails, returns a challenge or access-denied page (even with HTTP 200), or no shell tool is available, say so and provide the GovOpps link for the user to open in a browser. Do not claim to have seen results that were not retrieved.
