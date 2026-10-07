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
