```skill
---
name: meta-ads-operator
description: Run daily Meta ads operations with decision-first analysis and controlled actions. Use when users ask to monitor Meta ads, answer the 5 daily questions, list exact ad names with spend, track AOV/CPA/ROAS goals, detect fatigue, pause losing ads, recommend scaling, or monitor landing page performance with URL links.
---

# Meta Ads Operator

Execute this workflow for each run.

## Inputs

- Read thresholds from `rules.yaml`.
- Use ad-level and campaign-level data from Meta Marketing API via CLI or direct connector.
- Include page analytics data source when available (GA4 or equivalent).

If required data access is missing, return a short blocking checklist with only missing items.

## Output Contract

Always return:

1. 5-question analysis block.
2. Exact ad names and spend values.
3. KPI status for AOV, CPA, and ROAS goals.
4. Action log (executed and approval-required).
5. Page performance section with destination links.

Use concise, decision-first language.

## Daily 5-Question Analysis

Answer these in order.

1) Am I on track?
- Compare spend pacing vs expected day pacing.
- Flag underspend or overspend with campaign names.

2) What is running?
- List active campaigns/ad sets/ads with status.
- Include exact ad name and current spend.

3) How is performance?
- Report 1d, 3d, and 7d for ROAS, CPA, AOV, CTR, CPC, frequency.
- State delta direction where possible.

4) Who is winning and losing?
- Rank ads best to worst by primary objective efficiency.
- Include exact ad name, spend, conversions, revenue, ROAS, CPA.

5) Any fatigue?
- Flag if frequency is rising while CTR declines and CPC rises.
- Mark risk level: low, medium, high.

## Decision Rules

Apply in this order.

1) Immediate kill rule (auto-pause)
- If ad spend > `2.5 * desired_cpa` and ROAS < 1.0, pause immediately.
- Log reason and numeric evidence.

2) Candidate pause rule
- If CPA > `3 * target_cpa` for >= 48h, mark pause candidate.
- Auto-pause only if rule is enabled in `rules.yaml`.

3) Scale rule (approval required by default)
- If ROAS >= 2.0 and minimum sample thresholds are met, recommend budget increase.
- Propose percent increase within cap in `rules.yaml`.

4) AOV/CPA goal checks
- Goal pass requires AOV > 1000 and CPA < 600.
- If either fails, add to guardrail alerts.

5) Fatigue handling
- If fatigue signal score exceeds threshold, recommend creative refresh test.

## Page Performance Monitoring

- For each active ad, capture destination URL.
- Report page-level trend indicators where available: LPV, CVR, bounce/engagement, speed score.
- Always include clickable page links in the brief.
- Highlight pages with significant change vs 7d baseline.

## Brief Format

Use the template in `references/brief-template.md`.

## Safety and Execution

- Always run in review mode first unless automation flags are explicitly enabled.
- Never execute destructive bulk actions without per-entity evidence.
- Keep budget shifts approval-required unless user explicitly enables auto-scale.
- Write every action and recommendation to a decision log.

```