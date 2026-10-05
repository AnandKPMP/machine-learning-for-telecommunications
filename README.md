# 📡 Machine Learning for Telecommunications

> **Context:** This repo is forked from the [AWS Solutions Library](https://github.com/aws-solutions-library-samples/machine-learning-for-telecommunications). I used it as a working reference during my tenure as Group PM at T-Mobile (2015 to 2022), where ML-driven network analytics informed capacity planning decisions at 100M+ subscriber scale.

## What This Does

An end-to-end ML framework on AWS SageMaker for telecom network data analysis. Uses IP Data Records (IPDR) as the primary data source to demonstrate:

- Network traffic pattern analysis and anomaly detection
- Churn prediction using subscriber behavioral features
- Feature engineering pipelines for time-series network telemetry
- Model training, evaluation, and deployment via SageMaker + Jupyter

## How I Applied This at T-Mobile

At T-Mobile, I led the technical program for network capacity planning for a 100M+ subscriber network. The core insight was that raw network traffic data (similar to what this framework ingests) could be combined with infrastructure efficiency metrics (Power Usage Effectiveness / PUE) to predict data center capacity requirements 2 years ahead of need.

The ML pipeline I drove in production:

1. **Ingest:** Network traffic telemetry (IPDR-class records) across towers and regional PoPs
2. **Feature engineering:** Subscriber growth curves, traffic per tower, peak-hour load patterns, seasonal adjustments
3. **Model:** Time-series forecasting (traffic demand) + regression (PUE → cooling/power overhead)
4. **Output:** 2-year capacity forecast per data center region → fed directly into capital budget planning
5. **Result:** $200M in capex savings by right-sizing data center buildout vs. prior rule-of-thumb planning

This repo's SageMaker infrastructure (IPDR feature extraction, SageMaker notebook workflows, and the ETL architecture) is structurally similar to what we built internally. I've kept it as a reference for the patterns that translate from telecom data to production ML decisions.

## Stack

- AWS SageMaker (notebook instances + training jobs)
- PySpark for large-scale ETL on IPDR datasets
- Python 3 / scikit-learn / XGBoost
- AWS CloudFormation for infrastructure deployment
- Jupyter Notebooks for exploration and model evaluation

## Running It

See the original AWS deployment guide below. You'll need an AWS account, S3 bucket, and SageMaker access.

```bash
# Deploy the CloudFormation stack
chmod +x build-s3-dist.sh
./build-s3-dist.sh $DIST_OUTPUT_BUCKET $TEMPLATE_OUTPUT_BUCKET $VERSION

aws s3 cp ./dist s3://$DIST_OUTPUT_BUCKET/machine-learning-for-all/latest \
  --recursive --acl bucket-owner-full-control
```

---

> Original solution by AWS Solutions Library. My additions: context, applied notes, and the capacity planning narrative above. All AWS license terms apply.
