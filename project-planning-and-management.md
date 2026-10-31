# Project Planning and Management

**Project:** Shoreline Analytics: Satellite-Based Coastal Erosion & Risk Mapping in Alexandria

| Project details | Information |
|:--|:--|
| Domain | Data Engineering / Geospatial Analytics and Data products |
| Team members | Asmaa Bahaa  ·  Doha Yehia  ·  Hagar Arafa  ·  Nourhan Fathy  ·  Shahd Abdelnasser |
| Group number | ALX5_AIS5_G1 |

## Project Proposal

### Project Overview & Idea
- **Project Title:** Shoreline Analytics: Satellite-Based Coastal Erosion & Risk Mapping in Alexandria.
- **Core Concept:** An end-to-end automated Data Engineering platform and Data Product designed to continuously monitor, quantify, and visualize coastal erosion, shoreline retreat, and land accretion along the coast of Alexandria, Egypt.
- **Mechanism:** Ingesting multi-temporal Earth Observation (satellite) data from Sentinel-2 APIs, automating spatial data extraction, computing shoreline metrics (such as net shoreline movement and annual erosion rates in meters per year), storing structured spatiotemporal data in a centralized Data Warehouse, and serving dynamic insights via an interactive GIS dashboard and REST APIs.

### Problem Statement

Alexandria's shoreline faces severe vulnerability due to climate-induced sea-level rise, coastal erosion, intense winter storms, and human engineering interventions. The system solves three critical limitations of traditional methods:
1. **High Cost & Low Frequency:** Manual ground surveys are labor-intensive, expensive, and sporadic.
1. **Unintegrated Data Sources:** Geospatial imagery, climate reports, and historical measurements remain fragmented across separate repositories.
1. **Lack of Automated Evidence-Based Monitoring:** Decision-makers lack timely, data-driven analytical tools to assess coastal protection works.

### Objectives
- **Automated ETL Pipeline:** Build a robust pipeline that extracts multi-temporal satellite imagery, cleans and validates spatial raster data, isolates shoreline boundaries, and calculates key indicators (Annual Erosion Rate, Critical Hotspots, Data Confidence Score) into a structured spatial database.
- **Interactive GIS Web Dashboard (Streamlit & Folium):** Provide stakeholders with a timeline slider (2018–2026), interactive Leaflet maps with color-coded risk markers across key sectors (e.g., Corniche Infill, Eastern Harbour, Montaza Bay), real-time KPI metrics, and one-click GeoJSON spatial data export.
- **Risk Assessment & API Serving Layer:** Deploy extensible REST API endpoints (Flask) to serve risk-level assessments and quantitative erosion data based on user-submitted coastal coordinates.

### Scope of Work

• **In-Scope: **
- Automated data ingestion from Sentinel-2 APIs targeting Alexandria coastal coordinates.
- Geospatial processing using Python libraries (GeoPandas, Rasterio, Shapely, NumPy) for NDWI calculation and shoreline vector extraction.
- Spatiotemporal Data Warehouse storage (PostgreSQL/PostGIS or SQL Server via Docker).
- Frontend interactive visualization using Streamlit and Folium

## Project Plan

### Project Timeline (Gantt Chart Code for Github)

gantt

title Shoreline Analytics - Detailed Engineering Timeline (DEPI 2026)     dateFormat  YYYY-MM-DD     axisFormat  %b %d

section Phase 1: Project Planning

Project Proposal & Scope Definition    :active, p1_1, 2026-10-02, 2026-10-16     Risk Assessment & Scope Boundaries     :active, p1_2, 2026-10-02, 2026-10-16     section Phase 2: Literature & Arch.

Remote Sensing & Sentinel-2 Research   :p2_1, 2026-10-09, 2026-10-16     NDWI Mathematical Foundations          :p2_2, 2026-10-09, 2026-10-16     section Phase 3: Requirements & Design

Stakeholder & Functional Requirements  :p3_1, 2026-10-09, 2026-10-16     Data Flow Diagrams (DFD) Mapping       :p3_2, 2026-10-09, 2026-10-16     section Phase 4: Database Schema

Spatiotemporal DWH Schema Design       :p4_1, 2026-10-09, 2026-11-06     PostGIS / SQL Server Container Setup   :p4_2, 2026-10-16, 2026-11-06     section Phase 5: Implementation

ETL Ingestion Script (STAC API)        :p5_1, 2026-10-16, 2026-11-10

Raster & NDWI Processing Engine        :p5_2, 2026-10-25, 2026-11-20

REST API Serving Layer (Flask)         :p5_3, 2026-11-05, 2026-11-25     Streamlit & Folium Interactive Map     :p5_4, 2026-11-10, 2026-11-30     section Phase 6: QA & Deployment

Pipeline Integration Testing           :p6_1, 2026-10-16, 2026-11-30

Confidence Validation & Documentation  :p6_2, 2026-11-20, 2026-12-04

Final Release & Project Presentation   :milestone, p6_3, 2026-12-04, 2026-12-04

### Project Milestones

| Phase | Workstream | Dates | Milestone |
| --- | --- | --- | --- |
| Phase 1 | Project Planning & Scope Definition | Oct 02, 2026 – Oct 16, 2026 | Finalizing project charter, problem statement formulation, scope boundaries, and risk assessment strategies. |
| Phase 2 | Literature Review & Technical Architecture | Oct 09, 2026 – Oct 16, 2026 | Documenting remote sensing methodologies, NDWI mathematical formulations, and ETL pipeline architecture. |
| Phase 3 | Requirements Gathering & System Design | Oct 09, 2026 – Oct 16, 2026 | Defining functional/non-functional requirements for stakeholders (SPA, Ministry of Environment) and mapping Data Flow Diagrams (DFD). |
| Phase 4 | Spatiotemporal Database & Schema Design | Oct 09, 2026 – Nov 06, 2026 | Designing the Data Warehouse schema (PostgreSQL/PostGIS) for shoreline vectors and zonal metrics. |
| Phase 5 | Pipeline Implementation & Dashboard Development | Oct 16, 2026 – Nov 30, 2026 | Building the automated ETL ingestion script, raster processing algorithms, Flask REST API endpoints, and the Streamlit/Folium interactive web map. |
| Phase 6 | Testing, Validation & Final Deployment | Oct 16, 2026 – Dec 04, 2026 | Rigorous pipeline integration testing, data confidence score validation, and final project documentation release. |

### Project Deliverables
1. **ETL Ingestion Module: **
  1. Automated Python script (fetch_satellite_data.py) connected to Copernicus / Sentinel-2 Open Access APIs to retrieve multi-spectral satellite imagery over targeted coastal coordinates.
  1. Automated spatial filtering for the Alexandria bounding box ([29.8, 31.1, 30.1,

31.3]) and strict cloud-cover criteria.
1. **Raster Processing & Transformation Pipeline: **
  1. Spatial data processing modules using Rasterio, GeoPandas, and Shapely to handle GeoTIFF raster data structures while preserving Coordinate Reference Systems (CRS) and Affine Transformation metadata.
1. **Algorithm & NDWI Computation Engine: **
  1. Programmatic script executing the Normalized Difference Water Index (NDWI) calculation based on Green (Band 3) and Near-Infrared (Band 8) bands:
  1. Thresholding logic to generate binary water/land separation masks and extract historical shoreline vectors.
1. **Spatiotemporal Data Warehouse & Database Schema: **
  1. A centralized, structured database (PostgreSQL/PostGIS or SQL Server via Docker container) designed to store processed shoreline vectors, zonal erosion metrics ($m/yr$), confidence scores, and time-series metadata.
1. **REST API Serving Layer: **
  1. Extensible REST API endpoints (built with Flask) capable of serving risk level assessments and quantitative coastal erosion data based on user-submitted coordinates.
1. **Interactive GIS Web Dashboard (Data Product): **
  1. A fully functional, containerized Streamlit web application integrated with Folium/Leaflet maps.
  1. Features a timeline slider (2018–2026), color-coded risk markers across key sectors (e.g., Corniche Infill Sector, Eastern Harbour, Montaza Bay), real-time KPI metric cards, and oneclick GeoJSON spatial data export.

### Resource Allocation
- **Data Resources:** Open-access multi-temporal satellite imagery acquired via Sentinel-2 and Copernicus APIs targeting the Alexandria BBOX.
- **Software & Processing Stack:** Python programming environment, geospatial raster libraries

(Rasterio, GeoPandas, NumPy), and version control via GitHub.
- **Storage & Serving Infrastructure:** Spatiotemporal Data Warehouse (PostgreSQL/PostGIS or SQL Server via Docker containers) combined with Flask for REST APIs and Streamlit/Folium for the web visualization layer.

## Task Assignment & Roles

Each of the five members owns one technical part and a fixed set of documents, so everyone carries a similar load, and a second member reviews every part. We build a smaller version of the platform first and treat everything else as future work.

### Scope We Commit To

| Area | We will deliver | Future work (not committed) |
| --- | --- | --- |
| Satellite data | Sentinel-2 imagery only | Landsat and other sources |
| Study area | Three sectors: Corniche Infill, Eastern Harbour, Montaza Bay | The whole Alexandria coast |
| Time coverage | One clear scene per year, 2018–2026 | Seasonal or monthly shorelines |
| Pipeline | Python scripts run in order with one command | Automatic scheduling |
| Database | PostgreSQL/PostGIS in Docker | SQL Server |
| Dashboard | One map with year slider, risk markers, KPI cards and GeoJSON export | Dual-map comparison |
| API | Flask with two endpoints: risk by coordinates and erosion by sector | Authentication and more endpoints |
| Deployment | Docker Compose on a local machine | Azure deployment |

### Team Roles and Responsibilities

Each member has one main technical task and three or four documents. Each member's work is reviewed by one other member, who also acts as backup for that part.

| Team member | Main technical task | Documents owned |
| --- | --- | --- |
| Asmaa Bahaa | Data ingestion: script that downloads and filters Sentinel-2 scenes. Erosion rate per sector (shoreline change 2018–2026 in m/yr) | Project plan and Gantt chart, class diagram, state diagram, final presentation |
| Doha Yehia | NDWI calculation, water/land mask and shoreline extraction (one shoreline line per sector and year) | Literature review, NDWI algorithm description, sequence diagram, README |
| Hagar Arafa | PostGIS database: tables, loading shorelines, risk class and confidence score queries | ER diagram, logical and physical schema, data flow diagram, activity diagram |
| Nourhan Fathy | Streamlit/Folium dashboard: map, year slider, risk markers, KPI cards, GeoJSON export | Requirements and user stories, use case diagram, wireframes and UI guidelines, user manual |
| Shahd Abdelnasser | Flask API (two endpoints), Docker Compose setup, automated tests | Test plan and bug reports, API documentation, deployment and component diagrams |

### Shared Responsibilities
- Everyone attends the weekly meeting and writes the technical documentation for their own component.
- Every pull request is reviewed by the member in the last column above before it is merged.
- Everyone presents their own component in the final presentation.

### Task Breakdown and Timeline

The documents due on 16 October (proposal, plan, literature review, requirements) are covered by their own sections and files. The weekly plan below starts on 1 November. System design documents are due on 6 November, the code freeze is on 30 November and the final submission is on 4 December 2026.

| Week | Goal | Asmaa | Doha | Hagar | Nourhan | Shahd |
| --- | --- | --- | --- | --- | --- | --- |
| 1: 1–6 Nov | Design documents submitted; repo and Docker ready | Class and state diagrams; GitHub repo and issues; download one scene | Sequence diagram; run NDWI on that scene | ER diagram, schema, DFD, activity diagram | Use case diagram, wireframes, UI guidelines | Deployment and component diagrams; Docker Compose with PostGIS |
| 2: 7–13 Nov | One sector works end to end for one year | Ingestion script for the three sectors with cloud filter | Shoreline extraction for one sector, one year | Create tables; load the first shoreline | Dashboard with map and year slider on sample data | API skeleton with first endpoint on sample data; draft test plan |
| 3: 14–20 Nov | All years and sectors processed and loaded | Download one scene per year, 2018–2026; start erosion rates | Shoreline extraction for all years and sectors | Load all shorelines; risk class and confidence score queries | Connect dashboard to the database; shoreline layer per year; KPI cards | Risk-by-coordinates endpoint reading from the database; unit tests |
| 4: 21–27 Nov | Full system runs with one Docker Compose command | Finish erosion rates for all sectors and save them to the database | Check shorelines against the base map; adjust thresholds; algorithm document | Check risk classes; finish schema document | Risk markers, GeoJSON export, draft user manual | Erosion-by-sector endpoint; integration tests; README setup steps |
| 5: 28 Nov–4 Dec | Code freeze on 30 Nov; final testing; presentation on 4 Dec | Final presentation and report assembly | Final check of shoreline results; slides on the method | Final check of database and risk results; slides on the data model | Final user manual; slides on the dashboard | Final test report and bug list; GitHub release; slides on API and deployment |

### Communication and Working Rules
- One short weekly meeting, plus a written update from each member in the middle of the week.
- Tasks are tracked as GitHub Issues; code goes through feature branches and pull requests.
- A member who is more than two days behind tells the team straight away, so the work can be shared early instead of discovered at the deadline.

## Risk Assessment & Mitigation Plan

The three biggest risks are poor satellite data, an inaccurate shoreline and a slipping schedule. Likelihood and impact are rated Low, Medium or High, the most serious risks come first, and each member owns two risks.

### Risk Register

| ID | Risk | Likelihood | Impact | What we do about it | Owner |
| --- | --- | --- | --- | --- | --- |
| R1 | Satellite scenes are too cloudy, or downloads fail or are slow | High | High | Pick the clearest scene per year (one per year is enough); apply the 10% cloud filter; download all scenes in the first two weeks and store them locally; note backup dates for each year | Asmaa |
| R2 | The shoreline taken from 10 m pixels is inaccurate (waves, tides, threshold choice) | High | High | Test the NDWI threshold on one sector first; use the same season every year; check results visually on the base map; present values as estimates with a confidence score | Doha |
| R3 | The schedule slips because of other courses or a member being unavailable | High | High | Weekly goals with clear owners; the reviewer can take over a part; follow the fallback plan in 4.2; keep the last week free for testing and the presentation | Asmaa |
| R4 | Parts do not fit together (different file formats, coordinate systems or column names) | Medium | High | Agree formats, coordinate system and column names in week 1; run one sector end to end in week 2; run everything with Docker Compose | Shahd |
| R5 | No survey data is available to check the erosion results | Medium | High | Digitise a reference shoreline by hand for one sector and compare it; compare trends with published studies on Alexandria; state the limits clearly | Hagar |
| R6 | Raster processing is too slow or uses too much memory on our laptops | Medium | Medium | Clip each scene to the three sectors right after download; process one year at a time; store only shoreline lines in the database, not rasters | Doha |
| R7 | The database design changes late and breaks loading, the API or the dashboard | Medium | Medium | Freeze the schema after the 6 Nov design submission; later changes only by team agreement and announced to everyone | Hagar |
| R8 | Setups differ between laptops (GDAL, PostGIS, Python versions) | Medium | Medium | Use Docker Compose for everything; pin library versions; test the README setup steps on a second machine | Shahd |
| R9 | Risk labels on the dashboard mislead users, for example "critical" for an uncertain result | Medium | Medium | Document the rule for each risk level; show the confidence score next to every label; add a note on limits in the dashboard and user manual | Nourhan |
| R10 | Documentation falls behind the code | Medium | Medium | Each member writes their section in the same week they finish the part; the reviewer checks the document together with the code | Nourhan |

### Fallback Plan If We Fall Behind

If a weekly goal is missed, the team decides at the next meeting which of these to cut, in this order:
1. Drop the second API endpoint and keep only risk by coordinates.
1. Drop the GeoJSON export button.
1. Use every second year (2018, 2020, 2022, 2024, 2026) instead of every year.
1. Reduce the study area from three sectors to two.

We do not cut the ingestion script, shoreline extraction, the database, the dashboard map or the required documents.

### Risk Monitoring
- The risk register is reviewed at the weekly meeting, and likelihood and impact are updated.
- R1, R2 and R3 are checked every week.
- Any new risk is added with an owner and an action.

## Key Performance Indicators (KPIs)

### Purpose

This document defines the Key Performance Indicators used to measure the success of the Shoreline Analytics project. The project is an end-to-end Data Engineering platform that ingests Sentinel-2 satellite imagery of the Alexandria coast, computes NDWI to extract shorelines, stores spatiotemporal results in a PostgreSQL/PostGIS data warehouse, and serves erosion insights through a Flask REST API and a Streamlit/Folium dashboard.

The KPIs below turn the project objectives into measurable targets, so the team and stakeholders can objectively judge whether the pipeline, the data, the system and the final data product meet expectations.

### KPI Framework Overview

The KPIs are grouped into five categories that map directly to the project objectives and deliverables:

| KPI Category | # KPIs | Key Examples |
| --- | --- | --- |
| Data Pipeline Performance | 5 | Ingestion success, processing time, freshness |
| Data Quality & Accuracy | 5 | Shoreline RMSE, NDWI F1-score, confidence score |
| System Performance & Reliability | 5 | API response time, uptime, query time |
| User Adoption & Value | 5 | Stakeholder adoption, exports, satisfaction |
| Project Delivery & Management | 5 | On-time milestones, deliverables, tests |

Note: the targets are proposed baselines based on the project scope and typical standards for geospatial data pipelines. They can be adjusted by the team after the first testing cycle.

### Detailed KPIs

#### Data Pipeline Performance

Measures how reliably and quickly the automated ETL pipeline (Deliverables 1–3) turns satellite imagery into shoreline data.

| ID | KPI | Target | How It Is Measured | Frequency |
| --- | --- | --- | --- | --- |
| K1.1 | Ingestion Success Rate | ≥ 95% | Successful Sentinel-2 scene downloads ÷ total requested scenes (logged by fetch_satellite_data.py) | Per run |
| K1.2 | Cloud-Cover Filter Compliance | 100% of stored scenes ≤ 10% cloud | Check cloud-cover metadata of every scene accepted into the pipeline | Per run |
| K1.3 | ETL Processing Time per Scene | ≤ 5 minutes | Timestamp difference between scene download start and shoreline vector load into the DWH | Per run |
| K1.4 | Pipeline Failure Rate | ≤ 5% | Failed ETL runs ÷ total ETL runs (from pipeline logs) | Weekly |
| K1.5 | Data Freshness | ≤ 7 days after new scene release | Gap between Sentinel-2 acquisition date and availability in the warehouse | Weekly |

#### Data Quality & Accuracy

Measures whether the extracted shorelines and erosion metrics are trustworthy enough for evidence-based decisions.

| ID | KPI | Target | How It Is Measured | Frequency |
| --- | --- | --- | --- | --- |
| K2.1 | Shoreline Positional Accuracy | RMSE ≤ 10 m (1 pixel) | Compare extracted shoreline against a manually digitised reference shoreline for sample dates | Per release |
| K2.2 | Water/Land Mask Accuracy | F1-score ≥ 0.90 | Confusion matrix of the NDWI binary mask against reference labelled sample points | Per release |
| K2.3 | Average Data Confidence Score | ≥ 0.80 (scale 0–1) | Mean confidence score stored per shoreline record in the DWH | Monthly |
| K2.4 | Spatial Metadata Integrity | 100% CRS/affine preserved | Automated check that CRS and affine transform of outputs match the source GeoTIFF | Per run |
| K2.5 | Time-Series Completeness | ≥ 90% of expected periods (2018–2026) | Available annual/seasonal shorelines ÷ expected shorelines per sector | Monthly |

#### System Performance & Reliability

Measures the response time and availability of the database, REST API and dashboard (Deliverables 4–6).

| ID | KPI | Target | How It Is Measured | Frequency |
| --- | --- | --- | --- | --- |
| K3.1 | API Response Time | p95 ≤ 2 seconds | Measure Flask endpoint latency on test requests (e.g., Postman / Locust) | Weekly |
| K3.2 | Dashboard Load Time | ≤ 5 seconds | Time to render the Streamlit/Folium map with default timeline year | Per release |
| K3.3 | Database Query Time | ≤ 1 second | Execution time of common PostGIS spatial queries (EXPLAIN ANALYZE) | Weekly |
| K3.4 | System Uptime | ≥ 99% | Container health-check logs (API, DB, dashboard) over the testing period | Weekly |
| K3.5 | API Error Rate | ≤ 1% of requests | HTTP 4xx/5xx responses ÷ total requests (excluding invalid input) | Weekly |

#### User Adoption & Value

Measures whether stakeholders such as the Shore Protection Authority and the Ministry of Environment actually use the product and find it useful.

| ID | KPI | Target | How It Is Measured | Frequency |
| --- | --- | --- | --- | --- |
| K4.1 | Stakeholder Adoption | ≥ 80% of target stakeholders trial the dashboard | Count of stakeholders (e.g., SPA, Ministry of Environment) who accessed the demo ÷ invited | End of project |
| K4.2 | GeoJSON Export Usage | ≥ 20 exports during demo/testing | Counter logged on the one-click export button | Weekly |
| K4.3 | API Usage | ≥ 100 successful requests during testing | Flask request logs | Weekly |
| K4.4 | User Satisfaction | ≥ 4 / 5 | Short feedback form after the demo (usability, clarity of risk levels) | End of project |
| K4.5 | Risk Assessment Reliability | ≥ 85% agreement with expert review | Compare API risk levels with expert/reference classification on sample coordinates | Per release |

#### Project Delivery & Management

Measures whether the team delivers the project on time and with the agreed quality, based on the Gantt chart (Oct 02 – Dec 04, 2026).

| ID | KPI | Target | How It Is Measured | Frequency |
| --- | --- | --- | --- | --- |
| K5.1 | Milestone On-Time Completion | ≥ 90% | Milestones finished by planned date ÷ total milestones (per the Gantt chart) | Weekly |
| K5.2 | Deliverable Completion | 6 / 6 delivered | Checklist of the six project deliverables | End of each phase |
| K5.3 | Test Pass Rate | ≥ 90% | Passed integration tests ÷ total tests | Per sprint |
| K5.4 | Open Critical Defects at Release | 0 | Count of unresolved critical issues in GitHub Issues | Per release |
| K5.5 | Documentation Completeness | 100% | README, architecture, DFD, schema and user guide all available in the repository | End of project |

### KPI Mapping to Project Objectives
- **Objective 1:** Automated ETL pipeline → K1.1 to K1.5 and K2.4.
- **Objective 2:** Interactive GIS dashboard → K3.2, K4.1, K4.2, K4.4.
- **Objective 3:** Risk assessment and API serving layer → K3.1, K3.5, K4.3, K4.5.
- **Data trust:** Reliable and accurate erosion data → K2.1, K2.2, K2.3, K2.5.
- **Project success:** On-time and complete delivery → K5.1 to K5.5.

### Measurement & Reporting Plan
- **Data sources:** Pipeline logs, API logs and Docker health checks provide automatic measurements for most technical KPIs.
- **Stakeholder feedback:** A short demo session and feedback form collect adoption and satisfaction data from stakeholders.
- **Review cycle:** The team reviews KPI values weekly during implementation (Phase 5) and at each release during testing (Phase 6).
- **Corrective action:** Any KPI below target triggers an action item that is added to the risk register and assigned to a team member.

### Success Criteria

The project is considered successful when:
- All six deliverables are completed and presented by the final release on Dec 04, 2026.
- At least 80% of the KPIs reach their targets, including every data accuracy KPI in category 3.2.
- The system runs stably with uptime of at least 99% and API response time within 2 seconds during testing.
- Stakeholders confirm that the dashboard and API support their coastal monitoring decisions.
