# Shoreline Analytics

A colorful project overview for **Shoreline Analytics: Satellite-Based Coastal Erosion & Risk Mapping in Alexandria**. The page summarizes the supplied literature review, project plan, and requirements gathering document.

## View the colorful page

After adding `index.html` to this repository, open **Settings → Pages**. Under **Build and deployment**, select **Deploy from a branch**, choose `main` and `/(root)`, then save. GitHub will show a Pages link here after deployment finishes.

## Project Gantt chart

This is Mermaid Gantt syntax. Keep the opening and closing `mermaid` fences; GitHub renders the chart in Markdown preview and on the README page.

```mermaid
gantt
    title Shoreline Analytics — Engineering Timeline (DEPI 2026)
    dateFormat YYYY-MM-DD
    axisFormat %b %d

    section Project planning
    Proposal and scope definition       :active, p1_1, 2026-10-02, 2026-10-16
    Risk assessment and scope boundaries :active, p1_2, 2026-10-02, 2026-10-16

    section Literature and architecture
    Remote sensing and Sentinel-2 research :p2_1, 2026-10-09, 2026-10-16
    NDWI mathematical foundations          :p2_2, 2026-10-09, 2026-10-16

    section Requirements and design
    Stakeholder and functional requirements :p3_1, 2026-10-09, 2026-10-16
    Data flow diagram mapping               :p3_2, 2026-10-09, 2026-10-16

    section Database schema
    Spatiotemporal warehouse schema design :p4_1, 2026-10-09, 2026-11-06
    PostGIS container setup                 :p4_2, 2026-10-16, 2026-11-06

    section Implementation
    ETL ingestion script (STAC API)         :p5_1, 2026-10-16, 2026-11-10
    Raster and NDWI processing engine       :p5_2, 2026-10-25, 2026-11-20
    REST API serving layer (Flask)          :p5_3, 2026-11-05, 2026-11-25
    Streamlit and Folium interactive map    :p5_4, 2026-11-10, 2026-11-30

    section QA and deployment
    Pipeline integration testing            :p6_1, 2026-10-16, 2026-11-30
    Confidence validation and documentation :p6_2, 2026-11-20, 2026-12-04
    Final release and presentation          :milestone, p6_3, 2026-12-04, 0d
```

## Add or edit the Gantt code in GitHub

1. Open the repository and choose **Add file → Create new file**.
2. Name it `README.md` (or `PROJECT_PLAN.md` if a README already exists).
3. Paste the chart above. GitHub renders it when it is inside a fenced block that starts with `mermaid`.
4. Scroll down, enter a commit message, and select **Commit changes**.

To update the schedule later, edit a task's label, start date, or duration in its line. Dates use `YYYY-MM-DD`.
