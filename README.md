# NovaDrop Campaign Command Center
### A Multi-Dashboard Analytics Suite for Splunk Dashboard Studio

> **From Data to Insight: The Splunk Dashboard Contest 2026**

---

## 👋 Dear Judge — Start Here

You've just joined the war room on launch day. Follow this path:

1. **`01_campaign_command_center.json`** — watch the orders roll in, toggle the maps, keep an eye on the bots
2. **`02_infrastructure_stress_and_recovery.json`** — see the incident unfold in real time
3. **`03_campaign_post_mortem.json`** — find out exactly what it cost, who caused it, and what to do next time

Three dashboards. One story. Zero excuses for the next launch.

---

## 📸 Overview

![Campaign Command Center](docs/screenshots/01_campaign_command_center.png)
*Live campaign KPIs, geo-distribution maps, and platform health leaderboard*

![Infrastructure Stress & Recovery](docs/screenshots/02_infrastructure_stress.png)
*Anomaly detection, queue saturation, and business impact during a traffic spike*

![Campaign Post-Mortem](docs/screenshots/03_post_mortem.png)
*Lost GMV integral, | predict forecast gap, and AI-generated debrief*

---

## 📁 Repository Structure

```
novadrop-campaign-command-center/
├── dashboards/
│   ├── 01_campaign_command_center.json
│   ├── 02_infrastructure_stress_and_recovery.json
│   └── 03_campaign_post_mortem.json
├── default/
│   └── savedsearches.conf          # Scheduled platform leaderboard search
├── lookups/
│   └── novadrop_campaign_summary.csv   # Per-platform KPIs for | ai ingestion
├── viz_apps/                        # Four companion visualization apps
│   ├── radar_viz.spl
│   ├── bot_attack_map.spl
│   ├── treemap_viz.spl
│   └── gantt_chart.spl
└── docs/
    ├── submission_description.docx
    └── screenshots/
```

---

## 🚀 Installation

### 1. Import the Dashboards
Open Splunk Dashboard Studio → Source Editor → paste each JSON file in order.

### 2. Install the Lookup & Saved Search
Copy `savedsearches.conf` to `$SPLUNK_HOME/etc/apps/<your_app>/default/`  
Copy `novadrop_campaign_summary.csv` to `$SPLUNK_HOME/etc/apps/<your_app>/lookups/`

### 3. Install the Companion Viz Apps
Install all four `.spl` files via:
```
splunk install app viz_apps/radar_viz.spl
splunk install app viz_apps/bot_attack_map.spl
splunk install app viz_apps/treemap_viz.spl
splunk install app viz_apps/gantt_chart.spl
```
Or upload via Splunk Web: **Apps → Manage Apps → Install app from file**

### 4. Configure | ai (Optional)
For live AI-generated campaign debrief, install the [AI Toolkit](https://splunkbase.splunk.com/app/4607) and configure an Anthropic or OpenAI connection under **AI Toolkit → Connections**.

---

## 🎨 Companion Visualization Apps

### Radar Viz
Multi-axis radar/spider chart for comparing platform health scores across dimensions.

![Radar Viz example](docs/screenshots/viz_radar.png)

---

### Bot Attack Map
Geo-heatmap showing bot traffic origin by region, intensity-coded by attack volume.

![Bot Attack Map example](docs/screenshots/viz_bot_attack.png)

---

### Treemap Viz
Proportional area treemap for visualizing revenue or order share by platform and campaign segment.

![Treemap example](docs/screenshots/viz_treemap.png)

---

### Gantt Chart
Timeline visualization for campaign phases, incident windows, and recovery milestones.

![Gantt example](docs/screenshots/viz_gantt.png)

---

## 🛠 Technical Highlights

| Feature | Detail |
|---|---|
| `ds.chain` fan-out | Single `\| predict` search feeds both area chart and trapezoidal integral KPI |
| Trapezoidal integral in SPL | `eventstats` + endpoint correction computes ~$180K lost GMV inside the pipeline |
| `ds.savedSearch` | Platform leaderboard powered by hourly scheduled search via `savedsearches.conf` |
| `\| predict` with `holdback=8` | Trains on pre-incident trend, forecasts lost opportunity window |
| `\| ai` (Anthropic) | `\| inputlookup \| stats values(*) as *` → natural-language campaign debrief |
| Token-driven visibility | Button inputs toggle geo-choropleth vs. order-flow map via condition expressions |
| Live clock | `ds.search` with `refresh: '1s'` — no custom JavaScript |
| Absolute layout | 1440px precision for NOC / war-room wall display |

---

## 📋 Requirements

- Splunk Enterprise 10.2+ or Splunk Cloud
- Splunk Dashboard Studio (included with Splunk 10.2+)
- [AI Toolkit (MLTK)](https://splunkbase.splunk.com/app/4607) — for `| predict` and `| ai` commands
- Four companion viz apps (included in this repo)

---

## 📄 License

MIT — use it, fork it, build on it. If you win a contest with it, buy us a coffee. ☕

---

*Built with Splunk Dashboard Studio · Splunk Enterprise 10.2.3 · From Data to Insight Contest 2026*
