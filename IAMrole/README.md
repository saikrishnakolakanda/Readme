1. IAM — Identity and Access Management
IAM controls who can access GCP resources and what they are allowed to do.
It uses members (users/service accounts) + roles + permissions to control access.
Simple example:
Developer → Viewer role → GCP Project

2. Identity Federation
Identity Federation allows users or applications from another identity provider to access GCP without creating or storing GCP passwords/keys.
GCP trusts the external identity provider and gives temporary access.
Simple example:
GitHub Actions → Workload Identity Federation → GCP

3. Service Account
A service account is a special Google identity used by applications, VMs, pipelines, and automation, rather than a human.
It can be given IAM roles so that an application can access specific GCP resources.
Simple example:
Jenkins → Service Account → GCP resources

IAM role to a Google user account. The user first needs a Google account (for example, yourname@gmail.com), and then you add that email as a principal and assign the required role.

Steps in GCP Console
Open Google Cloud Console.
Select your project from the project selector at the top.
Go to:
IAM & Admin → IAM
Click Grant Access.
In New principals, enter the user's Google account email.

Example:

saikrishna.example@gmail.com
Under Assign roles, click Select a role.
Choose the required role.

For example:

Basic
 └── Viewer

Compute Engine
 └── Compute Viewer

Kubernetes Engine
 └── Kubernetes Engine Developer

Storage
 └── Storage Object Viewer
Click Save.

The user now has that role on the selected project.

Example

Suppose you want:

User:
developer@gmail.com

Project:
gcp-dev-project

Role:
Compute Engine Viewer

You would configure:

IAM & Admin
     ↓
IAM
     ↓
Grant Access
     ↓
New principal
developer@gmail.com
     ↓
Role
Compute Engine → Compute Viewer
     ↓
Save

The user can then sign in with developer@gmail.com and access the resources permitted by that role.

Important distinction: User vs Service Account

For your GCP DevOps/landing-zone setup, you'll commonly have both:

Identity	Example	Used for
User	developer@gmail.com	Human accessing GCP Console
Service Account	terraform-deployer@project.iam.gserviceaccount.com	Terraform/CI/CD workloads
Google Group	gcp-devops@company.com	Managing permissions for multiple users

For humans, use a Google user or preferably a Google Group in an organization environment.

For Terraform, Jenkins, GitHub Actions, etc., use a service account / Workload Identity Federation, rather than giving a personal user account permissions.

If you're building your GCP Landing Zone, I recommend setting up the IAM hierarchy as:

Organization
   │
   ├── Folder: Non-Prod
   │      ├── Dev
   │      ├── QA
   │      └── UAT
   │
   └── Folder: Prod
          └── Production

Users / Groups
       ↓
IAM Roles
       ↓
Folders / Projects
       ↓
Resources

This is much closer to how IAM is normally designed in a production GCP environment.

Perfect. ✅ You successfully created the service account in your active project.

What you created

Project:

devops-iam-demo-1791371340

Service account:

devops-bot@devops-iam-demo-1791371340.iam.gserviceaccount.com

Display name:

DevOps Pipeline Bot
Verify it

Run:

gcloud iam service-accounts list

You should see:

DISPLAY NAME           EMAIL
DevOps Pipeline Bot    devops-bot@devops-iam-demo-1791371340.iam.gserviceaccount.com
If you're following the IAM lab

The next step is usually to grant this service account a role.

For example, to give it Viewer access to the project:

gcloud projects add-iam-policy-binding devops-iam-demo-1791371340 \
  --member="serviceAccount:devops-bot@devops-iam-demo-1791371340.iam.gserviceaccount.com" \
  --role="roles/viewer"

Then verify:

gcloud projects get-iam-policy devops-iam-demo-1791371340

You should see:

role: roles/viewer
members:
- serviceAccount:devops-bot@devops-iam-demo-1791371340.iam.gserviceaccount.com

Important: For a real DevOps pipeline, avoid giving the service account broad roles such as Owner or Editor. Use the minimum roles required for the pipeline.
