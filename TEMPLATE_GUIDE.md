# Visualization Template Guide

This repository started with specific Teams demos. `visualization_template.html` turns the same idea into a reusable template.

## Core abstraction

The template separates **data contract** from **rendering logic**.

- `TEMPLATE.data`: your entities (teams, projects, apps, cost centers, etc.)
- `TEMPLATE.dimensions`: categorical fields you want to cluster/color by
- `TEMPLATE.modes`: scenario-specific views (e.g., landscape, risk, growth)
- `TEMPLATE.filters`: reusable filter functions

You only change the `TEMPLATE` object; the UI and D3 rendering are reused.

## Data contract (minimal)

Each entity should include:

- `name` (string)
- `owner` (string)
- `members` (number) for bubble size
- one or more dimension keys used in `dimensions` and `modes` (e.g., `group`, `risk`)

## Reuse scenarios from the blog

### Governance / CISO view
- cluster by `risk`
- filters: single-owner risk, guest access, ghost teams, data exposure

### Collaboration architecture
- cluster by `function` or `crossDeptIndex`
- filters: bridge teams, bottlenecks, high-centrality teams

### Growth & lifecycle
- cluster by `growthBand`
- filters: rapid growth, inactive > 180 days, renewal overdue

### Cost intelligence
- cluster by `storageBand` or `licenseMix`
- filters: high storage + low activity, guest/member imbalance

## Suggested production flow

1. Graph + PowerShell / API job exports normalized JSON daily.
2. Optional enrichment (HR, org roles, naming normalization).
3. Feed JSON to the template contract.
4. Publish static HTML in SharePoint/Portal, refresh data on schedule.

## Why this scales better than one-off pages

- one rendering engine, many use cases
- consistent interactions and visual language
- easier to test/iterate prompts for LLM-generated views
- mode/filter catalog can grow without redesigning the whole page
