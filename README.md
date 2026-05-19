# Vietnam — Rooftop Solar PV Status Dashboard

This repository contains an **interactive WebGIS dashboard** monitoring the deployment status of rooftop solar PV systems across all 63 provinces of Vietnam, based on EVN RTS monitoring data (Dec 2019 – Dec 2020).

The analysis visualizes real installation data from Vietnam Electricity (EVN), enriched with solar resource metrics (GHI, PVOUT) from the Global Solar Atlas and demographic data from the General Statistics Office of Vietnam.

🌐 **Web map: [Click here](https://jamberry129-lab.github.io/PV_Rooftop_Status)**

---

## Repository Structure

```
PV_Rooftop_Status/
├── index.html          ← WebGIS dashboard (Map + Analytics tabs)
├── data.json           ← Consolidated data (GeoJSON + timeseries + compare)
├── LICENSE
└── README.md
```

The `index.html` builds a two-tab dashboard:
- **🗺️ Map tab** — Leaflet choropleth map with 6 thematic layers, monthly filter, and province info panel
- **📊 Analytics tab** — 6 Chart.js visualizations for comparative provincial analysis

Built with [Leaflet.js](https://leafletjs.com) + [Chart.js](https://chartjs.org). Hosted on [GitHub Pages](https://pages.github.com). No backend required — all data served as static JSON.

---

## Results

| Metric | Value |
|--------|-------|
| Provinces covered | 63 / 63 |
| Total RTS installations | 561,935 systems |
| Total installed capacity | 21,716 MWp |
| Monitoring period | Dec 2019 – Dec 2020 (13 months) |
| Top province by capacity | Dak Lak |
| Top province by % HH penetration | Ninh Thuan |
| National avg GHI | 1,541 kWh/m²/yr |
| National avg W/person | 258 W |

---

## Dashboard Features

### 🗺️ Map Tab

| Layer | Description |
|-------|-------------|
| PV Capacity (monthly) | Installed capacity (MWp) — updates by selected month |
| Nr. Installations | Total number of RTS systems per province |
| % Households with PV | Proportion of households with rooftop solar |
| W per Person | PV density normalized by population |
| GHI Solar Resource | Annual solar irradiance (kWh/m²/yr) |
| kW per Household | Average system size per household |

**Interactive features:**
- Monthly filter: Dec 2019 → Dec 2020
- Click province → detailed info panel (capacity breakdown, solar resource, demographics)
- Monthly trend chart (capacity + installations) for selected province
- Top 5 provinces ranking by active layer

### 📊 Analytics Tab

| Chart | Description |
|-------|-------------|
| Total Capacity Top 20 | Horizontal bar — cumulative MWp by province |
| % Households Top 20 | Household penetration rate ranking |
| Capacity by Sector | Stacked bar — Residential / Commercial / Industrial / Admin |
| GHI vs Capacity Scatter | Solar resource vs actual deployment correlation |
| W per Person Top 20 | PV density per capita ranking |
| Monthly Trend Top 5 | Capacity growth trajectory Dec 2019 – Dec 2020 |

---

## Methodology

```
Data sources:
  EVN RTS Monitoring Reports (Dec 2019, Jan–Dec 2020)
  + Global Solar Atlas v2 (GHI, PVOUT, DNI, GTI)
  + GSO Vietnam (Population, Households by province)
  + Vietnam Province GeoJSON (63 provinces, standardized names)
        ↓
Python processing (Google Colab / pandas):
  province name normalization  → matched to standard GeoJSON names
  timeseries aggregation       → monthly capacity & installations per province
  derived indicators:
    pv_pct_hh    = qty_total / households × 100
    w_per_person = cap_total_kw / population
    kw_per_house = cap_total_kw / households
  solar zonal stats            → GHI_mean, PVOUT_mean per province
        ↓
data.json (consolidated):
  geojson    → province polygons + all attributes
  timeseries → monthly {cap_tot, qty_tot, cap_hh, qty_hh, ...} per province
  compare    → final snapshot with all indicators (63 rows)
  months     → ordered list of 13 months
        ↓
Leaflet + Chart.js (index.html) → GitHub Pages
```

---

## Data Sources

| Dataset | Source | Coverage |
|---------|--------|----------|
| RTS installation data | EVN Monitoring Reports 2019–2020 | 63 provinces, 13 months |
| GHI / PVOUT / DNI | Global Solar Atlas v2 (World Bank / Solargis) | ~1 km resolution |
| Population | General Statistics Office of Vietnam (GSO) | Province-level |
| Households | General Statistics Office of Vietnam (GSO) | Province-level |
| Province boundaries | Vietnam Province Shapefile (standardized) | 63 provinces |

---

## Parameters

| Parameter | Symbol | Value |
|-----------|--------|-------|
| Panel efficiency | η | 18% |
| Performance ratio | PR | 0.75 |
| Monitoring period | — | Dec 2019 – Dec 2020 |
| Capacity unit | — | MWp (megawatt-peak) |
| GHI unit | — | kWh/m²/yr |

---

## Practical Applications

- 🗺️ Theo dõi tình trạng triển khai điện mặt trời áp mái cấp tỉnh theo thời gian *(Monitor provincial RTS deployment status over time)*
- 📊 So sánh mức độ thâm nhập thị trường giữa các tỉnh thành *(Compare market penetration across provinces)*
- ☀️ Phân tích mối quan hệ giữa tiềm năng bức xạ và mức độ lắp đặt thực tế *(Analyze correlation between solar resource and actual deployment)*
- 🏛️ Hỗ trợ quy hoạch năng lượng tái tạo cấp quốc gia và tỉnh *(Support national and provincial renewable energy planning)*
- 🎓 Nghiên cứu học thuật về chính sách điện mặt trời tại Việt Nam *(Academic research on Vietnam solar PV policy)*
- 🌏 Framework có thể nhân rộng cho các quốc gia trong khu vực *(Replicable WebGIS framework for other countries in the region)*

---

## References

- EVN (2019–2020). *Báo cáo giám sát hệ thống điện mặt trời áp mái (RTS Monitoring Reports)*. Vietnam Electricity.
- Global Solar Atlas 2.0, Solargis / World Bank Group. https://globalsolaratlas.info
- General Statistics Office of Vietnam (GSO). *Population and Housing Census 2019*. https://www.gso.gov.vn
- OpenStreetMap contributors. Vietnam Province Boundaries.
- IRENA (2022). *Renewable Power Generation Costs in 2021*. International Renewable Energy Agency.
- Gagnon, P., Margolis, R., Melius, J., Phillips, C., & Elmore, R. (2016). *Rooftop Solar Photovoltaic Technical Potential in the United States: A Detailed Assessment*. NREL/TP-6A20-65298. [Download PDF](https://docs.nrel.gov/docs/fy16osti/65298.pdf)
- Copernicus Land Monitoring Service. *Global Land Cover 2015* (100 m). https://land.copernicus.eu

---

## License

MIT
