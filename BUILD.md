# BUILD.md — TENS Dashboard (TEN Projects: TAPC & oTherm Explorer)

## What it is

The **TENS dashboard** — an interactive explorer profiling 18 thermal energy network
(TEN) and district energy projects across the US and Canada, each mapped against the
TAPC business-model / financing framework and the oTherm.org M&V methodology.

Views: project profiles, an interactive map, three comparison tables, the TAPC roadmap,
and the TAPC/oTherm reference framework.

**Version:** v5 (`TEN_Projects_TAPC_Explorer_v5.html`, delivered here as `index.html`)

## This is an update, not a new feature

This **replaces the existing TENS dashboard** currently live in the Task Force section.
It is a content and structure update to the same single-page app — no new routes,
no new services, no new dependencies beyond what the current version already loads.

### What changed in v5

- Renamed "Con Edison Steam System" → **"Con Edison District Steam System"** (aligns
  with IDEA district energy terminology). Note: the project `id` (3) is unchanged, so
  any existing deep links by id still resolve.
- Full rewrite of the Con Edison profile, reviewed and corrected by Con Edison, and
  sourced to NY PSC Case 25-S-0741 Clean Energy Transition Panel exhibits, the 2009
  East River Repowering Project Cost Allocation Study, and the 2004 Steam Rate Order.
- **Two new profile categories added to all 18 projects:** "Avoided Emissions" and
  "Avoided Electric Peaks."
- **New third comparison table** covering those two categories.
- NY UTEN pilots and the Eversource pilot updated for Local Law 97, Local Law 154, and
  the NY All-Electric Buildings Act.

All source content is drawn from public regulatory filings. There is no proprietary,
confidential, or personally identifiable data in this repo.

## Where it should go

Inside the **CapUtility LL97 app**, replacing the existing TENS dashboard in the
**Task Force** section. The AI/integration team can decide the best placement and
routing within that app.

One layout constraint worth knowing: the page is built for **full width**. It contains
a Leaflet map and three wide comparison tables. It works best as its own full-page view
rather than as a narrow framed panel. It is responsive but will feel cramped below
roughly 900px of usable width.

## How to run it

It is a **single self-contained static HTML file**. There is no build step, no bundler,
no server-side code, no package manager, and no compilation.

Open it directly:

```
open index.html
```

Or serve it statically (any static server works):

```
python3 -m http.server 8000
# then visit http://localhost:8000
```

To deploy: copy `index.html` to wherever the Task Force section serves static assets.

## What it needs

**No environment variables. No API keys. No secrets. No database. No backend.**
All project data is embedded in the file as a JSON object in an inline `<script>` block.

### External CDN dependencies — flagged for security review

The page makes outbound requests to two third-party origins at runtime. Please review
these against the site's Content Security Policy before deploy:

| Purpose | Origin | Resource |
|---|---|---|
| Map library | `cdnjs.cloudflare.com` | `/ajax/libs/leaflet/1.9.4/leaflet.js` and `/ajax/libs/leaflet/1.9.4/leaflet.min.css` |
| Map tiles | `*.tile.openstreetmap.org` | OpenStreetMap raster tiles (`{s}.tile.openstreetmap.org/{z}/{x}/{y}.png`) |

Notes for review:

- These are the **same dependencies the currently deployed version already uses** — this
  update does not introduce a new external origin.
- Leaflet 1.9.4 is pinned to an exact version, not a floating tag.
- If the CSP forbids external CDN calls, both are straightforward to remediate:
  Leaflet can be vendored into the repo and served locally, and the tile layer URL can
  be swapped to a self-hosted or commercially licensed tile provider by changing a
  single `L.tileLayer(...)` URL string. Say the word and we'll ship a vendored variant.
- OpenStreetMap tile usage should be checked against the OSM Tile Usage Policy if
  traffic volume is expected to be significant; a commercial tile provider is the
  normal answer at production scale.
- Everything else — HTML, CSS, JavaScript, and all project data — is inline and local.
  No analytics, no trackers, no fonts loaded from third parties, no `localStorage`,
  no cookies, no network calls other than the two above.

Outbound links in the "Sources" lines of each project profile point to public documents
(coned.com, nyc.gov, dps.ny.gov, and similar). They are `target="_blank"` with
`rel="noopener"`. They are user-initiated navigation only, not runtime fetches.

## Contact

CapUtility Advisors — caputility.advisors@gmail.com
