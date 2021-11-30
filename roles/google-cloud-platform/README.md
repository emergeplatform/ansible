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
