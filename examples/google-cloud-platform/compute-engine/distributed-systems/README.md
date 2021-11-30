# Example
========

![alt text](https://github.com/emergeplatform/ansible/blob/main/docs/images/Distributed-Systems-Design.png?raw=true)

The example project provisions and decommissions in the Google Cloud Platform:
- 1 Virtual Private Network
- 1 Virtual Private Network Firewall
- 5 Public IP Addresses
- 5 Storage Disks
- 5 Network Devices
- 5 virtual machines running centos 8 linux

The playbooks installs  and configures the following sub-systems:
- HAProxy (load balancer),
- pgadmin4 web application,
- Network File System (NFS) + postgresql database server

The following Google Cloud Platform services are utilized:
- Cloud Identity Access Management (IAM)
- Compute Engine
- Cloud Storage
- Cloud External IP Addresses
- Cloud Firewall
- Virtual Private Cloud

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


#### Tasks for each instance

1. allocate an ip address
2. create hard drive
3. create a vm instance
 

#### Command line
```
cd ansible/examples/google-cloud-platform/compute-engine/distributed-systems
ansible-playbook -e @provision.json -e operation=provision -e removeNetwork=false -u [username] gcp-vm-instance.yml
```

The playbook role will create a GCP VM like displayed below.

![alt text](https://github.com/emergeplatform/ansible/blob/main/docs/images/gcp-test-vms.png?raw=true)


### External IP Address
![alt text](https://github.com/emergeplatform/ansible/blob/main/docs/images/gcp-vpc-external-ips.png?raw=true)

### GCP Hard Drive
![alt text](https://github.com/emergeplatform/ansible/blob/main/docs/images/gcp-vm-disks.png?raw=true)

