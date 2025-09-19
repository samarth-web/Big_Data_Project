#  Spotify Big Data Analysis with PySpark, Hive & Hadoop

The aim of this project is to demonstrate how Apache Spark and Hive can be used for large-scale data processing. For this example, the pipeline runs on Google Colab (https://colab.research.google.com/drive/11FbZr4hCwC9ci2t-AFewpSVyMKkorxod?usp=sharing), but in production, it would scale across Hadoop clusters (HDFS + YARN).

This project explores Spotify’s track dataset (~1140k rows) https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset?resource=download using **Apache Spark**.  
I built an end-to-end pipeline that combines **Big Data processing (Spark SQL, Hive, Hadoop (theoretical), Parquet)** with **Machine Learning (RandomForest)** to complete exploratory data analysis, analyse audio features and predict track genres.  

The work demonstrates how local Spark jobs in Colab can scale seamlessly to **Hadoop (HDFS/YARN)** or cloud platforms like **AWS EMR** or **Databricks**.

##  Exploratory Data Analysis (EDA)
After cleaning and casting numeric features, I ran Spark SQL queries to explore trends in the dataset:

- **Danceability:** Chicago-house & kids were the most danceable.
- **Energy:** Death metal and Grindcore are the most energetic genres
- **Correlation:** Loudness and energy showed a correlation (r ≈ 0.007).  
- I completed  data visualisation using matplotlib.pyplot

 **Note on Loudness values:**  
The Spotify dataset reports loudness in **dBFS/LUFS (decibels relative to full scale)**.  
- 0 dB = the maximum possible loudness in digital audio.  
- Real tracks are always **below 0**, so values are negative (e.g., -30 dB = quiet, -6 dB = loud).  
- This is different from **dB SPL** (e.g., ~60 dB SPL = normal conversation) which measures real-world sound pressure.

---

## Machine Learning

### Multi-Class Classification (125 genres)
- Model: RandomForest (200 trees, max depth 12)  
- **Accuracy:** ~18%  
- **F1 Score:** ~13%  
- Above random baseline (~1%), but shows the challenge of fine-grained genre prediction.

### Binary Classification (Pop vs Not-Pop, balanced dataset)
- Balanced dataset: 1000 *pop* vs 1000 *not-pop* tracks  
- **Accuracy:** ~89%  
- **F1 Score:** ~89%  


---

## Scalability Note
- **Local (Colab):** SparkSession with Hive-style Parquet tables.  
- **Production (Hadoop):** Same tables stored in **HDFS**, Spark jobs executed across nodes with **YARN**.  
- **Cloud:** Equivalent on **AWS EMR / Databricks** with S3 in place of HDFS.  

This pipeline demonstrates how an experiment on a laptop can scale to real-world big-data clusters.

---
