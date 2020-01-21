# Customer sentiment on seller quality with Watson Natural Language Understanding on Cloud Pak for Data

In this code pattern, we will analyse the seller's quality by understanding the sentiments and emotions of reviews given by customers to the sellers and using Watson Natural Language Understanding on Cloud Pak for Data. 

In any E-Commerce website the product sellers have a rating between 0 to 5 stars which are explicitly given by the customers based on the product that have been purchased. Considering this rating into account the customers feel confident enough to purchase products from the particular seller. 

The rating which is given to the seller on e-commerce platform is just a rating given explicitly by the customers and does not make more impact to the sellers quality. We are adding more parameters to this rating to make it stronger and more impacting. We read the product reviews of a seller and analyse the sentiment and emotion behind the review with Watson Natural Language Understanding and compute a score, we also analyse the delivery status of the product and whether the product is delivered on or before the estimated date of delivery and compute another score, finally we add up these scores to get a seller quality rating between 0 to 5 stars which makes more impact to the seller ratings.

When you have completed this code pattern, you will understand how to:

* Use advanced NLP to analyze text and extract meta-data from content such as sentiment, emotion, relations, etc.
* Run small pieces of code to process your data and immediately view the results with Jupyter Notebook.
* 
* Build Interactive dashboards and produce visualizations directly from your data in real-time with Embedded Dashboard.

<!--add an image in this path-->
![architecture](doc/source/images/architecture.png)

<!--Optionally, add flow steps based on the architecture diagram-->
## Flow

1. Create a connection for the refined data in db2 into IBM Watson Studio project in Cloud Pak for Data
2. Setup Jupyter Notebook that reads the dataset from the IBM db2 Connection
3. Run the Algorithm from Jupyter notebook that computes the seller rating with the help of Watson Natural Language Understanding on Cloud Pak for Data
4. Visualise insights from the data using Watson Embedded Dashboard on Cloud Pak for Data

<!--Optionally, update this section when the video is created-->
# Pre-requisites
- Any Database. In this Code Pattern we demonstrate using [Db2 on Cloud Pak for Data] (https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/cpd/svc/db2z/create_database_db2z.html)

# Steps
## Deploy to IBM Cloud

[![Deploy to IBM Cloud](https://cloud.ibm.com/deploy/button.png)](https://cloud.ibm.com/deploy?repository=https://github.com/IBM/watson-banking-chatbot.git)

1. Press **Deploy to IBM Cloud**, and then click **Deploy**.

<!--optional step-->
2. In Toolchains, click **Delivery Pipeline** to watch while the app is deployed. After it's deployed, the app can be viewed by clicking **View app**.
![toolchain pipeline](doc/source/images/toolchain-pipeline.png)

<!--update with service names from manifest.yml-->

3. To see the app and services created and configured for this code pattern, use the IBM Cloud dashboard. The app is named `watson-banking-chatbot` with a unique suffix. The following services are created and easily identified by the `wbc-` prefix:
    * `wbc-conversation-service`
    * `wbc-discovery-service`
    * `wbc-natural-language-understanding-service`
    * `wbc-tone-analyzer-service`

## Run locally

> NOTE: These steps are only needed when running locally instead of using the **Deploy to IBM Cloud** button.

<!-- there are MANY updates necessary here, just screenshots where appropriate -->

1. [Clone the repo](#1-clone-the-repo).
2. [Create Watson services](#2-create-watson-services).
3. [Import the Watson Assistant workspace](#3-import-the-watson-assistant-workspace).
4. [Load the Watson Discovery documents](#4-load-the-watson-discovery-documents).
5. [Configure credentials](#5-configure-credentials).
5. [Run the application](#6-run-the-application).

### 1. Clone the repo

Clone the `watson-banking-chatbot` repo locally. In a terminal, run:

```bash
git clone https://github.com/IBM/watson-banking-chatbot
```

We’ll be using the file [`data/assistant/workspaces/banking.json`](data/assistant/workspaces/banking.json) and the folder
[`data/assistant/workspaces/`](data/assistant/workspaces/)

### 2. Create Watson services

Create the following services:

* [**Watson Assistant**](https://cloud.ibm.com/catalog/services/assistant)
* [**Watson Discovery**](https://cloud.ibm.com/catalog/services/discovery)
* [**Watson Tone Analyzer**](https://cloud.ibm.com/catalog/services/tone-analyzer)
* [**Watson Natural Language Understanding**](https://cloud.ibm.com/catalog/services/natural-language-understanding)

### 3. Import the Watson Assistant workspace

* Find the Watson Assistant service in your IBM Cloud Dashboard.
* Select the service, and then click **Launch tool**.
* Go to the **Skills** tab.
* Click **Create skill**.
* Click the **Import skill** tab.
* Click **Choose JSON file**, go to your cloned repo dir, and `Open` the workspace.json file in `data/conversation/workspaces/banking.json` (or the old full version in `full_banking.json`).
* Select **Everything**, and click **Import**.

To find the `WORKSPACE_ID` for Watson Assistant:

* Go back to the **Skills** tab.
* Click the three dots in the upper-right corner of the **watson-banking-chatbot** card, and select **View API Details**.
* Copy the `Workspace ID` GUID.
  ![view_api_details](doc/source/images/view_api_details.png)

*Optionally*, to view the assistant dialog, select the workspace and choose the
**Dialog** tab. Here's a snippet of the dialog:

![dialog](doc/source/images/dialog.PNG)

### 4. Load the Watson Discovery documents

Launch the **Watson Discovery** tool. Create a **new data collection**,
and give the data collection a unique name.

> Save the **environment_id** and **collection_id** for your `.env` file in the next step.

Under **Add data to this collection**, use **Drag and drop your documents here or browse from computer** to seed the content with the five documents in `data/discovery/docs`.

### 5. Configure credentials

The credentials for IBM Cloud services (Watson Assistant, Watson Discovery, 
Watson Tone Analyzer and Watson Natural Language Understanding) can be found in the **Services** menu in IBM Cloud
by selecting the **Service Credentials** option for each service.

The other settings for Watson Assistant and Watson Discovery were collected during the
earlier setup steps (``DISCOVERY_COLLECTION_ID``, ``DISCOVERY_ENVIRONMENT_ID``, and
``WORKSPACE_ID``).

Copy the [`env.sample`](env.sample) to `.env`.

```bash
cp env.sample .env
```
Edit the `.env` file with the necessary settings.

#### `env.sample:`

```bash
# Copy this file to .env and replace the credentials with
# your own before starting the app.

# Note: If you are using older services, you may need _USERNAME and _PASSWORD
# instead of _IAM_APIKEY.

# Watson Assistant
WORKSPACE_ID=<add_assistant_workspace>
ASSISTANT_URL=<add_assistant_url>
ASSISTANT_IAM_APIKEY=<add_assistant_iam_apikey>

# Watson Discovery
DISCOVERY_URL=<add_discovery_url>
DISCOVERY_ENVIRONMENT_ID=<add_discovery_environment_id>
DISCOVERY_COLLECTION_ID=<add_discovery_collection_id>
DISCOVERY_IAM_APIKEY=<add_discovery_iam_apikey>

# Watson Natural Language Understanding
NATURAL_LANGUAGE_UNDERSTANDING_URL=<add_nlu_url>
NATURAL_LANGUAGE_UNDERSTANDING_IAM_APIKEY=<add_nlu_iam_apikey>

# Watson Tone Analyzer
TONE_ANALYZER_URL=<add_tone_analyzer_url>
TONE_ANALYZER_IAM_APIKEY=<add_tone_analyzer_iam_apikey>

# Run locally on a non-default port (default is 3000)
# PORT=3000
```

### 6. Run the application

1. Install [Node.js](https://nodejs.org/en/) runtime or NPM.
1. Start the app by running `npm install`, followed by `npm start`.
1. Use the chatbot at `localhost:3000`.

> Note: The server host can be changed as required in the server.js file, and `PORT` can be set in the `.env` file.

<!--Add a section that explains to the reader what typical output looks like, include screenshots -->

# Sample output

![sample_output](doc/source/images/sample_output.png)

<!--Optionally, include any troubleshooting tips (driver issues, etc)-->

# Troubleshooting

* Error: Environment {GUID} is still not active, retry once status is active

  > This is common during the first run. The app tries to start before the Watson Discovery
environment is fully created. Allow a minute or two to pass. The environment should
be usable on restart. If you used **Deploy to IBM Cloud** the restart should be automatic.

* Error: Only one free environment is allowed per organization

  > To work with a free trial, a small free Watson Discovery environment is created. If you already have
a Watson Discovery environment, this will fail. If you are not using Watson Discovery, check for an old
service thay you might want to delete. Otherwise, use the `.env DISCOVERY_ENVIRONMENT_ID` to tell
the app which environment you want it to use. A collection will be created in this environment
using the default configuration.

<!-- keep this -->
## License

This code pattern is licensed under the Apache License, Version 2. Separate third-party code objects invoked within this code pattern are licensed by their respective providers pursuant to their own separate licenses. Contributions are subject to the [Developer Certificate of Origin, Version 1.1](https://developercertificate.org/) and the [Apache License, Version 2](https://www.apache.org/licenses/LICENSE-2.0.txt).

[Apache License FAQ](https://www.apache.org/foundation/license-faq.html#WhatDoesItMEAN)
