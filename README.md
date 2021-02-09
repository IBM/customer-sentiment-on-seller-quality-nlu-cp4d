
# Use advanced NLU to determine sellers’ quality

In this code pattern, we will analyse sellers quality by understanding the sentiments and emotions of reviews given by customers to the sellers using Watson Natural Language Understanding on Cloud Pak for Data or IBM Cloud and give a more impactful seller rating to the sellers. 

In any E-Commerce website the product sellers have a rating between 0 to 5 stars which are explicitly given by the customers based on the product that have been purchased. Considering this rating into account the customers feel confident enough to purchase products from the particular seller. 

The rating which is given to a seller on e-commerce platform is just a rating given explicitly by the customers and does not make more impact to the sellers quality. We are adding more parameters to this rating to make it stronger and more impactful. We read the product reviews of a seller and analyse the sentiment and emotion behind the review with Watson Natural Language Understanding and compute a score, we also analyse the delivery status of the product and whether the product is delivered on or before the estimated date of delivery and compute another score, finally we sum up these scores to get a seller quality rating between 0 to 5 stars which makes more impact to the seller ratings.

When you have completed this code pattern, you will understand how to:

* Use advanced NLP to analyze text and extract meta-data from content such as sentiment, emotion, relations, etc.
* Run small pieces of code to process your data and immediately view the results with Jupyter Notebook.
* Use Data Refinery to prepare training data for an Machine Learning task.
* Build Interactive dashboards and produce visualizations directly from your data in real-time with Embedded Dashboard.

<!--add an image in this path-->
![architecture](doc/source/images/architecture.png)

<!--Optionally, add flow steps based on the architecture diagram-->
## Flow

1. Create a connection for the refined data in db2 into IBM Watson Studio project in Cloud Pak for Data or IBM Cloud.

2. Setup Jupyter Notebook that reads the dataset from the IBM db2 Connection.

3. Run the Algorithm from Jupyter notebook that computes the seller rating with the help of Watson Natural Language Understanding on Cloud Pak for Data or IBM Cloud.

4. Visualise insights from the data using Watson Embedded Dashboard on Cloud Pak for Data or IBM Cloud.

<!--Optionally, update this section when the video is created-->
## Pre-requisites
- Implementation of this Code Pattern requires a basic understanding of Data Refinery and it also makes use of the dataset created in the tutorial [Collect, cleanse, and enhance your data](https://developer.ibm.com/tutorials/collect-cleanse-and-enhance-your-data/?utm_medium=OSocial&utm_source=Facebook&utm_content=000039JL&utm_term=10013593&utm_id=2020-general&cm_mmc=OSocial_Facebook-_-Audience+Developer_Developer+Conversation-_-WW_WW-_-2020-general_ov75912&cm_mmca1=000039JL&cm_mmca2=10013593&social_post=3227766987&linkId=85137945). Please complete the above tutorial before implementing this code pattern.

- Any SQL Database. 
>In this Code Pattern we demonstrate using [Db2 on Cloud Pak for Data](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/cpd/svc/db2z/create_database_db2z.html)

- [IBM Cloud Account](https://cloud.ibm.com/)

## Steps

1. [Download the Dataset](#1-download-the-dataset)

2. [Create Watson Natural Language Understanding Service](#2-create-watson-natural-language-understanding-service)

3. [Create a Project](#3-create-a-project) **_(Already completed as a part of the Tutorial)_**

4. [Add Db2 Connection to the Project](#4-add-db2-connection-to-the-project) **_(Already completed as a part of the Tutorial)_**

5. [Prepare and Run the Jupyter Notebook](#5-prepare-and-run-the-jupyter-notebook)

6. [Add Embedded Dashboard to the Project](#6-add-embedded-dashboard-to-the-project)

7. [Visualize the Dashboard](#7-visualize-the-dashboard)

### 1. Download the Dataset

In this Code Pattern we are going to use **Customised version of Brazilian E-Commerce Public Dataset by Olist** that we created in the Tutorial [Prepare your Dataset for your ML Models using Data Refinery from Db2](https://developer.ibm.com/tutorials/collect-cleanse-and-enhance-your-data).

We are also going to use **Consumer Reviews of Amazon Products** from Kaggle. Download the dataset from the link below.

- <https://www.kaggle.com/datafiniti/consumer-reviews-of-amazon-products>

After Downloading, Extract the `consumer-reviews-of-amazon-products.zip` file.

We’ll be using the following files:

_`Datafiniti_Amazon_Consumer_Reviews_of_Amazon_Products_May19.csv`_ : This dataset is a list of over 28,000 consumer reviews for Amazon products like the Kindle, Fire TV Stick, and more from Datafiniti's Product Database updated between February 2019 and April 2019.

As we don’t have a proper dataset with product reviews and product delivery status, we are cooking up the dataset by assuming that the products from the **Customised version of Brazilian E-Commerce Public Dataset by Olist and the Consumer Reviews of Amazon Products** are the same and thereby we are merging these 2 sets of datasets as 1 dataset and using the Jupyter Notebook.

### 2. Create Watson Natural Language Understanding Service

We will be using Watson Natural Language Understanding service to read the comments of the customer and analyse the Sentiment and Emotions of the Customers review.

- Create a [Watson Natural Language Understanding](https://cloud.ibm.com/catalog/services/natural-language-understanding) service on IBM Cloud.

- Once the service is created copy the **API Key** and **URL** of the service as shown.

![nluCredentials](doc/source/images/nluCredentials2.png)

**NOTE: These credentials are important as it will be used in [step 5](#5-prepare-and-run-the-jupyter-notebook)**

### 3. Create a Project  
### _(You will have already completed this step as a part of the Tutorial, use the same project)_

<details><summary><b>IBM Cloud Pak for Data</b></summary>
    
- Create a Project in Cloud Pak for Data choose an Empty Project.

![createProject](doc/source/images/emptyProject.png)

- Once The Project is Created you will see the below page.

![projectDashboard](doc/source/images/projectDashboard.png)

</details>

<details><summary><b>IBM Cloud</b></summary>
    
* Create [**Watson Studio**](https://cloud.ibm.com/catalog/services/watson-studio) service.

![createwatsonstudio](/doc/source/images/createwatsonstudio.png)

* Then click on **Get Started**.

* In Watson Studio click **`Create a project > Create an empty project`** and name it **_`Retail`_**.

![watsonstudioproject](/doc/source/images/watsonstudioproject.png)

</details>

### 4. Add Db2 Connection to the Project 

Now that we have created a project, we will start adding components to our project. We will start by adding Db2 Connection to our project first.

### _(You will have already completed this step as a part of the Tutorial, use the same project)_

<details><summary><b>IBM Cloud Pak for Data</b></summary>
    
- Click on **Add to Project** and select **Connection**. If you have followed [step 2](#2-create-watson-natural-language-understanding-service) select **Db2** from the list and add the credentials of your provisioned Db2 Instance. If you have a different database then you can select that and fill in the credentials.

![gif](doc/source/images/create_connection.gif)

- After filling the credentials click on **Test Connection** to make sure you have entered correct credentials. Finally select **Create**.

![connection](doc/source/images/connImage.png)

</details>

<details><summary><b>IBM Cloud </b></summary>
    
* Click on **Add to Project** and select **Connection**. If you have followed [step 2](#2-create-watson-natural-language-understanding-service) select **Db2** from the list and add the credentials of your provisioned Db2 Instance. If you have a different database then you can select that and fill in the credentials.

![gif](doc/source/images/create_connection2.gif)

* After filling the credentials click on **Create**.

![connection](doc/source/images/connImage2.png)

</details>

**NOTE: The Database Credentials will be provided by your Database administrator. If you have provisioned a Db2 instance on Cloud Pak for Data then you can follow the steps [here](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/create-db.html#create-db) to get the credentials.**

### 5. Prepare and Run the Jupyter Notebook

We have successfully created a project and added Db2 Connection to our project. We will now add the required credentials to our python Jupyter notebook and run the notebook.

#### 5.1. Prepare the Notebook

- Add Jupyter notebook to the Project by clicking on **Add to Project** and select **Notebook**. Click on **New Notebook from URL** and paste the below URL and create a Notebook.
  - [https://github.com/IBM/customer-sentiment-on-seller-quality-nlu-cp4d/blob/master/notebook/customer-sentiment-on-seller.ipynb](https://github.com/IBM/customer-sentiment-on-seller-quality-nlu-cp4d/blob/master/notebook/customer-sentiment-on-seller.ipynb)

![createJupyterNotebook](doc/source/images/createJupyterNbCp4d.gif)

- Once the notebook is created we will have to fill in 4 Cells with the following:
  - Watson Natural Language Understanding Credentials
  - Upload the Consumer Reviews of Amazon Products dataset and insert Pandas Dataframe
  - Insert the Customised version of Brazilian E-Commerce Public Dataset by Olist from Db2
  - Insert Db2 Credentials into the Notebook

##### 5.1.1. Watson Natural Language Understanding Credentials

- Insert the credentials copied from [step 2](#2-create-watson-natural-language-understanding-service) in the cell shown below.

![nluCredentials](doc/source/images/nluCredentials.png)

##### 5.1.2. Upload the Consumer Reviews of Amazon Products dataset and insert Pandas Dataframe

- Click on the **Assets** tab, and select **browse**, from the file uploader select the extracted file from [step 1](#1-download-the-dataset) named **Datafiniti_Amazon_Consumer_Reviews_of_Amazon_Products_May19.csv** from the **Consumer Reviews of Amazon Products**.

![uploadDataset](doc/source/images/uploadDatasetCp4d.gif)

- Once the Dataset is uploaded, click on the cell which says _"Insert Customer Review Dataset here"_, click on **`Insert to code > Insert Pandas Dataframe`**. You will see the code to read the dataset in the cell.

- Finally replace the variable name to **data** as shown.

![insertPandasDf](doc/source/images/insertPandasDfCp4d.gif)

##### 5.1.3. Insert the Customised version of Brazilian E-Commerce Public Dataset by Olist from Db2

- Select the cell which says _"Insert Customer Order Details Dataset here"_, click on **Connections** in the assets tab and select **`Insert to code > Insert Pandas Dataframe`** from your Db2 Connection variable. Select the Schema of your table and choose **DERIVEDDATA** and click on _Select_.

>NOTE: If you have used Db2 Instance then the schema name is your _Username_.

- Once the credentials are inserted, replace the variable name to **data2** as shown.

![insertPandasDf](doc/source/images/insertPandasDfForDBCp4d.gif)

##### 5.1.4. Insert Db2 Credentials into the Notebook

- Select the cell which says _"Insert Db2 Connection Credentials here"_, click on **Connections** in the assets tab and select **`Insert to code > Insert Credentials`** from your Db2 Connection variable.

- Once the credentials are inserted, replace the variable name to **`credentials_1`** as shown.

![insertDbCredentials](doc/source/images/insertDbCredentialsCp4d.gif)

#### 5.2. Run the Notebook

After all the Preperations are done, we will run the Jupyter Notebook by Clicking on **`Cell > Run All`** as shown.

![runAllCells](doc/source/images/runAllCellscp4d.png)

**NOTE: It will take around 20 Min to complete the execution of entire notebook, please be Patient!**

### 6. Add Embedded Dashboard to the Project

The Jupyter Notebook generated the Dataset for customer sentiments on seller quality. Further the data can be visualised in an Interactive Embedded Dashboard with IBM Embedded Dashboard Service.

<details><summary><b>IBM Cloud Pak for Data</b></summary>
    
- Add Embedded Dashboard to the Project by clicking on **Add to Project** and select **Dashboard**. Click on **from file** and upload the file [`dashboard/dashboard.json`](dashboard/dashboard.json)

![embeddedDashboard](doc/source/images/addEmbeddedDashboard.gif)

</details>

<details><summary><b>IBM Cloud</b></summary>
    
- Create an [Embedded Dashboard Service](https://cloud.ibm.com/catalog/services/ibm-cognos-dashboard-embedded) on IBM Cloud.

- From the [IBM Cloud Resources](https://cloud.ibm.com/resources) open the Watson Studio and load the project **Retail**.

- Add Embedded Dashboard to the Project by clicking on **Add to Project** and select **Dashboard**. Click on **from file** and upload the file [`dashboard/dashboard.json`](dashboard/dashboard.json) and select the newly created Embedded service.

![dashboard](doc/source/images/addEmbeddedDashboardcloud.gif)

</details>

- Once the _`dashboard.json`_ file is loaded it may ask you to enter username and password. Enter the database username and password used in [step 4](#4-add-db2-connection-to-the-project).

![credentials](doc/source/images/credentialsDb.png)

- The Dashboard will give you a prompt to relink the data asset (as the database schema of my Db2 and your Db2 is different) choose the `SELLERQUALITYSCORE` and relink.

![relink](doc/source/images/relink.png)

### 7. Visualize the Dashboard

- You will see a dashboard as shown.

![visualize](doc/source/images/visualize1.png)

**NOTE: If the Dashboard takes along time to load, clear your browsing data & cache then reload.**

- The components in the dashboard are:

  - **_Analysis by Sellers_** : You can click on any seller name to visualize ratings of that particular seller.
  - _**Analysis by Products**_ : Similar to analysis by sellers, you can click on products name to visualize the particular product's ratings.
  - _**Seller Satisfaction Score**_ : For selected seller and product, the seller satisfaction score can be viewed.
  - _**Products Ratings by Seller Graph**_ : You can see the graph of every sellers with their products and the respected ratings.
  - _**Customers Emotion**_ : For selected Product and seller, along with Seller Satisfaction Score, Customers Emotions can be visualized.

- Conclusion that can be drawn from the Dashboard Visualization are:

  - For the product _Alexa_ customers emotions were **mixed** i.e. joy, anger and sad. Based on the sentiments and emotions from the reviews and order delivery status, Watson Natural Language Understanding gave the highest seller satisfaction score of **3.38** for **seller3** which can be visualized by selecting Alexa and Seller3 as shown.
  ![visualize](doc/source/images/visualize3.png)

  - For the product _Batteries_ customers emotions were **joy**. Based on the sentiments and emotions from the reviews and order delivery status, Watson Natural Language Understanding gave the highest seller satisfaction score of **3.53** for **seller4** which can be visualized by selecting Batteries and Seller4 as shown.
  ![visualize](doc/source/images/visualize2.png)

  - For the product _Fire HD_ customers emotions were **mixed** i.e. joy, disgust and sad. Based on the sentiments and emotions from the reviews and order delivery status, Watson Natural Language Understanding gave the highest seller satisfaction score of **3.27** for **seller4** which can be visualized by selecting Fire HD and Seller4 as shown.
  ![visualize](doc/source/images/visualize4.png)

  - For the product _Kindle_ customers emotions were **joy**. Based on the sentiments and emotions from the reviews and order delivery status, Watson Natural Language Understanding gave the highest seller satisfaction score of **3.29** for **seller2** which can be visualized by selecting Batteries and Seller2 as shown.
  ![visualize](doc/source/images/visualize5.png)

  - For the product _Tablet 8in_ customers emotions were **mixed** i.e. joy, disgust and fear. Based on the sentiments and emotions from the reviews and order delivery status, Watson Natural Language Understanding gave the highest seller satisfaction score of **3.22** for **seller3** which can be visualized by selecting Tablet 8in and Seller3 as shown.
  ![visualize](doc/source/images/visualize6.png)

- Hence the following products can be brought from the following sellers.

  | Product | Seller to buy from | Seller Rating |
  |---------|--------------------|---------------|
  | Alexa   | Seller3 | 3.38 |
  | Batteries   | Seller4 | 3.53 |
  | Fire HD   | Seller4 | 3.27 |
  | Kindle   | Seller2 | 3.29 |
  | Tablet 8in   | Seller3 | 3.22|

- Further if you want to play around with the dashboard you can do so by reffering to the following tutorial.
  
  - <https://developer.ibm.com/tutorials/create-interactive-dashboards-on-watson-studio/>

<!--Add a section that explains to the reader what typical output looks like, include screenshots -->

## Sample output

![sample_output](doc/source/images/screenshot.gif)

<!-- keep this -->
## License

This code pattern is licensed under the Apache License, Version 2. Separate third-party code objects invoked within this code pattern are licensed by their respective providers pursuant to their own separate licenses. Contributions are subject to the [Developer Certificate of Origin, Version 1.1](https://developercertificate.org/) and the [Apache License, Version 2](https://www.apache.org/licenses/LICENSE-2.0.txt).

[Apache License FAQ](https://www.apache.org/foundation/license-faq.html#WhatDoesItMEAN)
