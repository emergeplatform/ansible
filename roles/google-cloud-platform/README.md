Google Cloud Platform
=========

### Interesting Facts

- Google overhead is ~12% including cafeterias
- 75,000 machines per data center
- Network bandwidth 1 petabit per second (more data than the entire internet)
- Software designed networking principles abstract physical network features and allow users to program custom networks
- Networking technology (IPv6, fiber cable, etc) is designed to keep up with the growing global capacity
- Low latency and high throughput networking technology allows users to reliably access storage and computing resources
- Each data center is running and connected on B4 internet backbone (google’s privately owned highly efficient SDN-based internet backbone)
- Hard drives and SSD failure are securely replaced and destroyed daily following a secure procedures tested regularally for effectiveness


# Credentials for Authentication

### GCP Service Account

To work with the GCP modules, you’ll first need to get some credentials in the JSON format:

- [Create a Service Account](https://developers.google.com/identity/protocols/OAuth2ServiceAccount#creatinganaccount)
- [Download JSON credentials](https://support.google.com/cloud/answer/6158849?hl=en&ref_topic=6262490#serviceaccounts)

In this example, we use "ansible-gcp-automation" as the service account name and choose Compute Engine Admin as the role. This provides ansible with full control of all Compute Engine resources.

#### Serice Account Role

![alt text](https://github.com/emergeplatform/ansible/blob/main/docs/images/gcp-service-account-role.png?raw=true)

#### Service Account Key

![alt text](https://github.com/emergeplatform/ansible/blob/main/docs/images/gcp-service-account-key.png?raw=true)

Once your add new key, the browser will begin to download the .json file to your systems download directory.

Make sure to move and rename the file to a secure location, separate from the project directory.

### Move credentials to secure folder

```
mv ~/Downloads/your-project-id-xxxxxxx.json ~/secure/gcp-service-account.json
```



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

### Variables

```yaml
---
# vars file for google-cloud-platform
vm_name: test-gcp-vm
disk_name: test-hard-drive
ip_name: test-ip-address
machine_type: n1-standard-1
zone: "us-central1-a"
region: "us-central1"
service_account_file: "{{ lookup('env', 'GCP_SERVICE_ACCOUNT_FILE') }}"
project: "{{ lookup('env', 'GCP_PROJECT_ID') }}"
auth_kind: serviceaccount
disk_size_gb: 100
disk_img: projects/centos-cloud/global/images/centos-8-v20211105
scopes:
  - https://www.googleapis.com/auth/compute
```

### Create GCP VM Instance

#### Tasks

1. allocate an ip address
2. create hard drive
3. create a vm instance
 

#### Command line
```
ansible-playbook gcp-vm-instance.yml
```

The playbook role will create a GCP VM like displayed below.

![alt text](https://github.com/emergeplatform/ansible/blob/main/docs/images/gcp-test-vm.png?raw=true)

### Example output

```
PLAY [create google cloud platform vm instance] ***************************************************************************************************************************************************

TASK [google-cloud-platform : allocate an ip address] *********************************************************************************************************************************************
ok: [localhost]

TASK [google-cloud-platform : create a hard drive] ************************************************************************************************************************************************
ok: [localhost]

TASK [google-cloud-platform : create a vm instance] ***********************************************************************************************************************************************
ok: [localhost]

TASK [google-cloud-platform : allocate an ip address] *********************************************************************************************************************************************
ok: [localhost]

TASK [google-cloud-platform : create a hard drive] ************************************************************************************************************************************************
ok: [localhost]

TASK [google-cloud-platform : create a vm instance] ***********************************************************************************************************************************************
ok: [localhost]

PLAY RECAP ****************************************************************************************************************************************************************************************
localhost                  : ok=6    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
```
### External IP Address
![alt text](https://github.com/emergeplatform/ansible/blob/main/docs/images/gcp-expternal-ip-address.png?raw=true)

### GCP Hard Drive
![alt text](https://github.com/emergeplatform/ansible/blob/main/docs/images/gcp-test-hd.png?raw=true)

