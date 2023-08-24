
How to setup Buildkite with dbt Cloud CI
- Add ci python code to repository
- Add dbt Labs API key to Secret manager
- Point BuildKite at dbtLabs Repo
- Only Run Builds on Pull Requests
- Updates Buildkite YAML steps to below
```
env:
  DBT_CLOUD_API_TOKEN: "${DBT_CLOUD_API_TOKEN}"
  DBT_CLOUD_ACCOUNT_ID: "20"
  DBT_CLOUD_PROJECT_ID: "3530"
  DBT_CLOUD_JOB_ID: "3627"
  DBT_CLOUD_STEPS: "'dbt build -s state:modified+'"
  
steps:
  - label: ":dbt: Run dbt CI Check"
    command: "python3 .buildkite/dbt_cloud_ci.py -s $DBT_CLOUD_STEPS"
    env:
      DBT_CLOUD_PULL_REQUEST_ID: "${BUILDKITE_PULL_REQUEST}"
      DBT_CLOUD_JOB_BRANCH: "${BUILDKITE_BRANCH}"
      DBT_CLOUD_JOB_SCHEMA_OVERRIDE: "dbt_cloud_pr_${DBT_CLOUD_JOB_ID}_${BUILDKITE_PULL_REQUEST}"
```
