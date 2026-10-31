<div align="center">

# 🌊 Shoreline Analytics

### Satellite Based Coastal Erosion and Risk Mapping in Alexandria

![Alexandria](https://img.shields.io/badge/Study%20Area-Alexandria%2C%20Egypt-087E8B?style=for-the-badge)
![Sentinel 2](https://img.shields.io/badge/Satellite-Sentinel--2-2575A8?style=for-the-badge)
![Time series](https://img.shields.io/badge/Observation%20Years-2018%E2%80%932026-EA8A37?style=for-the-badge)
![Geospatial](https://img.shields.io/badge/Focus-Geospatial%20Analytics-6554C0?style=for-the-badge)

*Turning satellite observations into clear, inspectable evidence about shoreline change.*

</div>

---

## 🗺️ Project at a glance

| 📍 Study area | 🛰️ Imagery | 📆 Observation period | 🏖️ Coastal sectors |
|:--|:--|:--|:--|
| Alexandria, Egypt | Sentinel-2 | 2018–2026 | Corniche Infill · Eastern Harbour · Montaza Bay |

Shoreline Analytics is a geospatial data engineering project that will extract shorelines from suitable Sentinel-2 scenes, measure shoreline movement, estimate annualized erosion rates, and present the results through a map dashboard and REST API.

> **Observation note:** The current plan selects one suitable, low-cloud image for each year. Results represent the shoreline on those image dates; they do not capture every seasonal fluctuation or short-term coastal event.

## 🔄 How the platform works

```mermaid
flowchart LR
    A["🛰️ Sentinel-2 scenes"] --> B["🧹 Quality checks and preprocessing"]
    B --> C["🌊 NDWI water and land mask"]
    C --> D["📍 Shoreline vectors"]
    D --> E["📏 Displacement and annual rate"]
    E --> F[("🗄️ PostgreSQL / PostGIS")]
    F --> G["🗺️ Streamlit and Folium dashboard"]
    F --> H["🔌 Flask REST API"]
```

## 🧪 Analysis method

The project uses the Normalized Difference Water Index (NDWI) to help separate water from land in Sentinel-2 imagery:

$$
\mathrm{NDWI} = \frac{\mathrm{Green} - \mathrm{NIR}}{\mathrm{Green} + \mathrm{NIR}}
$$

For Sentinel-2, the planned inputs are **Band 3 (Green)** and **Band 8 (Near Infrared)**. The resulting water/land mask is used to extract shoreline vectors for each selected observation. Shoreline positions are then compared to estimate displacement and annualized rates, with confidence information stored alongside the results.

## ✨ Planned project features

- 🛰️ Find and filter Sentinel-2 scenes for the Alexandria study area.
- 🧮 Calculate NDWI and extract shoreline vectors for the selected sectors and years.
- 🗄️ Store shoreline geometry, dates, sector identifiers, metrics, risk labels, and confidence scores in PostgreSQL/PostGIS.
- 📊 Explore observations with a year selector, map layers, risk markers, KPI cards, and sector information popups.
- 🔌 Request risk, erosion-rate, and confidence information through a Flask API.
- 📤 Export supported spatial layers as GeoJSON.

### Technology palette

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![PostGIS](https://img.shields.io/badge/PostGIS-3D6D9A?style=flat-square)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-222222?style=flat-square&logo=flask&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

## 📅 Project Gantt chart

```mermaid
gantt
    title Shoreline Analytics Engineering Timeline 2026
    dateFormat YYYY-MM-DD
    axisFormat %b %d

    section Planning
    Proposal and scope definition          :p1_1, 2026-10-02, 2026-10-16
    Risk assessment and scope boundaries   :p1_2, 2026-10-02, 2026-10-16

    section Literature and architecture
    Remote sensing and Sentinel-2 research :p2_1, 2026-10-09, 2026-10-16
    NDWI mathematical foundations          :p2_2, 2026-10-09, 2026-10-16

    section Requirements and design
    Stakeholder and functional requirements :p3_1, 2026-10-09, 2026-10-16
    Data flow diagram mapping               :p3_2, 2026-10-09, 2026-10-16

    section Database
    Spatiotemporal schema design           :p4_1, 2026-10-09, 2026-11-06
    PostGIS container setup                 :p4_2, 2026-10-16, 2026-11-06

    section Implementation
    Sentinel-2 ingestion script             :p5_1, 2026-10-16, 2026-11-10
    Raster and NDWI processing              :p5_2, 2026-10-25, 2026-11-20
    Flask REST API                          :p5_3, 2026-11-05, 2026-11-25
    Streamlit and Folium map                :p5_4, 2026-11-10, 2026-11-30

    section QA and release
    Pipeline integration testing            :p6_1, 2026-10-16, 2026-11-30
    Confidence validation and documentation :p6_2, 2026-11-20, 2026-12-04
    Final release and presentation          :milestone, p6_3, 2026-12-04, 0d
```

## 👥 Team and work areas

| Team member | Work area |
|:--|:--|
| **Asmaa Bahaa** | Sentinel-2 ingestion, cloud filtering, shoreline change, and annual erosion rates |
| **Doha Yehia** | NDWI, water/land masks, and shoreline extraction |
| **Hagar Arafa** | PostgreSQL/PostGIS schema, data loading, risk and confidence queries |
| **Nourhan Fathy** | Streamlit/Folium dashboard, map layers, KPIs, and GeoJSON export |
| **Shahd Abdelnasser** | Flask API, Docker Compose, and automated tests |

## 🧭 Scope for the first version

**Included:** three Alexandria sectors; Sentinel-2 scenes from 2018 to 2026 where suitable imagery is available; Python geospatial processing; PostgreSQL/PostGIS; a local Docker-based setup; a dashboard and API.

**Future work:** whole-coast coverage, additional satellite sources, seasonal observations, automatic scheduling, expanded API features, and cloud deployment.

## 📄 Project documents

- [Literature Review](literature-review.md)
- [Project Planning and Management](project-planning-and-management.md)
- [Requirements Gathering](requirements-gathering.md)
## 📚 Selected references

- McFeeters, S. K. (1996). The use of the Normalized Difference Water Index (NDWI) in the delineation of open water features. *International Journal of Remote Sensing, 17*(7), 1425–1432. [https://doi.org/10.1080/01431169608948714](https://doi.org/10.1080/01431169608948714)
- Abou Samra, R. M., & Ali, R. R. (2021). Applying DSAS tool to detect coastal changes along Nile Delta, Egypt. *The Egyptian Journal of Remote Sensing and Space Science, 24*(3), 463–470. [https://doi.org/10.1016/j.ejrs.2020.11.002](https://doi.org/10.1016/j.ejrs.2020.11.002)
- Pucino, N., et al. (2022). Assessing the accuracy of Sentinel-2 instantaneous subpixel shorelines using synchronous UAV ground truth surveys. *Remote Sensing of Environment, 282*, 113293. [https://doi.org/10.1016/j.rse.2022.113293](https://doi.org/10.1016/j.rse.2022.113293)
- Vos, K., et al. (2023). Benchmarking satellite-derived shoreline mapping algorithms. *Communications Earth & Environment, 4*, 345. [https://doi.org/10.1038/s43247-023-01001-2](https://doi.org/10.1038/s43247-023-01001-2)
- Pardo-Pascual, J. E., et al. (2024). Assessment of satellite-derived shorelines automatically extracted from Sentinel-2 imagery using SAET. *Coastal Engineering, 188*, 104426. [https://doi.org/10.1016/j.coastaleng.2023.104426](https://doi.org/10.1016/j.coastaleng.2023.104426)
- El-Masry, E. A., et al. (2024). Multi-decadal coastal change detection using remote sensing: The Mediterranean coast of Egypt between El-Dabaa and Ras El-Hekma. *Environmental Monitoring and Assessment, 196*, 182. [Article](https://link.springer.com/article/10.1007/s10661-024-12359-x)

---

<div align="center">

**Shoreline Analytics** · ALX5_AIS5_G1 · Alexandria, Egypt

</div>


