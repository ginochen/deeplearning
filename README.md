* Run the query on Bigquery and export to `gs://opimage/tmp/deeplearning.csv`.
```mySQL
SELECT year, month, state, is_male, child_race, weight_pounds, mother_married, cigarette_use, 
cigarettes_per_day, alcohol_use, drinks_per_week, weight_gain_pounds, father_age, father_race
FROM [bigquery-public-data:samples.natality] LIMIT 10000
```
* Use PySpark to configure and import the data:
```python
sc = SparkContext()
spark = SparkSession(sc)
bucket = spark._jsc.hadoopConfiguration().get("fs.gs.system.bucket")
project = spark._jsc.hadoopConfiguration().get("fs.gs.project.id")
todays_date = datetime.strftime(datetime.today(), "%Y-%m-%d-%H-%M-%S")
input_directory = "gs://{}/tmp/open_images-{}".format(bucket, todays_date)
conf = {
    "mapred.bq.project.id": project,
    "mapred.bq.gcs.bucket": bucket,
    "mapred.bq.temp.gcs.path": input_directory,
    "mapred.bq.input.project.id": project,
    "mapred.bq.input.dataset.id": "open_images_yolov3",
    "mapred.bq.input.table.id": "open_images_annotation",
    }
```
