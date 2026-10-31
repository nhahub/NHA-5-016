# Requirements Gathering

**Project:** Shoreline Analytics: Satellite-Based Coastal Erosion & Risk Mapping in Alexandria

| Project details | Information |
|:--|:--|
| Domain | Data Engineering / Geospatial Analytics and Data products |
| Team members | Asmaa Bahaa  ·  Doha Yehia  ·  Hagar Arafa  ·  Nourhan Fathy  ·  Shahd Abdelnasser |
| Group number | ALX5_AIS5_G1 |

## Stakeholder Analysis

### Stakeholder Identification

Stakeholders are the people and organizations that use the system, influence it, or are affected by it. They are the user groups and data providers listed below.
- Coastal protection and environmental authorities (Shore Protection Authority and Ministry of Environment teams)
- Urban planners and civil engineers (municipalities and infrastructure planning teams)
- Environmental researchers and academics (geospatial analysts and oceanographers)
- GIS analysts (users of exported spatial layers in QGIS or ArcGIS)
- Satellite data providers (Copernicus / ESA, Google Earth Engine, USGS)
- General public (residents and visitors of the Alexandria coast)

### Stakeholder Needs and Expectations

| ID | Stakeholder | Role | Key Needs | Expectations |
| --- | --- | --- | --- | --- |
| SH1 | Coastal Protection and Environmental Authorities (SPA, Ministry of Environment) | Primary user, decision maker | Regular monitoring of erosion hotspots; evidence on whether hard infrastructure works are effective | Reliable, current, easy-to-read risk indicators; trustworthy data |
| SH2 | Urban Planners and Civil Engineers | Primary user | Spatial risk maps before coastal development or infill projects; risk lookup for a specific site | Fast answers by location; clear risk levels |
| SH3 | Environmental Researchers and Academics | Secondary user | Standardized open spatial data; long-term time series; transparency about data quality | Documented methodology; confidence scores; exportable data |
| SH4 | GIS Analysts | Technical user | Downloadable spatial layers; stable API | Valid GeoJSON; consistent schema |
| SH5 | Satellite Data Providers | Data source | Compliance with API usage limits and terms | Responsible, rate-limited access |
| SH6 | General Public | Indirect beneficiary | Safer and better-protected coastline | Indirect benefit through better decisions |

### Influence / Interest Matrix

Stakeholders are ranked by how much influence they have over the project and how interested they are in its outcome. This determines how closely each group is engaged.

| Level | Stakeholders | Strategy |
| --- | --- | --- |
| High influence, high interest | SH1, SH2 | Manage closely: involve in requirement reviews and validation |
| Low influence, high interest | SH3, SH4 | Keep informed: share documentation, data schema, and release updates |
| Medium influence, low interest | SH5 | Keep satisfied: respect usage terms and rate limits |
| Low influence, medium interest | SH6 | Monitor: indirect beneficiary, no direct engagement required |

### Engagement Plan
- **SH1 and SH2:** present the dashboard prototype and API examples, collect feedback on risk indicators, thresholds, and sector definitions.
- **SH3 and SH4:** document the methodology (NDWI, shoreline extraction, erosion rate formulas, confidence score) and the GeoJSON schema.
- **SH5:** Follow API quotas and cite data sources properly.

## User Stories

User stories describe the system from the user's point of view*.* Each story has acceptance criteria that define when it is complete and a priority using the MoSCoW method (Must, Should, Could).

| ID | User Story | Acceptance Criteria | Priority |
| --- | --- | --- | --- |
| US1 | As an SPA analyst, I want to select a year on a timeline slider, so that I can view historical and recent shoreline conditions (2018–2026). | The slider covers 2018–2026; changing the year updates the map and KPIs. | Must |
| US2 | As an SPA analyst, I want to see the average annual erosion rate for the selected year, so that I can track whether erosion is improving or worsening. | The KPI is shown in m/yr and updates when the year changes. | Must |
| US3 | As an SPA analyst, I want sectors color-coded by risk level, so that I can identify critical hotspots quickly. | Red, orange, and green markers are used based on documented thresholds for each sector (Corniche Infill Sector, Eastern Harbour, Montaza Bay). | Must |
| US4 | As an SPA analyst, I want to see the number of critical hotspots, so that I can prioritize protection work. | A hotspot count KPI is displayed and matches the sectors flagged as critical. | Must |
| US5 | As an urban planner, I want to submit coordinates and receive a risk level, so that I can assess a site before planning development. | The API accepts latitude and longitude and returns risk level, erosion rate, and confidence; invalid or off-coast coordinates return a clear error. | Must |
| US6 | As a researcher, I want a data confidence score for each measurement, so that I can judge how reliable it is. | A confidence score is stored and displayed per sector and year, with a documented calculation. | Should |
| US7 | As a GIS analyst, I want to download shoreline layers as GeoJSON, so that I can analyze them in QGIS or ArcGIS. | A one-click export produces a valid GeoJSON file that opens in QGIS without errors and includes geometry and attributes. | Should |
| US8 | As a data engineer, I want the pipeline to retrieve new satellite imagery automatically, so that data stays current without manual work. | The pipeline runs on a schedule, downloads imagery for the target area, and logs each run. | Must |
| US9 | As a data engineer, I want cloudy or invalid imagery to be rejected, so that bad data does not distort the metrics. | Images above a defined cloud-cover threshold are excluded and the rejection is logged. | Should |
| US10 | As a data engineer, I want processed shorelines and metrics stored in a spatial database, so that all consumers read from one consistent source. | Shoreline vectors, zonal erosion metrics, confidence scores, and time-series metadata are stored in PostGIS and queryable by year and sector. | Must |
| US11 | As a researcher, I want to view the shoreline overlay and location popups on the map, so that I can inspect specific areas. | Clicking a sector shows a popup with its erosion rate, risk level, and confidence. | Could |

## Use Cases

Use cases describe, step by step, how an actor interacts with the system to reach a goal. The main use cases are detailed below.

### Actors

| Actor | Description |
| --- | --- |
| SPA Analyst / Decision Maker | Views dashboards and risk indicators to monitor erosion |
| Urban Planner | Queries site-level risk through the dashboard or API |
| Researcher / GIS Analyst | Explores data and exports spatial layers |
| Data Engineer / Scheduler | Runs and monitors the ETL pipeline |
| Satellite Data Provider (external system) | Supplies imagery through APIs |

### Use Case Summary

| ID | Use Case | Primary Actor | Related Stories |
| --- | --- | --- | --- |
| UC1 | Run Automated ETL Pipeline | Data Engineer / Scheduler | US8, US9, US10 |
| UC2 | View Erosion Risk on Dashboard | SPA Analyst | US1, US2, US3, US4, US6, US11 |
| UC3 | Get Site Risk Level via API | Urban Planner | US5 |
| UC4 | Export Spatial Layer as GeoJSON | GIS Analyst / Researcher | US7 |

#### UC1: Run Automated ETL Pipeline
- **Primary actor:** Data Engineer / Scheduler
- **Secondary actor:** Satellite Data Provider
- **Description:** The pipeline retrieves satellite imagery, processes it into shoreline metrics, and loads the results into the data warehouse.
- **Preconditions:** API access to the imagery source is configured; the database is running; target coastal coordinates are defined.

**Main flow:**

| 01 | The scheduler (or engineer) triggers the pipeline. |
| --- | --- |
| 02 | The system requests Sentinel-2 or Landsat imagery for the target area and period. |
| 03 | The system validates the imagery and rejects images that fail quality checks (for example, excessive cloud cover). |
| 04 | The system calculates NDWI to separate water from land. |
| 05 | The system extracts the shoreline as a vector. |
| 06 | The system compares shorelines across years and computes net shoreline movement, annual erosion rate, hotspots, and a confidence score. |
| 07 | The system loads the results into PostgreSQL/PostGIS. |
| 08 | The system logs the run and its outcome. |

**Alternative and exception flows:**
  - a. The imagery API is unavailable or rate-limited: the system retries, logs the failure, and ends the run safely.
  - b. No usable imagery for the period: the system logs the gap and skips that period.
  - c. Database load fails: the system rolls back and reports the error.
- **Postconditions:** The warehouse contains up-to-date shoreline vectors and metrics with a run log.

#### UC2: View Erosion Risk on Dashboard
- **Primary actor:** SPA Analyst
- **Description:** The analyst explores erosion indicators and risk levels by year and sector.
- **Preconditions:** The ETL pipeline has loaded data into the warehouse; the dashboard is running.

**Main flow:**

| 01 | The analyst opens the dashboard. |
| --- | --- |
| 02 | The analyst selects a year using the timeline slider. |
| 03 | The system retrieves the matching data from the warehouse. |
| 04 | The system displays the map with the shoreline overlay and color-coded risk markers. |
| 05 | The system displays the KPIs: average erosion rate, critical hotspots, and data confidence. |
| 06 | The analyst selects a sector, and the system shows its details in a popup. |

**Alternative and exception flows:**
  - a. No data for the selected year: the system shows a clear "no data available" message.
  - b. The database is unreachable: the system shows an error message and no stale values.
- **Postconditions:** The analyst understands the erosion situation and risk level per sector for the chosen year.

#### UC3: Get Site Risk Level via API
- **Primary actor:** Urban Planner (or an external application)
- **Description:** A user submits coordinates and receives a risk assessment for that location.
- **Preconditions:** The API is running and the warehouse contains processed data.

**Main flow:**

| 01 | The user sends a request with latitude and longitude. |
| --- | --- |
| 02 | The system validates the coordinates. |
| 03 | The system identifies the nearest coastal sector. |
| 04 | The system retrieves the erosion rate, risk level, and confidence for that sector. |
| 05 | The system returns the result in a structured response. |

**Alternative and exception flows:**
  - a. Invalid format: the system returns an error with a clear message.
  - b. Coordinates too far from the coast or outside the study area: the system returns an out-of-range error.
- **Postconditions:** The user receives a risk assessment for the requested location.

#### UC4: Export Spatial Layer as GeoJSON
- **Primary actor:** GIS Analyst / Researcher
- **Description:** The user downloads the processed spatial layer for use in external GIS tools.
- **Preconditions:** A year is selected and processed data exists for it.

**Main flow:**

| 01 | The user selects a year in the dashboard. |
| --- | --- |
| 02 | The user clicks the download button. |
| 03 | The system generates a GeoJSON file from the stored vectors and attributes. |
| 04 | The system delivers the file to the user. |
| 05 | The user opens the file in QGIS or ArcGIS. |

**Alternative and exception flows:**
  - a. No data for the selected year: the system disables the export and shows a message.
- **Postconditions:** The user holds a valid GeoJSON file for external analysis.

## Functional Requirements

### Data Ingestion

| ID | Requirement | Related Deliverable (1-6) | Related User Story | Priority (MoSCoW) |
| --- | --- | --- | --- | --- |
| FR-01 | The system shall automatically retrieve multi-temporal Sentinel-2 scenes on a scheduled basis through an open-access Copernicus/Sentinel-2 interface for the configured Alexandria area. | 1 | US8 | Must |
| FR-02 | The system shall restrict scene search to the Alexandria bounding box [29.8, 31.1, 30.1, 31.3]. | 1 | US8 | Must |
| FR-03 | The system shall reject scenes whose cloud-cover metadata exceeds 10% and log each rejection. | 1 | US9 | Must |
| FR-04 | The system shall record each requested scene and its download outcome for ingestion-success measurement. | 1 | US8 | Must |

### Raster Processing & NDWI

| ID | Requirement | Related Deliverable (1-6) | Related User Story | Priority (MoSCoW) |
| --- | --- | --- | --- | --- |
| FR-05 | The system shall validate that each downloaded raster can be opened and contains the required spectral bands before processing. | 2 | US9 | Should |
| FR-06 | The system shall preserve source CRS and affine-transform metadata in processed raster outputs. | 2 | Gap — no direct user story | Must |
| FR-07 | The system shall calculate NDWI as (Green − NIR) / (Green + NIR) using Sentinel-2 Band 3 as Green and Band 8 as NIR. | 3 | Gap — no direct user story | Must |
| FR-08 | The system shall apply a documented thresholding rule to produce a binary water/land mask from NDWI values. | 3 | Gap — no direct user story | Must |
| FR-09 | The system shall extract shoreline vectors from the binary water/land mask for each processed observation date. | 3 | Gap — no direct user story | Must |
| FR-10 | The system shall calculate net shoreline movement between comparable shoreline observations. | 3 | Gap — no direct user story | Must |
| FR-11 | The system shall calculate annual shoreline erosion rate in metres per year for each supported coastal zone when the required observations exist. | 3 | Gap — no direct user story | Must |
| FR-12 | The system shall store a confidence score with each shoreline result and its associated observation metadata. | 3 | US6 | Must |

### Data Warehouse

| ID | Requirement | Related Deliverable (1-6) | Related User Story | Priority (MoSCoW) |
| --- | --- | --- | --- | --- |
| FR-13 | The system shall store shoreline geometry, observation date, sector, erosion metrics, confidence score, and relevant time-series metadata in PostgreSQL/PostGIS. | 4 | US10 | Must |
| FR-14 | The system shall support spatial queries against stored shoreline geometries and coastal-sector records. | 4 | US10 | Must |

### Risk Assessment & REST API

| ID | Requirement | Related Deliverable (1-6) | Related User Story | Priority (MoSCoW) |
| --- | --- | --- | --- | --- |
| FR-15 | The system shall assign each supported sector one of the project risk labels Critical, Moderate, or Stable using a documented rule. | 5 | US3; US5 | Must |
| FR-16 | The system shall expose a Flask REST API endpoint that accepts submitted coastal coordinates and returns the available risk label, erosion rate, and confidence score. | 5 | US5 | Must |
| FR-17 | The system shall validate API coordinate inputs and return a controlled client error for invalid or out-of-scope coordinates. | 5 | US5 | Must |

### Dashboard & Visualization

| ID | Requirement | Related Deliverable (1-6) | Related User Story | Priority (MoSCoW) |
| --- | --- | --- | --- | --- |
| FR-18 | The system shall provide a Streamlit dashboard integrated with Folium/Leaflet to display the selected shoreline observation on an interactive map. | 6 | US1; US3; US11 | Must |
| FR-19 | The system shall provide a timeline slider covering the years 2018–2026 and update the displayed data for the selected year where data are available. | 6 | US1 | Must |
| FR-20 | The system shall display color-coded risk information for Corniche Infill, Eastern Harbour, and Montaza Bay when records are available. | 6 | US3 | Must |
| FR-21 | The system shall display dashboard KPI cards for average erosion rate, critical hotspots, and data confidence using stored results. | 6 | US2; US4; US6 | Must |
| FR-22 | The system shall allow users to export the currently selected spatial layer as GeoJSON. | 6 | US7 | Should |
| FR-27 | The system shall show a sector popup containing the selected sector’s erosion rate, risk level, and confidence when a user selects a sector on the map. | 6 | US11 | Could |

### Monitoring & Logging

| ID | Requirement | Related Deliverable (1-6) | Related User Story | Priority (MoSCoW) |
| --- | --- | --- | --- | --- |
| FR-23 | The system shall log ingestion and processing run status, timestamps, and failure details sufficient to calculate pipeline failure rate. | 1–3 | US8; US9 | Must |
| FR-24 | The system shall log API request outcomes and response times sufficient to calculate API error rate and response-time KPIs. | 5 | Gap — no direct user story | Should |
| FR-25 | The system shall expose container health information for the database, API, and dashboard during test runs. | 4–6 | Gap — no direct user story | Should |
| FR-26 | The system shall provide setup and usage documentation for the pipeline, database schema, API, and dashboard in the project repository. | 1–6 | Gap — no direct user story | Should |

- **MoSCoW count — FR: 21 Must / 5 Should / 1 Could.**

## Non-functional Requirements

### Performance

| ID | Requirement | Measurable Target | Related KPI | Priority |
| --- | --- | --- | --- | --- |
| NFR-01 | The system shall complete scene ingestion-to-warehouse loading within the KPI-defined processing window per scene. | ≤ 5 minutes per scene | K1.3 | Must |
| NFR-11 | The system shall serve API requests within the defined response-time target under the documented test workload. | p95 ≤ 2 seconds | K3.1 | Must |
| NFR-12 | The system shall render the default Streamlit/Folium dashboard view within the defined load-time target. | ≤ 5 seconds | K3.2 | Must |
| NFR-13 | The system shall execute common PostGIS spatial queries within the defined query-time target. | ≤ 1 second | K3.3 | Must |

### Reliability

| ID | Requirement | Measurable Target | Related KPI | Priority |
| --- | --- | --- | --- | --- |
| NFR-02 | The system shall achieve the target successful scene-download rate across requested scenes. | ≥ 95% | K1.1 | Must |
| NFR-03 | The system shall keep the pipeline failure rate within the KPI target. | ≤ 5% | K1.4 | Must |
| NFR-04 | The system shall make newly released Sentinel-2 scenes available in the warehouse within the KPI freshness window when accessible and eligible. | ≤ 7 days after new scene release | K1.5 | Should |
| NFR-14 | The system shall maintain the defined container availability during the test period. | ≥ 99% uptime | K3.4 | Should |
| NFR-15 | The system shall keep server-side API errors within the KPI-defined rate, excluding invalid-input responses. | ≤ 1% of requests | K3.5 | Should |
| NFR-23 | The system shall log successful API requests during testing. | ≥ 100 successful requests during testing | K4.3 | Should |

### Data Quality

| ID | Requirement | Measurable Target | Related KPI | Priority |
| --- | --- | --- | --- | --- |
| NFR-05 | The system shall exclude every stored scene that fails the cloud-cover rule. | 100% of stored scenes ≤ 10% cloud | K1.2 | Must |
| NFR-06 | The system shall preserve source CRS and affine transform metadata in all processed raster outputs. | 100% CRS/affine preserved | K2.4 | Must |
| NFR-07 | The system shall achieve the specified shoreline positional accuracy against manually digitised reference shorelines for sample dates. | RMSE ≤ 10 m (1 pixel) | K2.1 | Must |
| NFR-08 | The system shall achieve the specified water/land mask accuracy against reference-labelled sample points. | F1-score ≥ 0.90 | K2.2 | Must |
| NFR-09 | The system shall store shoreline records with confidence scores whose average meets the KPI target. | ≥ 0.80 on a 0–1 scale | K2.3 | Must |
| NFR-10 | The system shall provide annual/seasonal shoreline observations for the expected time-series periods where eligible source imagery is available. | ≥ 90% of expected periods (2018–2026) | K2.5 | Should |
| NFR-24 | The system shall achieve the defined agreement between API risk classifications and expert/reference classifications on the validation sample. | ≥ 85% agreement with expert review | K4.5 | Should |

### Security

| ID | Requirement | Measurable Target | Related KPI | Priority |
| --- | --- | --- | --- | --- |
| NFR-16 | The system shall use environment variables for credentials and shall not commit secrets to the repository. | Verified by checklist | Verified by checklist | Must |
| NFR-17 | The system shall validate coordinate inputs and use parameterized database queries for user-supplied values. | Verified by checklist | Verified by checklist | Must |

### Usability

| ID | Requirement | Measurable Target | Related KPI | Priority |
| --- | --- | --- | --- | --- |
| NFR-18 | The system shall provide a clear dashboard flow for selecting a year, inspecting risk information, and exporting GeoJSON. | ≥ 4/5 user satisfaction at demo | K4.4 | Should |
| NFR-21 | The system shall record whether each invited target stakeholder trialled the dashboard during the project demo. | ≥ 80% of target stakeholders trial the dashboard | K4.1 | Should |
| NFR-22 | The system shall count successful GeoJSON exports during demo/testing. | ≥ 20 exports during demo/testing | K4.2 | Should |

### Scalability & Portability

| ID | Requirement | Measurable Target | Related KPI | Priority |
| --- | --- | --- | --- | --- |
| NFR-19 | The system shall support a reproducible Docker-based local setup using documented configuration without requiring an Azure deployment. | Verified by checklist | Verified by checklist | Must |

### Maintainability

| ID | Requirement | Measurable Target | Related KPI | Priority |
| --- | --- | --- | --- | --- |
| NFR-20 | The system shall use modular, documented source code and version control so pipeline, API, and dashboard components can be reviewed and maintained. | 100% documentation completeness for required repository documentation | K5.5 | Should |

- **MoSCoW count — NFR: 14 Must / 10 Should / 0 Could.**
