## Dataset Access & Samples

Due to GitHub file size limitations, the full source dataset (~200MB CSV) 
is hosted on Google Drive.

### Source Dataset
🔗 Google Drive (Read-only):
https://drive.google.com/drive/folders/1MHq5zFZYwzaEyNwpy5jU5z85RWxu7HIh?usp=sharing

### Destination Location
- Store the source file Databricks Volume:
  /Volumes/sentiment_analysis/raw/social_media_volume

### How to Use
1. Upload the CSV to the above location
2. Run the Bronze ingestion notebook
3. Data will be converted to Delta Bronze tables

### Sample Data (GitHub)
To understand data expectations before running the pipeline, 
sample CSV files (5 rows each) are provided:

- `data_samples/source_sample.csv`
- `data_samples/bronze_sample.csv`
- `data_samples/silver_sample.csv`
- `data_samples/gold_sample.csv`
- `data_samples/gold_ml_core_sample.csv`

These samples reflect the exact schema and transformations
applied in each layer.

### Important Note
Do not open the Source Dataset in microsoft Excel or any other platform, it will change the date and id formats. 
Upload the CSV to the location as mentioned above.