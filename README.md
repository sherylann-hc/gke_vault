# Vault in Kubernetes

This repo provides a demo non prodcution app that works with HashiCorp Vault 

### Installation
#### Locally
Deploy this follow these steps

Edit the Variables to suit your envrioment and account detail

1. clone this repo
2. Run Terrafom init
3. Run Terraform apply 

Once the apply is compelete connect to your Kubenetes envrioment via your cloud shell and verify the pods are up using kubectl get pods

Now

1. clone this repo into your shell https://github.com/dawright22/app_stack.git
2. change into this repo and run ./full_stack_deploy.sh

#### Via Terraform Cloud (TFC)
If you are new to TFC, complete this tutorial: https://learn.hashicorp.com/collections/terraform/cloud-get-started

1. Fork this repo
2. Set Up your TFC Account and Organization
3. Create a new Workspace and select the "Version control workflow" 
4. Choose the repo you forked
5. Update Variables
6. Ensure K8s Engine API is enabled in APIs & Services
7. Queue and Run the plan </br>

**Retrieve and update the Variables in TFC**

Review variables.tf

1. Create a GCP project
2. Create a service account key: https://console.cloud.google.com/apis/credentials/serviceaccountkey </br>
   * Select the project you created in the previous step.
   * Click "Create Service Account".
   * Give it any name you like and click "Create".
   * For the Role, choose "Project -> Editor", then click "Continue".
   * Skip granting additional users access, and click "Done".

   After you create your service account, download your service account key.

   * Select your service account from the list.
   * Select the "Keys" tab.
   * In the drop down menu, select "Create new key".
   * Leave the "Key Type" as JSON.
   * Click "Create" to create the key and save the key file to your system.
3. Upload key file to your repo

What you will require:</br>
```
Add Terraform Variables 
gcp_project : "<project-name>"

Add Environment Variables
GOOGLE_APPLICATION_CREDENTIALS : "<key-file-location>"
```

### What you get!
A standalone vault instance that can be either OSS (default) or Enterprise to demonstrate dynamic user credentials and trasit data encryption as a service 

### Vault
You can connect to the Vault UI and see the secrets engines enabled using http://<EXTERNAL_IP:8200>

You will need to login in using the ROOT TOKEN from the init.json file located in app_stack/vault/init.json to authenticate

it should look like this:

![](/images/vault.png)

### Transit-app

Execute kubectl get svc transit-app to see the ip address to connect too

You can connect to the app UI and add or change record using http://<EXTERNAL_IP:5000>

![](/images/tranist-app.png)


### Clean up
in the app_stack repo run the ./cleanup.sh
