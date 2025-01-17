GitHub Actions Workflow: TEST
This workflow, named TEST, is designed to build and push a Docker image to the Azure Container Registry (ACR). It includes validation for user permissions to ensure only authorized users can execute it.

Workflow Triggers
Manual Trigger: The workflow can only be triggered manually using the workflow_dispatch event.
Jobs and Steps
Job: build-and-push
Runs On: A self-hosted runner.
Steps:
Checkout Repository:

Uses the actions/checkout@v3 action to clone the repository.
Validate User Permissions:

Retrieves a list of allowed users from the repository variable ALLOWED_USERS.
Verifies if the workflow initiator ($GITHUB_ACTOR) or the re-run initiator ($GITHUB_TRIGGERING_ACTOR) is authorized.
If unauthorized, the workflow terminates.
Get Git Commit ID:

Retrieves the short Git commit hash and stores it as an environment variable (COMMIT_ID).
Build Docker Image:

Builds a Docker image tagged with the short commit ID:
ostacrdev.azurecr.io/wdfe:<commit_id>.
Push Docker Image:

Pushes the Docker image to the Azure Container Registry (ACR).

Usage:
Define a repository variable ALLOWED_USERS with a comma-separated list of authorized GitHub usernames.
Manually trigger the workflow from the Actions tab in your GitHub repository.
Ensure the self-hosted runner has the necessary permissions to build and push Docker images.
This workflow ensures security by restricting access to authorized users and enables efficient Docker image management with versioning based on Git commit IDs.
