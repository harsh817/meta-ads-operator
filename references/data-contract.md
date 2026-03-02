```markdown
# Data Contract

## Required Meta ad fields

- account_id
- campaign_id, campaign_name, campaign_status
- adset_id, adset_name, adset_status
- ad_id, ad_name, ad_status
- spend
- impressions, clicks, ctr, cpc, frequency
- purchases_or_leads (primary conversion)
- conversion_value (revenue)
- date_start, date_stop
- destination_url (final URL used by ad)

## Required computed metrics

- CPA = spend / conversions
- AOV = revenue / purchases
- ROAS = revenue / spend

## Optional but recommended page analytics fields

- sessions or LPV
- CVR
- bounce_rate or engagement_rate
- avg_page_load_time or speed score

## Connection checklist

- Meta API access token with ads read and ads management permissions
- Default ad account ID configured
- CLI or connector tested for read and write actions
- Destination page analytics source connected (GA4 or equivalent)

```