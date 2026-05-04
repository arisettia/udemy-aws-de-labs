# Udemy AWS Data Engineering Labs

Hands-on **labs** and **assignments** for an AWS data engineering course. Each top-level folder is a self-contained exercise: sample data, Glue/Lambda/Spark scripts, Airflow DAGs, Step Functions definitions, Docker helpers, and related AWS artifacts.

## Repository layout

| Kind | Folders |
|------|---------|
| **Labs** | `Lab1-` … `Lab10-` |
| **Assignments** | `Assignment1-` … `Assignment5-` |

There is no single root build for the whole repo—dependencies and run instructions live inside each lab or assignment where applicable.

## Labs

| # | Folder | Topics |
|---|--------|--------|
| 1 | `Lab1-Airflow-redshift-dyanmo-spotifySongs` | Airflow, Redshift, DynamoDB, Spotify-style song data |
| 2 | `Lab2-Airflow-Spark-Dynamo` | Airflow, Spark / PySpark, DynamoDB; local Glue-libs Docker helper (`local-docker-development.sh`) |
| 3 | `Lab3-ETLGluePythonShell-Stepfunctions-S3-Redshift -Rental Apartments` | Glue Python Shell, Step Functions, S3, Redshift (rental apartments) |
| 4 | `Lab4-Batch ETL-EMR-StepFunctions-S3-Datalake-RentalVehicles` | Batch ETL, EMR, Step Functions, S3 data lake (rental vehicles) |
| 5 | `Lab5-ecs-step-function-dynamodb-EcommerceOrders` | ECS, Step Functions, DynamoDB (e-commerce orders) |
| 6 | `Lab6-delta-lake-SupermarketPurchases` | Delta Lake, supermarket purchases |
| 7 | `Lab7-kinesis-lambda-dynamo-TaxiTrips` | Kinesis, Lambda, DynamoDB (taxi trips) |
| 8 | `Lab8-Pyspark-Glue-Kinesis-Mobile Network` | PySpark, Glue, Kinesis (mobile network / coverage) |
| 9 | `Lab9-CICD-GithubActions-Lambda-Glue-ECS` | CI/CD with GitHub Actions, Lambda, Glue, ECS |
| 10 | `Lab10-Kinesis-Firehose-lambda-redshift` | Kinesis Data Firehose, Lambda, Redshift |

## Assignments

| # | Folder | Topics |
|---|--------|--------|
| 1 | `Assignment1-Prepare-MySql-AuroraDB-Delta-Lake-Flight Data` | MySQL / Aurora, Delta Lake, flight data prep |
| 2 | `Assignment2-CreatingLakeHouse-DeltaTables` | Lakehouse patterns, Delta tables |
| 3 | `Assignment3-Ecommerce-Purchase-History-Lambda-Kinesis` | E-commerce purchase history, Lambda, Kinesis |
| 4 | `Assignment4-Pyspark-streaming-songs` | PySpark streaming (songs / streams) |
| 5 | `Assignment5-CI-CD-of-Lambda` | CI/CD for Lambda (includes `test_lambda.py` and workflow samples) |

## Agent / review conventions (optional)

Project-specific Cursor agent guidance: [.cursor/skills/repo-quality-gate/SKILL.md](.cursor/skills/repo-quality-gate/SKILL.md) (ground-truth reads, validation commands, test expectations, Blocker vs Nit, versioning).

## Cloning on Windows

Older copies of this course material sometimes used **paths that are invalid on Windows** (for example `|` or `:` in folder names). Git then reports:

```text
error: invalid path '...'
fatal: unable to checkout working tree
Clone succeeded, but checkout failed.
```

**This repository** uses Windows-safe directory names. If you clone a remote that still has unsafe paths, use **WSL2**, **macOS**, or **Linux**, or obtain an archive / branch with compatible paths from the maintainer.
