<div align="center">

# 🔥 FIREWATCH SA
### Where South Africa Burns

**An interactive spatial statistics and seasonal fire-intelligence dashboard for South Africa**

[![R Shiny](https://img.shields.io/badge/Built%20with-R%20Shiny-1764AB?style=for-the-badge&logo=r&logoColor=white)](https://shiny.posit.co/)
[![Spatial analysis](https://img.shields.io/badge/Spatial%20Statistics-KDE%20%7C%20NN%20%7C%20Ripley's%20K-E85D04?style=for-the-badge)](#spatial-statistics)
[![Data](https://img.shields.io/badge/Data-NASA%20FIRMS%20NOAA--21-087E8B?style=for-the-badge)](https://firms.modaps.eosdis.nasa.gov/)

### 🌍 [**Explore the live dashboard**](https://brudance.shinyapps.io/firewatch-sa-kde-map/) · 📂 [**Explore the code**](app.R)

<img src="assets/firewatch-overview.png" width="530" alt="Illustration of South African VIIRS NOAA-21 active fire detections on a national map" />

<sub>Project map illustration showing a sample of VIIRS NOAA-21 fire detections. This is not a live dashboard screenshot.</sub>

</div>

---

## ✨ Project at a glance

| 🌍 Study area | 🛰️ Satellite | 📆 Period | 🔥 Prepared detections |
|:--:|:--:|:--:|:--:|
| South Africa · 9 provinces | VIIRS NOAA-21 | 2024–2025 | **340,156** |

Wildfire and vegetation-fire activity is spatially and seasonally uneven. **FIREWATCH SA** transforms NASA FIRMS active-fire detection points into an interactive dashboard that helps users explore **where detections concentrate, when they occur, and whether their spatial arrangement departs from a simple random-pattern benchmark**.

Built as a group project for **STAT7006A — Spatial Statistics** at the University of the Witwatersrand.

> **Interpretation note:** Satellite *detections* are not necessarily unique fire events or measurements of burned area. The dashboard supports exploratory spatial analysis, not causal attribution.

## 🧭 Explore the dashboard

| Section | What you can explore |
|---|---|
| **Start Here** | Project background, research questions and dashboard navigation |
| **Overview** | National and provincial fire-detection distributions and summary indicators |
| **Seasonal Fire Intelligence** | Monthly trends, seasonal patterns and provincial comparisons for 2024–2025 |
| **Kernel Density (KDE)** | Interactive density surface over an **OpenStreetMap basemap**, with provincial boundaries and interpretation |
| **Nearest Neighbour** | Observed and expected nearest-neighbour distances, clustering ratio and Monte Carlo assessment |
| **Ripley's K** | Clustering across spatial distances, using transformed K/L statistics and simulation envelopes |
| **Methods & Limitations** | Data processing, methodological assumptions and responsible interpretation |

### 🗺️ Kernel density with a basemap

The KDE tab overlays an estimated fire-detection intensity surface on an interactive **OpenStreetMap** background. Users can pan, zoom and compare density patterns with geographic context. The downloadable static KDE figure is separate from the interactive basemap view.

### 📊 Spatial statistics

| Method | Question answered | Important qualification |
|---|---|---|
| **Kernel Density Estimation** | Where are detections spatially concentrated? | Descriptive smoothing; not a significance test |
| **Nearest-Neighbour Analysis** | Are detections closer together than expected under complete spatial randomness (CSR)? | Depends on the study window and CSR assumptions |
| **Ripley's K / L** | At which spatial distances is clustering or dispersion evident? | Pointwise simulation envelopes are not a global significance test |

**National and provincial analysis** are available. To help the hosted application remain responsive, analyses use capped samples: **KDE up to 6,000**, **Nearest Neighbour up to 2,000**, and **Ripley's K up to 800** detection points.

## 🗃️ Data and attribution

**Primary source:** [NASA FIRMS](https://firms.modaps.eosdis.nasa.gov/) — VIIRS NOAA-21 active-fire detections, 2024–2025. [Download portal](https://firms.modaps.eosdis.nasa.gov/download/).

**Basemap:** © [OpenStreetMap contributors](https://www.openstreetmap.org/copyright).

**Provincial boundaries:** Supplied in `data/provinces.rds`. The original boundary provider and version must be confirmed by the team before formal citation; no provider is assumed here.

The dashboard loads two **prepared** data files:

```text
data/
├── fires_final.rds    # Processed VIIRS fire-detection points (sf)
└── provinces.rds      # South African province polygons (sf)
```

> These `.rds` files are required to run the app. If they are not committed to the repository, request them from the project team. The original FIRMS download archive does not replace the processed files.

## 💻 Run locally

**1. Install dependencies** in the RStudio Console:

```r
install.packages(c(
  "shiny", "sf", "dplyr", "ggplot2", "leaflet", "scales",
  "spatstat.geom", "spatstat.explore", "spatstat.random", "terra"
))
```

**2.** Place `app.R` at the repository root and both `.rds` files in `data/`.

**3.** From the project folder, run:

```r
shiny::runApp(".")
```

The interactive OpenStreetMap basemap requires an internet connection. **Never add `rsconnect::deployApp()` inside `app.R`**; deployment commands belong in the RStudio Console.

## 🧪 Research integrity and limitations

- Repeated satellite detections may correspond to the same ongoing fire; detection counts are **not** fire counts or burned area.
- Satellite overpass timing, clouds, land cover and observation conditions can affect spatial and seasonal patterns.
- KDE depends on bandwidth, projection, study window and sampling.
- Nearest Neighbour and Ripley's K comparisons use a **uniform CSR null model**; apparent clustering does not establish a causal mechanism.
- Ripley's K pointwise envelopes should not be interpreted as a formal global test.
- Calendar-year seasonal groupings follow the dashboard's month-to-season definitions.

## 📁 Repository structure

```text
FIREWATCH-SA/
├── app.R                     # Seven-tab Shiny dashboard
├── README.md                 # This project showcase
├── assets/
│   └── firewatch-overview.png
├── data/
│   ├── fires_final.rds       # Add the team's prepared data
│   └── provinces.rds         # Add the team's prepared boundaries
└── docs/                     # Optional reports and presentation materials
```

## 👥 Team and submission

**University:** University of the Witwatersrand  
**Module:** STAT7006A — Spatial Statistics  
**Project:** FIREWATCH SA — Where South Africa Burns  
**Contributors:** 
### 🚀 [Launch FIREWATCH SA](https://brudance.shinyapps.io/firewatch-sa-kde-map/)

<sub>Developed for academic teaching and exploratory spatial analysis. Satellite data credit: NASA FIRMS. Basemap credit: OpenStreetMap contributors.</sub>
