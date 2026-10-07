Setting up your own GCP Billing account

Google account → Cloud Billing account → GCP projects → attach projects to billing account

A single Cloud Billing account can be linked to multiple projects, while each project can be linked to only one billing account at a time.

1. Create the Billing Account
Open the Google Cloud Console.
Make sure you are logged in with your personal GCP/Free Tier Google account, not the temporary Skills Boost student account.
Open Billing from the navigation menu.
Click Create account.
Enter:
Billing account name: e.g. Sai-Krishna-GCP-Billing
Country/region
Payment profile/billing information
Payment method, if requested
Click Submit and enable billing.

Google's current documentation confirms that a self-serve Cloud Billing account is used to pay for usage across one or more Google Cloud projects.

Google Cloud Billing – Create a billing account

2. Create your GCP projects

For your learning environment, you could create projects such as:

gcp-dev-project
gcp-test-project
gcp-uat-project
gcp-prod-project
gcp-shared-services
gcp-monitoring

Go to:

Google Cloud Console → Project selector → New Project

Create each project.

If you're following a lab that already provides a project, don't attach that temporary Skills Boost project to your personal billing account.

3. Attach an existing project to your Billing Account

For example, suppose you created:

Project name: GCP Dev Project
Project ID: gcp-dev-project

Then:

Open Google Cloud Console.
Go to Billing.
Select My Projects.
Find gcp-dev-project.
If it says Billing is disabled, open the Actions (⋮) menu.
Select Change billing.
Select your billing account:
Sai-Krishna-GCP-Billing
Click Set account.

Google documents this exact My Projects → Actions → Change billing → Set account process.

Google Cloud – Enable, disable, or change billing for a project

4. Attach multiple projects

You can repeat the same process:

Project	Billing
gcp-dev-project	Sai-Krishna-GCP-Billing
gcp-test-project	Sai-Krishna-GCP-Billing
gcp-uat-project	Sai-Krishna-GCP-Billing
gcp-prod-project	Sai-Krishna-GCP-Billing
gcp-shared-services	Sai-Krishna-GCP-Billing
gcp-monitoring	Sai-Krishna-GCP-Billing

All usage from these projects is then charged to that billing account.

5. Verify the billing

For each project:

Select project → Billing

You should see something like:

Billing account:
Sai-Krishna-GCP-Billing

Billing status:
Billing enabled

You can also go to Billing → My Projects and see the billing account associated with each project.

⚠️ Important for your Skills Boost situation

Because you mentioned that your Free Tier account and Skills Boost subscription use the same email, keep these two environments separate:

YOUR PERSONAL ACCOUNT
        │
        └── Personal Billing Account
                │
                ├── gcp-dev-project
                ├── gcp-test-project
                └── gcp-uat-project


SKILLS BOOST LAB
        │
        └── Temporary Student Account
                │
                └── Temporary Lab Project

Do not attach a Skills Boost temporary project to your personal billing account. Skills Boost labs provide their own lab credentials/project; use those credentials when the lab instructs you to access Cloud Console.

If your goal is to build the GCP Landing Zone you were working on earlier, 
I can also give you the exact order to create Billing → Organization → Folders → Projects → Shared VPC → IAM → APIs so you can build the whole setup correctly.
