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

![alt text](https://github.com/emergeplatform/ansible/blob/main/docs/images/gcp-test-vm.png?raw=true)

```
ansible-playbook google-cloud-platform/tests/test.yml

PLAY [create google cloud platform vm instance] ***************************************************************************************************************************************************

TASK [google-cloud-platform : allocate an ip address] *********************************************************************************************************************************************
ok: [localhost]

TASK [google-cloud-platform : create a hard drive] ************************************************************************************************************************************************
changed: [localhost]

TASK [google-cloud-platform : create a vm instance] ***********************************************************************************************************************************************
changed: [localhost]

TASK [google-cloud-platform : wait for ssh to come up] ********************************************************************************************************************************************
ok: [localhost]

TASK [google-cloud-platform : add host to groupname] **********************************************************************************************************************************************
changed: [localhost]

PLAY RECAP ****************************************************************************************************************************************************************************************
localhost                  : ok=5    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```


