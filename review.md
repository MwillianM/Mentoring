DATA ENGINEERING
===

Motivation
---

+ It's one of the most important skill for a data scientist toolkit.
+ A data scientist should carefully evaluate how his skills are aligned with the company.
+ Take larger projects.

Organization
---

+ Airflow
+ Batch data processing
+ SQL-like languages

First Job
---

+ How real life data projects actually work?
+ Raw data vs Pre-processed data
+ Instrumentation, parse data and SQL
+ Count carefully and intelligently

Hierarchy of Analytics
---

+ IA is the top of the Hierarchy based on:
  + Data literacy
  + Data collection
  + Data infraestructure
+ Hiring out-of-order problem
+ Layers of fundational work needs to be built first
+ you should hire data talents according to the order of needs

![Data Hierarchy](https://cdn-images-1.medium.com/max/800/1*2XybEH3eav63pBIu-tlRlw.png)

Data Foundation and Warehouses
---

* Ability to design, build and maintain data warehouses
+ Be not expensive
+ Be scalabe

ETL
---

### Frameworks

+ Azkaban (linkedin - hadoop)
+ Luigi (spotify - python)
+ Pinball (Pinterest - python)
* Airflow (Airbnb - python)

### Paradigms

+ JVM
+ SQL
+ Hybrid (Spark)

Recapitulation
---

1. Collect raw data
1. ETL framework
1. Data Modeling
1. Build a data warehouse
1. Apply machine learning

Data Modeling
---

+ OLTP vs OLAP
+ Normalization vs wide tables
+ Star Schema
+ Fact and Dimension tables

Backfilling Historical Data
---

+ Data storage cost is slow
+ Computation is cheap
+ Store all historical data
+ Compute metrics and dimension in the past
+ Hive dynamic partitions

Data Partitioning
---

+ Improve query performance
+ Store data into chunks
+ Datestamps as partition keys
+ Time-labeled directories
+ A partition for each ETL run (tipically daily jobs)
+ Datastamp partition facilitates data backfilling

Airflow Pipeline
---

+ ETL tasks
+ DAG
+ nodes as tasks and arrows as dependencys
+ DAG definition file
+ Operators:
  + Sensors: Extract
  + Operators: Transform
  + Transfers: Load

ETL Best Pratice
---

+ Partition data table
  + Large size tables
  + Dynamic partition
  + Parallelize backfilling
+ Load data incrementally
  + More modular and manageable
  + build dimension tables from fact tables
  + > In each run, we only need to append the new transactions to the dimension table from previous date partition instead of scanning the entire fact history.
+ Idempotency
  + Immutable tables
  + Point-in-time snapshots
  + Same query, same business logic, same time range, same result
  + Every mutation on tables generates new partitions
+ Parameterize workflow
  + Jinja + HQL
  + Incorporate backfilling on Hive SQL
+ Data checks
  + Staging tables
  + Check data quality
  + Staging-check-exchange
  + Greater than 0 checks
  + Anomaly detection
  + Unseen category
  + Outliers
  + Presto checks
+ Alerts and Monitoring System
  + Send alerts email
  + experiment imbalance
  + Model performance
  + SlackOperators
  + SLA alerts

Common Steps
---

1. Data modeling
1. Schema Design
1. Identify relevant fact
1. Identify dimension tables
1. Calculate meaningful metrics
1. Organize by dimensional cuts
1. Join tables
1. Create denormalized table
1. Backfill the historical data
1. Build dashboard/product
1. Make experimentation
1. Join experiment with fact tables
1. Aggregate user-level metrics
1. Compute test statistics
1. Calculate p-values
1. Calculate confidence intervals

From Pipeline to Frameworks
---

+ Generate ETL DAGs on the fly
+ YAML config file to build workflows dynamically
+ Auto generate user-level metrics
+ Auto calculate statistics experiment
+ Auto generate OLAP tables
+ Auto build ML engineering work

Incremental Computation Framework
---

+ Avoid scans the entire fact table
+ Summary table
+ HOCON configuration file
  + Metrics or events to pre-compute
  + Keys to group by
  + Fact table to query from
+ Airflow script builds the summary table

Backfill Framework
---

+ Specify start and end date
+ Specify parallelization and days per process
+ Airflow job automatically build
  + Parallelize the backfill tasks
  + Perform sanity checks
  + Swap stage table with production table

Global Metrics Framework
---

+ HOCON configuration file
  + Metrics
  + Dimensions
  + Keys
+ Framework identifies metrics and dimensional cuts
+ Automatically creates denormalized tables
+ Druid + Superset for visualization

Experimentation Report Framework
---

+ Fully fledged UI
  + Target and segundaries metrics
  + Type of experiment
  + Experiment buckets and its size
+ Compute metrics pipeline
+ Combinations between metrics and dimensions
+ Statistics output
  + p-value
  + Confidence interval
  + Significance
  + Minimum detectable effect
+ Metrics capping
+ Variance reduction

Used Steps
---

1. Infrastructure
1. Data Collection
1. ETLs
1. Data Warehousing
1. Reporting
1. Analytics
1. Predictive modelling

Airbnb Infra
---

1. Silver and Gold Hadoop Cluster
   + Isolation
   + Bad querys tolerance
   + Real time Replication
   + ETL jobs on gold
1. All cloud infrastructure
   + Reduce the infrastructure cost
   + Faster compute and jobs
   + cloud advantages
1. Search log table
1. Core data schema, the canonical source of truth
   + reliable
   + up-to-date
   + consistent
   + intuitive
   + acessible
   + star schema
   + facts and dimensions tables
   + date partition
   + variables with type on names
   + table metadata
   + Do not rewrite rows, write new rows instead
1. Airflow
   + hive and python
   + data curation
   + data checks
   + problems notification
   + prevents bad data
1. Knowledge repo

References
---

1. <https://medium.com/@rchang/a-beginners-guide-to-data-engineering-part-i-4227c5c457d7>
1. <https://medium.com/@rchang/a-beginners-guide-to-data-engineering-part-ii-47c4e7cbda71>
1. <https://medium.com/@rchang/a-beginners-guide-to-data-engineering-the-series-finale-2cc92ff14b0>
