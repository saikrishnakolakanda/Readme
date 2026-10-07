To list all GCP projects using gcloud, run:

gcloud projects list

You'll get output similar to:

PROJECT_ID          NAME                PROJECT_NUMBER
gcp-dev-project     GCP Dev Project     123456789012
gcp-uat-project     GCP UAT Project     234567890123
gcp-prod-project    GCP Prod Project    345678901234
Useful commands

1. Check which account you're using

gcloud auth list

2. Check your current project

gcloud config get-value project

3. Set a project

gcloud config set project PROJECT_ID

Example:

gcloud config set project gcp-dev-project

4. List projects with more details

gcloud projects list --format="table(projectId,name,projectNumber,lifecycleState)"

5. List only project IDs

gcloud projects list --format="value(projectId)"
