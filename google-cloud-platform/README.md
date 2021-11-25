Google Cloud Platform
=========

# Credentials
It’s easy to create a GCP account with credentials for Ansible. You have multiple options to get your credentials - here are two of the most common options:

Service Accounts (Recommended): Use JSON service accounts with specific permissions.

To work with the GCP modules, you’ll first need to get some credentials in the JSON format:

- Create a Service Account
- Download JSON credentials


# Setup

### Environment Variables

```
export GCP_PROJECT_ID=your-project-id
export GCP_SERVICE_ACCOUNT_FILE=~/secure/gcp-service-account.json
```

### Installation

```
sudo dnf install ansible pip
pip install google-auth
source ~/secure/environment/ansible/google-cloud-platform/vars
env | grep GCP
```

# Testing 

### Create GCP VM Instance

```
ansible-playbook google-cloud-platform/tests/test.yml
```
