# Project Proposal

**Project:** Shoreline Analytics: Satellite-Based Coastal Erosion & Risk Mapping in Alexandria

**Objective:**

To develop an end-to-end geospatial data engineering platform that monitors shoreline changes and assesses coastal erosion risks in selected areas of Alexandria using Sentinel-2 satellite imagery from 2018 to 2026. The project aims to extract shorelines, calculate shoreline displacement and annual erosion rates, classify erosion risk, and present the results through an interactive dashboard and REST API.

**Description:**

The project will use Sentinel-2 satellite imagery to analyze three selected coastal sectors in Alexandria: Corniche Infill, Eastern Harbour, and Montaza Bay. One suitable, low-cloud satellite image will be selected for each year from 2018 to 2026.

The team will calculate the Normalized Difference Water Index (NDWI) using the Green Band (Band 3) and Near-Infrared Band (Band 8) to distinguish water from land. The resulting water/land masks will be used to extract shoreline vectors and measure shoreline displacement over time. Based on these measurements, annual erosion rates will be calculated and used to assign coastal risk classes.

The extracted shorelines, erosion metrics, risk classifications, confidence scores, and related metadata will be stored in a PostgreSQL/PostGIS database. The results will be presented through a Streamlit and Folium dashboard, supported by a Flask REST API that provides access to risk and erosion information.

The project will be developed and tested locally using Docker Compose.

**Tools & Design:**

The project will follow a modular data engineering pipeline consisting of:

1. **Data Ingestion:** Collect Sentinel-2 imagery and filter scenes based on cloud coverage.
2. **Data Processing:** Preprocess satellite imagery and calculate NDWI to generate water/land masks.
3. **Shoreline Extraction:** Convert the extracted water boundaries into shoreline vectors.
4. **Shoreline Analysis:** Calculate shoreline displacement and annualized erosion rates for the selected sectors.
5. **Data Storage:** Load shoreline geometries, measurements, risk classes, confidence scores, and metadata into PostgreSQL/PostGIS.
6. **Data Access & Visualization:** Develop Flask API endpoints and an interactive Streamlit/Folium dashboard to display the results.

The dashboard will include a year selector, map layers, risk markers, KPI cards, information popups, and GeoJSON export functionality.

**Technologies to Use:**

- **Programming Language:** Python
- **Satellite Data:** Sentinel-2 imagery / Copernicus data
- **Geospatial Processing:** Rasterio, GeoPandas, Shapely
- **Data Processing:** NumPy
- **Database:** PostgreSQL and PostGIS
- **Backend:** Flask REST API
- **Dashboard:** Streamlit and Folium
- **Containerization:** Docker and Docker Compose
- **Version Control:** Git and GitHub
- **Data Formats:** GeoTIFF and GeoJSON

---

## Team Members & Responsibilities

1. **Asmaa Bahaa:** Sentinel-2 data ingestion, cloud filtering, shoreline-change calculations, and annual erosion-rate estimation for the selected sectors.

2. **Doha Yehia:** NDWI calculation, water/land mask generation, and shoreline vector extraction.

3. **Hagar Arafa:** PostgreSQL/PostGIS database design, shoreline data loading, and risk classification and confidence-score queries.

4. **Nourhan Fathy:** Streamlit/Folium dashboard development, including map layers, year selection, risk markers, KPI cards, and GeoJSON export.

5. **Shahd Abdelnasser:** Flask REST API development, Docker Compose setup, and automated testing.

---

## Week 1: 1–6 November — Project Setup and Initial Design

**Tasks:**

- **Asmaa Bahaa:** Prepare the class and state diagrams, organize the project plan and Gantt chart, and download an initial Sentinel-2 scene.
- **Doha Yehia:** Prepare the sequence diagram and test the NDWI calculation using a sample satellite image.
- **Hagar Arafa:** Design the ER diagram, database schema, data flow diagram, and activity diagram.
- **Nourhan Fathy:** Prepare the use case diagram, user stories, dashboard wireframes, and UI guidelines.
- **Shahd Abdelnasser:** Prepare the deployment and component diagrams and configure Docker Compose with PostGIS.
- **All team members:** Set up the GitHub repository, organize project tasks, and agree on the initial system structure.

**Deliverables:**

- Initial project documentation and design diagrams.
- GitHub repository and organized project tasks.
- Docker Compose environment with PostGIS.
- Initial Sentinel-2 sample image.
- Preliminary NDWI processing results.

## Week 2: 7–13 November — Initial End-to-End Implementation

**Tasks:**

- **Asmaa Bahaa:** Develop the Sentinel-2 ingestion script for the three sectors, including cloud filtering.
- **Doha Yehia:** Implement shoreline extraction for one selected sector and one year.
- **Hagar Arafa:** Create the PostGIS tables and load the first extracted shoreline.
- **Nourhan Fathy:** Develop the initial dashboard map and year selector using sample data.
- **Shahd Abdelnasser:** Build the Flask API structure and implement the first endpoint using sample data.
- **All team members:** Test the initial workflow and ensure that the main components can work together.

**Deliverables:**

- Initial Sentinel-2 ingestion script.
- NDWI processing and shoreline extraction for one sector and year.
- Initial PostGIS database tables with sample shoreline data.
- Preliminary dashboard interface.
- Flask API skeleton with the first endpoint and a draft test plan.

## Week 3: 14–20 November — Full Data Processing and Integration

**Tasks:**

- **Asmaa Bahaa:** Download one suitable Sentinel-2 scene per year from 2018 to 2026 for the three sectors and begin calculating shoreline displacement and erosion rates.
- **Doha Yehia:** Apply NDWI and extract shoreline vectors for all selected years and sectors.
- **Hagar Arafa:** Load the extracted shoreline data into PostGIS and develop risk classification and confidence-score queries.
- **Nourhan Fathy:** Connect the dashboard to the database and display shoreline layers and KPI information.
- **Shahd Abdelnasser:** Connect the coordinate-based risk endpoint to the database and implement unit tests.
- **All team members:** Integrate the processing, database, API, and dashboard components and resolve initial integration issues.

**Deliverables:**

- Processed Sentinel-2 data for the selected years and sectors.
- Extracted shoreline vectors for all selected years and sectors.
- PostGIS database populated with shoreline data.
- Initial erosion measurements and risk classification queries.
- Dashboard connected to the database and coordinate-based API endpoint with unit tests.

## Week 4: 21 November–4 December — System Completion, Testing, and Final Presentation

**Tasks:**

- **Asmaa Bahaa:** Complete shoreline displacement and annual erosion-rate calculations and save the results in the database.
- **Doha Yehia:** Validate extracted shorelines against the base map and adjust the NDWI/shoreline extraction process where necessary.
- **Hagar Arafa:** Complete the database structure, risk classification queries, and final data validation.
- **Nourhan Fathy:** Complete dashboard features, including risk markers and GeoJSON export, and prepare the user manual.
- **Shahd Abdelnasser:** Complete the erosion-by-sector API endpoint, integration tests, deployment documentation, and GitHub release.
- **All team members:** Complete system integration, final testing, documentation, and presentation preparation. Freeze the code by 30 November and prepare for the final presentation on 4 December.

**Deliverables:**

- Completed and integrated geospatial data engineering pipeline.
- Final shoreline measurements, annual erosion rates, and risk classifications.
- Functional dashboard and Flask REST API.
- Final database, validated results, and GeoJSON export.
- User manual, API documentation, test report, and deployment instructions.
- Final project report and presentation (4 December).