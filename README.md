<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">

</head>
<body>

<h1>📊 YouTube-DataAnalysis-ETL</h1>

<h2>📌 Project Summary</h2>
<p>This project focuses on analyzing YouTube trending video data using Power BI. The pipeline involves ingesting raw data from Kaggle, processing and storing it via AWS services, and finally visualising trends and insights using interactive Power BI dashboards.</p>

<hr>

<h2>🔧 End-to-End Architecture</h2>
<table>
  <thead>
    <tr><th>Stage</th><th>Tool</th><th>Purpose</th></tr>
  </thead>
  <tbody>
    <tr><td>1. Data Ingestion</td><td>Kaggle Dataset → AWS S3 (Raw)</td><td>Collect trending videos data in CSV/JSON format</td></tr>
    <tr><td>2. Preprocessing</td><td>AWS Lambda</td><td>Initial clean-up and validation</td></tr>
    <tr><td>3. Schema Discovery</td><td>AWS Glue Crawler</td><td>Create and update the data catalog</td></tr>
    <tr><td>4. ETL Transformation</td><td>AWS Glue (PySpark)</td><td>Convert to Parquet, partition by region/date</td></tr>
    <tr><td>5. Storage</td><td>S3 (Clean/Analytics Zones)</td><td>Organized, query-optimized data lake</td></tr>
    <tr><td>6. SQL Querying</td><td>Amazon Athena</td><td>Serverless querying engine</td></tr>
    <tr><td>7. Dashboarding</td><td><strong>Power BI</strong></td><td>Interactive visual analytics</td></tr>
  </tbody>
</table>

<hr>

<h2>🧾 Dataset Description</h2>
<ul>
  <li>Source: <a href="https://www.kaggle.com/datasets/datasnaek/youtube-new" target="_blank">Kaggle's YouTube Trending Dataset</a></li>
  <li>Regions Covered: CA, US, GB, IN, etc.</li>
  <li>Key Fields: <code>video_id</code>, <code>channel_title</code>, <code>views</code>, <code>likes</code>, <code>dislikes</code>, <code>comment_count</code>, <code>category_id</code>, <code>region</code>, <code>publish_time</code></li>
</ul>

<hr>

<h2>🎨 Power BI Dashboard Features</h2>
<ul>
  <li>📈 <strong>Views over Time</strong>: Line charts showing video trends</li>
  <li>⭐ <strong>Top Channels</strong>: Ranked by views, likes, or engagement</li>
  <li>🌍 <strong>Regional Insights</strong>: Visualize popularity by country or region</li>
  <li>🧩 <strong>Filters</strong>: Region, Category, Date Range</li>
  <li>📊 <strong>KPI Cards</strong>: Total Views, Likes, Dislikes, Comments</li>
</ul>

<hr>

<h2>🔍 Visual Components in Power BI</h2>
<table>
  <thead>
    <tr><th>Visual</th><th>Data Fields</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td>Card</td><td><code>SUM(views)</code></td><td>Total Views</td></tr>
    <tr><td>Card</td><td><code>SUM(likes)</code></td><td>Total Likes</td></tr>
    <tr><td>Bar Chart</td><td><code>channel_title</code>, <code>views</code></td><td>Top Channels by Views</td></tr>
    <tr><td>Line Chart</td><td><code>trending_date</code>, <code>views</code></td><td>Daily View Trends</td></tr>
    <tr><td>Pie Chart</td><td><code>snippet_title</code></td><td>Distribution by Content Category</td></tr>
    <tr><td>Slicer</td><td><code>region</code>, <code>category_id</code>, <code>channel_title</code></td><td>Interactive Filtering</td></tr>
  </tbody>
</table>

<hr>

<h2>🧠 Data Model Notes</h2>
<ul>
  <li>Ensure <code>trending_date</code> is parsed as Date type in Power BI</li>
  <li>Use DAX measures if needed:</li>
</ul>
<pre><code>EngagementScore = ([likes] + [comment_count]) / [views]</code></pre>

<hr>

<h2>📁 Folder Structure in AWS</h2>
<pre><code>s3://youtube-data-pipeline/
├── raw/
│   └── region=ca/
├── clean/
│   └── region=ca/
├── analytics/
│   └── region=ca/</code></pre>

<hr>

<h2>✅ Getting Started</h2>
<ol>
  <li>Clone or download this repository</li>
  <li>Import cleaned <code>.csv</code> or <code>.parquet</code> data into Power BI</li>
  <li>Build visuals using the suggested fields</li>
  <li>Use slicers to filter by <code>region</code>, <code>category_id</code>, or <code>channel</code></li>
</ol>

<hr>

<h2>🚀 Sample Athena Queries</h2>
<pre><code>SELECT channel_title, SUM(views) AS total_views
FROM db_youtube_analytics.final_analytics
WHERE region = 'us'
GROUP BY channel_title
ORDER BY total_views DESC
LIMIT 10;</code></pre>

<hr>

<h2>🔒 Security & IAM</h2>
<ul>
  <li>IAM roles restricted to specific S3 actions</li>
  <li>Athena query access via policy-controlled roles</li>
</ul>

<hr>
<!-- Architecture Overview -->
<h2>⛩️ AWS Architecture Diagram</h2>
<!-- <img src="Images/Architecture.svg" alt="AWS Architecture" width="800" style="border:1px solid #ddd; padding:10px; border-radius:8px;"> -->
<img width="1280" height="720" alt="architecture" src="https://github.com/user-attachments/assets/2ac35704-3a9d-41fe-9e75-6d7ca9b37aed" />


<!-- Ingestion Layer -->
<h3>S3 Buckets</h3>
<img width="1895" height="820" alt="Screenshot 2025-07-28 145829" src="https://github.com/user-attachments/assets/f25d0838-2dda-430b-9135-2db781c34b3f" />


<!-- Processing Layer -->
<h3>🛠️Lambda Function</h3>
<img width="1908" height="778" alt="Screenshot 2025-07-28 145853" src="https://github.com/user-attachments/assets/56fc12a0-da51-4779-910c-313927779089" />


<!-- Analytics Layer -->
<h3>📊 Glue Console </h3>
<img width="1910" height="827" alt="Screenshot 2025-07-28 145931" src="https://github.com/user-attachments/assets/52deb235-e80c-4b1a-bcc3-9524ef271f08" />


<h2>🌟 Final Dashboard Example</h2>
<!-- <img src="" alt="Power BI Dashboard" width="800"> -->
<img width="1115" height="625" alt="Screenshot 2025-07-28 143625" src="https://github.com/user-attachments/assets/160143fa-ec40-46c6-b7c7-093b626536c3" />

<hr>

<h2>👨‍💻 Authors & Contributions</h2>
<ul>
  <li>AWS Glue jobs: PySpark-based transformation</li>
  <li>Athena SQL Layer: Optimized analytical queries</li>
  <li>Power BI: Dashboard and KPIs</li>
</ul>

</body>
</html>

