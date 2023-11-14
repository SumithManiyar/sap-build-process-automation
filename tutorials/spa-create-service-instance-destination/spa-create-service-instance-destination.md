---
parser: v2
author_name: Chaitanya Priya Puvvada
author_profile: https://github.com/chaitanya-priya-puvvada
keywords: destination
auto_validation: true
time: 10
tags: [ tutorial>beginner, software-product>sap-business-technology-platform, tutorial>free-tier]
primary_tag: software-product>sap-build-process-automation
---

# Create Destination to Trigger Process From any Service
<!-- description --> Create a destination to trigger a business process by creating a service instance and service key of SAP Build Process Automation.

## Prerequisites
- Subscribe to [SAP Build Process Automation using booster in SAP BTP Free Tier](spa-subscribe-booster) **OR**
- Subscribe to [SAP Build Process Automation using SAP BTP Free Trial](spa-subscribe-free-trial)
- Proper roles to create service instance, service key and destinations in SAP BTP Cockpit

## You will learn
- How to create a destination in the SAP BTP cockpit to start a business process from SAP Build Apps.
- How to create a service instance and service key for SAP Build Process Automation

## Intro
In this tutorial, you will create a service instance and service key for SAP Build Process Automation. You would consume the credentials of the service key of SAP Build Process Automation to create a destination that would trigger a business process from SAP Build Apps.

---

### Create an instance for SAP Build Process Automation

Once you have successfully subscribed to SAP Build Process Automation in SAP BTP Cockpit, you can find the Subscription in  your subaccount view, under **Instances and Subscriptions**.

<!-- border --> ![SBPA Service](1.png)

> **IMPORTANT:** If you are using a SAP BTP Free Trial account, the Instance **SPA-instance** and the Key **SBPA key** get automatically created when you subscribe to SAP Build Process Automation in SAP BTP Cockpit. You will find the Instance under **Instances and Subscriptions > Instances**. Please skip to step 2.3 to retrieve the credentials of your key. 

1. Let's create an **Instance** for SAP Build Process Automation. Choose **Create**.

2. Select the Service as **SAP Build Process Automation** and plan as **standard instance**.

    <!-- border --> ![Create](2.png)

3. Enter the values for other fields as shown below and give an instance name as **spa-adoption-us**. Choose **Create**.

    | Field|Value
    | --- | :---
    | Service | SAP Build Process Automation
    | Plan | standard - Instance
    | Runtime Environment | Cloud Foundry
    | Space | dev
    | Instance Name | any name   (spa-adoption-us)

    <!-- border --> ![Create](3.png)  

4. Once the instance is created successfully, you can find it in **Instances** section.

    <!-- border --> ![Create](6.png)  

### Create a service key for the instance of SAP Build Process Automation  

1. Once you have successfully created the instance, select **...** > **Create Service Key**.

    <!-- border --> ![Create](7.png)  

2. Enter the name for Service Key as **spa-key** and choose **Create**.

    <!-- border --> ![Create](8.png)  

3. The service key is created and you can view the credentials.

    <!-- border --> ![Create](9.png)  

4. After the key is provisioned, open it and take note of the following fields:

    - `api`
    - `clientid`
    - `clientsecret`
    - `url`

    These values are needed later in the **Destination Configuration** section.

    <!-- border --> ![Create](9.1.png)  

### Create a destination to trigger process

1. Navigate to **Destinations** > **Create Destination**. Enter the destination name as `spa_process_destination`.

    <!-- border --> ![Create](10.png)

2. Enter the details as below.

    | Field|Value
    | --- | :---
    | Name | any name (`spa_process_destination`)
    | Type | HTTP
    | Description | any description
    | URL | `api/public/workflow/rest/v1/workflow-instances`, where `api` is noted previously in step 2<div>&nbsp;</div> such as: `https://spa-api-gateway-bpi-us-prod.cfapps.us10.hana.ondemand.com/public/workflow/rest/v1/workflow-instances`
    | Proxy Type | Internet
    | Authentication |  OAuth2ClientCredentials
    | Use `mTLS` for token retrieval |  Off
    | Client ID | Paste the client id noted previously in step 2
    | Client Secret | Paste the client secret noted previously in step 2
    | Token Service URL Type | Dedicated
    | Token Service URL|  `url/oauth/token`, where `url` is noted previously in step 2<div>&nbsp;</div>The final URL should be something like this: <div></div>`https://<your tenant>.authentication.<domain>.hana.ondemand.com/oauth/token`
    | Token Service User| Blank
    | Token Service Password| Blank

    > Additionally, enable the following Properties when you would like to integrate with SAP Build Apps.

    - `AppgyverEnabled`
    - `HTML5.DynamicDestination`
    - `WebIDEEnabled`  
    - `sap.processautomation.enabled`

    <!-- border --> ![Create](11.png)    

    You have successfully created a destination and you can trigger your business process from any service like SAP Build Apps.

### Test the destination

When you will check the connection to the destination, the status will show **401: Unauthorized**. 

> Even though the connection returns unauthorized, the status is successful.

<!-- border --> ![Status connection](12.png) 
