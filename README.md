# Loan Data Pipeline Project

## Overview

The dataset contains loan-related details and specifications.

The Databricks project is organized into three layers: Bronze, Silver, and Gold. Each layer builds upon the output of the previous layer.

### Bronze Layer

The Bronze layer ingests the source data and performs initial validation checks, such as verifying column availability and validating data against required conditions. The output of this stage is the Bronze table.

### Silver Layer

The Bronze table is used as the input for the Silver layer. Additional data quality validations and transformations are performed to refine the data. The output of this stage is the Silver table.

### Gold Layer

The Silver table is used in the Gold layer to generate business insights and answer business-related questions. This layer contains the final reporting and analytical outputs.

## Databricks Workflow

The workflow is configured with task dependencies:

Bronze → Silver → Gold

Each layer starts only after the successful completion of the previous layer. If a layer fails, downstream tasks do not execute.

## GitHub Integration

The Databricks project is connected to GitHub for version control and CI/CD automation.

The following GitHub Secrets were configured:

* DATABRICKS_HOST: Obtained from the Databricks workspace URL.
* DATABRICKS_TOKEN: Generated from User Settings → Developer → Access Tokens.
* DATABRICKS_JOB_ID: Obtained from the Databricks Workflow Job.

## GitHub Actions

A GitHub Actions workflow is configured using a YAML file.

The workflow:

1. Validates the presence of required notebooks.
2. Triggers the Databricks workflow.
3. Executes the Bronze → Silver → Gold pipeline through the configured Databricks job.

## Data Validation

Validation checks are implemented within the Databricks pipeline to ensure data quality. If a validation fails, the corresponding task fails and the workflow stops execution.
