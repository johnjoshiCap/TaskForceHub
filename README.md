# TaskForceHub
This is for TENS Dashboard develop - Non-Profit
# TENS Dashboard — TEN Projects: TAPC & oTherm Explorer

Interactive explorer profiling 18 thermal energy network and district energy projects
across the US and Canada, each mapped against the TAPC business-model / financing
framework and the oTherm.org M&V methodology.

**Version:** v5 — update to the TENS dashboard in the CapUtility LL97 app, Task Force section.

## Quick start

Single self-contained static HTML file. No build step, no dependencies to install.

```
open index.html
```

or

```
python3 -m http.server 8000   # then http://localhost:8000
```

## Integration

See **[BUILD.md](BUILD.md)** for placement, runtime requirements, and the external CDN
dependencies flagged for security review.

## Contents

| File | Purpose |
|---|---|
| `index.html` | The dashboard. All markup, styles, scripts and project data inline. |
| `BUILD.md` | Integration and security-review notes for the CapUtility team. |

## Data sources

All content is drawn from public regulatory filings and operator disclosures, including
NY PSC Case 25-S-0741 (Con Edison Steam Rate Filing) Clean Energy Transition Panel
exhibits, the 2009 East River Repowering Project Cost Allocation Study, PSC Case
22-M-0429 UTEN Stage 2 filings, and MA DPU networked geothermal filings. Per-project
citations appear in the "Sources" line of each profile.

No proprietary, confidential, or personally identifiable data. No secrets in this repo.
