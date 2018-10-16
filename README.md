* Run the query on Bigquery and export to `gs://opimage/tmp/deeplearning.csv`.
```mySQL
SELECT year, month, state, is_male, child_race, weight_pounds, mother_married, cigarette_use, 
cigarettes_per_day, alcohol_use, drinks_per_week, weight_gain_pounds, father_age, father_race
FROM [bigquery-public-data:samples.natality] LIMIT 10000
```
