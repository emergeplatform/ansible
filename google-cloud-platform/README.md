Google Cloud Platform
=========

# Credentials

### GCP Service Account Key Download

![alt text](https://github.com/emergeplatform/ansible/blob/main/docs/images/gcp-test-vm.png?raw=true)

It’s easy to create a GCP account with credentials for Ansible. You have multiple options to get your credentials - here are two of the most common options:

Service Accounts (Recommended): Use JSON service accounts with specific permissions.

To work with the GCP modules, you’ll first need to get some credentials in the JSON format:

- [Create a Service Account](https://developers.google.com/identity/protocols/OAuth2ServiceAccount#creatinganaccount)
- [Download JSON credentials](https://support.google.com/cloud/answer/6158849?hl=en&ref_topic=6262490#serviceaccounts)


# Setup

### Environment Variables
```
vi ~/secure/environment/ansible/google-cloud-platform/vars
```

Enter the following environment variables like below.

```
export GCP_PROJECT_ID=your-project-id
export GCP_SERVICE_ACCOUNT_FILE=~/secure/gcp-service-account.json
```

### Installation

```
# install ansible and pip
sudo dnf install ansible pip
```

```
# install google auth plugin
pip install google-auth
```

```
# source environment variables
source ~/secure/environment/ansible/google-cloud-platform/vars
```

```
#verify environment variables are set
env | grep GCP
GCP_SERVICE_ACCOUNT_FILE=~/secure/gcp-service-account.json
GCP_PROJECT_ID=your-project-id
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
### External IP Address
![alt text](https://github.com/emergeplatform/ansible/blob/main/docs/images/gcp-expternal-ip-address.png?raw=true)

### GCP Hard Drive
![alt text](https://github.com/emergeplatform/ansible/blob/main/docs/images/gcp-test-hd.png?raw=true)

