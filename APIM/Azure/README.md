# Axway AMPLIFY API Management on Azure


## Dependencies
This ressource is available only for version **7.6.2-SP4** and **7.7-SP1** available on Axway website. Also new APIM version will be tested in time.

It uses Cassandra v2.2.6 for persistant database.

Although Axway AMPLIFY API Management is supported with other RBDMS, the script can only deploy a Mysql server. 

The deployment is based on a **Kubernetes version 1.15.5**, that is in preview on Azure Kubernetes Services.

## Prerequisites
For prerequisite, you must have enough permission on your subscription to create a service principal on services:
- DNS Zone contributor (only if you set to true manage DNS parameter)
- Owner on the target resource group deployment.
Please follow this [link](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/aks/kubernetes-service-principal.md) to configure one.

Then create a Blob storage account in the target region with 3 containers :
1. products : upload application package APIGateway, APIPortal and docker scripts. Go to Axway's support website [download page](https://support.axway.com/en/).
2. dependencies : Upload the mysql jar library.
3. data : Upload your Docker license key file and a fed with your configuration.
4. helmcharts : Copy the helmchart source available [here](https://github.com/Axway/Cloud-Automation/tree/master/APIM/Helmchart) 

## Deployment
Somes parameters change the deployment. Here is a resume:
- *apimVersion*. It will be used to search package and name package. Value autorized 7.6.2 and 7.7
- *projectName* and *environment* are used for naming.
- *userAdmin* and *_adminPassword* set the user on the bastion VM.
- *email* used for let's encrypt registration.
- *sourceBlobStorageName* is the blob where stored assets.
- *portal* set true to deploy API-Portal component.
- *webhookUrl* Streams log on Microsoft Teams.
- *servicePrincipalName*, *_servicePrincipalID*, *_servicePrincipalSecret* to the prefconfigured SP.
- *_tenantID*

After the deployment, the VM can be used to manage the cluster. Access in ssh is granted. (please definir an **IP restriction** for more security).
Two opportunities to deploy the solution.

### Azure Portal : Deploy without changes
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https://github.com/rsandy43/APIMTest" 4target="_blank">
    <img src="https://azuredeploy.net/deploybutton.png"/>
</a>

