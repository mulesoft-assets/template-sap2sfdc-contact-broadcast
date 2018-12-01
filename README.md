
# Anypoint Template: SAP to Salesforce Contact Broadcast	

<!-- Header (start) -->
Broadcast changes to contacts in SAP as accounts to Salesforce in real time. The detection criteria, and fields that should be moved are configurable. Additional systems can be added to be notified of the changes. 

Real time synchronization is achieved via rapid polling of SAP. Note that this template also brings over the parent customer (account in Salesforce) if it does not already exist in Salesforce. 

This template uses both Mule batch and watermarking capabilities to ensure that only recent changes are captured and that it can efficiently process large amounts of records.

![b558c678-c644-48c7-9fed-6c4d135e2ec0-image.png](https://exchange2-file-upload-service-kprod.s3.us-east-1.amazonaws.com:443/b558c678-c644-48c7-9fed-6c4d135e2ec0-image.png)

<!-- Header (end) -->

# License Agreement
This template is subject to the conditions of the <a href="https://s3.amazonaws.com/templates-examples/AnypointTemplateLicense.pdf">MuleSoft License Agreement</a>. Review the terms of the license before downloading and using this template. You can use this template for free with the Mule Enterprise Edition, CloudHub, or as a trial in Anypoint Studio. 
# Use Case
<!-- Use Case (start) -->
This template is for an online sync of contacts from SAP to Salesforce as a push notification. Each time there is a new contact or a change in an existing one, SAP sends the IDoc with it to the running template which will update or create a contact in the Salesforce target instance.

Requirements have been set not only to be used as examples, but also to act as a starting point to adapt your integration to your requirements.

This template leverages the Mule batch module. The batch job is divided in *Process* and *On Complete* stages.

The integration is triggered by an inbound SAP endpoint listening for incoming IDOC **DEBMAS01** messages including information about a customer's contacts. This XML is passed to the batch process and transformed to a Salesforce contact.

In this template you may choose whether an account for a contact should be created as well during the process.
This functionality relies on a standard BAPI for retrieving details about customers: **BAPI_CUSTOMER_GETDETAIL2**
<!-- Use Case (end) -->

# Considerations
<!-- Default Considerations (start) -->

<!-- Default Considerations (end) -->

<!-- Considerations (start) -->
To make this template run, there are certain preconditions that must be considered.
All of them deal with the preparations in both source (SAP) and destination (Salesforce) systems, that must be made for the template to run smoothly. Failing to do so could lead to unexpected behavior of the template.

## Disclaimer

This template uses a few private Maven dependencies from MuleSoft to work. If you intend to run this template with Maven support, you need to add extra dependencies for SAP to the pom.xml file.
<!-- Considerations (end) -->


## SAP Considerations

Here's what you need to know to get this template to work with SAP.

### As a Data Source

The SAP backend system is used as a source of data. The SAP connector is used to send and receive the data from the SAP backend. The connector can either use RFC calls of BAPI functions and/or IDoc messages for data exchange, and needs to be properly customized per the "Properties to Configure" section.

The partner profile needs to have a customized type of logical system set as partner type. An outbound parameter of message type DEBMAS should be defined in the partner profile. An RFC destination created earlier should be defined as the receiver port. THe IDoc type base type should be set as DEBMAS01.

## Salesforce Considerations

Here's what you need to know about Salesforce to get this template to work:

- Where can I check that the field configuration for my Salesforce instance is the right one? See: <a href="https://help.salesforce.com/HTViewHelpDoc?id=checking_field_accessibility_for_a_particular_field.htm&language=en_US">Salesforce: Checking Field Accessibility for a Particular Field</a>.
- Can I modify the Field Access Settings? How? See: <a href="https://help.salesforce.com/HTViewHelpDoc?id=modifying_field_access_settings.htm&language=en_US">Salesforce: Modifying Field Access Settings</a>.

### As a Data Destination

There are no considerations with using Salesforce as a data destination.

# Run it!
Simple steps to get this template running.
<!-- Run it (start) -->

<!-- Run it (end) -->

## Running On Premises
In this section we help you run this template on your computer.
<!-- Running on premise (start) -->

<!-- Running on premise (end) -->

### Where to Download Anypoint Studio and the Mule Runtime
If you are new to Mule, download this software:

+ [Download Anypoint Studio](https://www.mulesoft.com/platform/studio)
+ [Download Mule runtime](https://www.mulesoft.com/lp/dl/mule-esb-enterprise)

**Note:** Anypoint Studio requires JDK 8.

<!-- Where to download (start) -->
<!-- Where to download (end) -->

### Importing a Template into Studio
In Studio, click the Exchange X icon in the upper left of the taskbar, log in with your Anypoint Platform credentials, search for the template, and click Open.
<!-- Importing into Studio (start) -->

<!-- Importing into Studio (end) -->

### Running on Studio
After you import your template into Anypoint Studio, follow these steps to run it:

+ Locate the properties file `mule.dev.properties`, in src/main/resources.
+ Complete all the properties required as per the examples in the "Properties to Configure" section.
+ Right click the template project folder.
+ Hover your mouse over `Run as`.
+ Click `Mule Application (configure)`.
+ Inside the dialog, select Environment and set the variable `mule.env` to the value `dev`.
+ Click `Run`.
<!-- Running on Studio (start) -->
For this template to run in Anypoint Studio there are a few extra steps that needs to be made.
See [Configuring the Connector in Studio 7](https://docs.mulesoft.com/connectors/sap/sap-connector#configuring-the-connector-in-studio-7)
<!-- Running on Studio (end) -->

### Running on Mule Standalone
Update the properties in one of the property files, for example in mule.prod.properties, and run your app with a corresponding environment variable. In this example, use `mule.env=prod`. 


## Running on CloudHub
When creating your application in CloudHub, go to Runtime Manager > Manage Application > Properties to set the environment variables listed in "Properties to Configure" as well as the mule.env value.
<!-- Running on Cloudhub (start) -->

<!-- Running on Cloudhub (end) -->

### Deploying a Template in CloudHub
In Studio, right click your project name in Package Explorer and select Anypoint Platform > Deploy on CloudHub.
<!-- Deploying on Cloudhub (start) -->

<!-- Deploying on Cloudhub (end) -->

## Properties to Configure
To use this template, configure properties such as credentials, configurations, etc.) in the properties file or in CloudHub from Runtime Manager > Manage Application > Properties. The sections that follow list example values.
### Application Configuration
<!-- Application Configuration (start) -->
**Application Configuration**
+ page.size `200`

**SAP Connector Configuration**

+ sap.jco.ashost `your.sap.address.com`
+ sap.jco.user `SAP_USER`
+ sap.jco.passwd `SAP_PASS`
+ sap.jco.sysnr `14`
+ sap.jco.client `800`
+ sap.jco.lang `EN`

**SAP Endpoint Configuration**

+ sap.jco.operationtimeout `10000`
+ sap.jco.connectioncount `2`
+ sap.jco.gwhost `your.sap.addres.com`
+ sap.jco.gwservice `sapgw14`
+ sap.jco.idoc.programid `PROGRAM_ID`

**SalesForce Connector Configuration**

+ sfdc.username `bob.dylan@sfdc`
+ sfdc.password `DylanPassword123`
+ sfdc.securityToken `avsfwCUl7apQs56Xq2AKi3X`

**Policy for creating accounts in Salesforce syncAccount, doNotCreateAccount**

+ account.sync.policy `syncAccount`

**Note:** The property **account.sync.policy** can take any of the two following values:

+ **doNotCreateAccount**: Application does nothing to the account and just moves the contact over.
+ **syncAccount**: Tries to create the contact's account if it's not present in the Salesforce instance.
<!-- Application Configuration (end) -->

# API Calls
<!-- API Calls (start) -->
SalesForce imposes limits on the number of API calls that can be made.
Therefore calculating this amount may be an important factor to consider. 

The template calls to the API can be calculated using the formula:

**X * 3 + X / ${page.size}** -- Where X is the number of contacts to synchronize on each run.

Multiply by 3 because for every user if account.sync.policy is set to the **syncAccounts** value, then every contact is checked if an account with a matching name exists in Salesforce. If not, it's created.

Divide by ${page.size} because contacts are gathered in groups of ${page.size} for each Upsert API call in the commit step.

For instance if 10 records are fetched from origin instance, then 31 API calls to Salesforce are made (worst case scenario). If the account in Salesforce already exists or account synchronization is disabled, there will be fewer API calls made.
<!-- API Calls (end) -->

# Customize It!
This brief guide provides a high level understanding of how this template is built and how you can change it according to your needs. As Mule applications are based on XML files, this page describes the XML files used with this template. More files are available such as test classes and Mule application files, but to keep it simple, we focus on these XML files:

* config.xml
* businessLogic.xml
* endpoints.xml
* errorHandling.xml

<!-- Customize it (start) -->

<!-- Customize it (end) -->

## config.xml

<!-- Default Config XML (start) -->
This file provides the configuration for connectors and configuration properties. Only change this file to make core changes to the connector processing logic. Otherwise, all parameters that can be modified should instead be in a properties file, which is the recommended place to make changes.
<!-- Default Config XML (end) -->

<!-- Config XML (start) -->

<!-- Config XML (end) -->

## businessLogic.xml

<!-- Default Business Logic XML (start) -->
The business logic XML file creates or updates objects in the destination system for a represented use case. You can customize and extend the logic of this template in this XML file to more meet your needs.
<!-- Default Business Logic XML (end) -->

<!-- Business Logic XML (start) -->

<!-- Business Logic XML (end) -->

## endpoints.xml

<!-- Default Endpoints XML (start) -->
This file contains the endpoints for triggering the template and for retrieving the objects that meet the defined criteria in a query. You can execute a batch job process with the query results.
<!-- Default Endpoints XML (end) -->

<!-- Endpoints XML (start) -->

<!-- Endpoints XML (end) -->

## errorHandling.xml

<!-- Default Error Handling XML (start) -->
This file handles how your integration reacts depending on the different exceptions. This file provides error handling that is referenced by the main flow in the business logic.
<!-- Default Error Handling XML (end) -->

<!-- Error Handling XML (start) -->

<!-- Error Handling XML (end) -->

<!-- Extras (start) -->

<!-- Extras (end) -->
