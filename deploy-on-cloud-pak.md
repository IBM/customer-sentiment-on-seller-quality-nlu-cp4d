# Deploy on Cloud Pak for Data

## Steps

1. [Download the Dataset](#1-download-the-dataset)
2. [Create a Watson Natural Language Understanding Service](#2-create-a-watson-natural-language-understanding-service)
3. [Create a Project](#3-create-a-project) **_(Already completed as a part of the Tutorial)_**
4. [Add Db2 Connection to the Project](#4-add-db2-connection-to-the-project) **_(Already completed as a part of the Tutorial)_**
5. [Prepare and Run the Jupyter Notebook](#5-prepare-and-run-the-jupyter-notebook)
6. [Create Embedded Dashboard Service](#6-create-ibm-streaming-analytics-service)
7. [Visualize the Dashboard](#7-visualize-the-dashboard)

### 1. Download the Dataset
In this Code Pattern we are going to use **Customised version of Brazilian E-Commerce Public Dataset by Olist** that we created in the Tutorial [Prepare your Dataset for your ML Models using Data Refinery from Db2](https://github.com/IBM/prepare-your-dataset-using-data-refinery-from-db2-cp4d).

We are also going to use **Consumer Reviews of Amazon Products** from Kaggle. Download the dataset from the link below.

- https://www.kaggle.com/datafiniti/consumer-reviews-of-amazon-products

After Downloading, Extract the `consumer-reviews-of-amazon-products.zip` file.

We’ll be using the following files:

[Datafiniti_Amazon_Consumer_Reviews_of_Amazon_Products_May19.csv]() : This dataset is a list of over 28,000 consumer reviews for Amazon products like the Kindle, Fire TV Stick, and more from Datafiniti's Product Database updated between February 2019 and April 2019.

As we don’t have a proper dataset with product reviews and product delivery status, we are cooking up the dataset by _assuming_ 
that the products from the **Customised version of Brazilian E-Commerce Public Dataset by Olist** and the **Consumer Reviews of Amazon Products** are the same.

### 2. Create a Watson Natural Language Understanding Service

We will be using Watson Natural Language Understanding service to read the comments of the customer and analyse the Sentiment and Emotions of the Customers review.

* Create a [Watson Natural Language Understanding](https://cloud.ibm.com/catalog/services/natural-language-understanding) service on IBM Cloud.

* Once the service is created copy the **API Key** and **URL** of the service as shown. 

![nluCredentials](doc/source/images/nluCredentials2.png) 

**NOTE: These credentials are important as it will be used in [step 5](#5-prepare-and-run-the-jupyter-notebook)**

### 3. Create a Project  _(You will have already completed this step as a part of the Tutorial, use the same project)_

* Create a Project in Cloud Pak for Data choose an Empty Project.

![createProject](doc/source/images/emptyProject.png)

* Once The Project is Created you will see the below page.

![projectDashboard](doc/source/images/projectDashboard.png)

### 4. Add Db2 Connection to the Project _(You will have already completed this step as a part of the Tutorial, use the same project)_

Now that we have created a project, we will start adding components to our project. We will start by adding Db2 Connection to our project first.

* Click on **Add to Project** and select **Connection**. If you have followed [step 2](#2-load-the-data-into-tables-in-db2) select **Db2** from the list and add the credentials of your provisioned Db2 Instance. If you have a different database then you can select that and fill in the credentials.

![gif](doc/source/images/create_connection.gif)

* After filling the credentials click on **Test Connection** to make sure you have entered correct credentials. Finally select **Create**.

![connection](doc/source/images/connImage.png)

**NOTE: The Database Credentials will be provided by your Database administrator. If you have provisioned a Db2 instance on Cloud Pak for Data then you can follow the steps [here](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/create-db.html#create-db) to get the credentials.**

### 5. Prepare and Run the Jupyter Notebook

We have successfully created a project and added Db2 Connection to our project. We will now add the required credentials to our python Jupyter notebook and run the notebook.

#### 5.1. Prepare the Notebook
* Add Jupyter notebook to the Project by clicking on **Add to Project** and select **Notebook**. Click on **New Notebook from URL** and paste the below URL and create a Notebook.
  - [https://github.com/IBM/customer-sentiment-on-seller-quality-nlu-cp4d/blob/master/notebook/customer-sentiment-on-seller.ipynb](https://github.com/IBM/customer-sentiment-on-seller-quality-nlu-cp4d/blob/master/notebook/customer-sentiment-on-seller.ipynb)

![createJupyterNotebook](doc/source/images/createJupyterNbCp4d.gif)

* Once the notebook is created we will have to fill in 4 Cells with the following: 
  - Watson Natural Language Understanding Credentials
  - Upload the Consumer Reviews of Amazon Products dataset and insert Pandas Dataframe
  - Insert the Customised version of Brazilian E-Commerce Public Dataset by Olist from Db2
  - Insert Db2 Credentials into the Notebook
 
##### 5.1.1. Watson Natural Language Understanding Credentials
* Insert the credentials copied from [step 2](#2-create-a-watson-natural-language-understanding-service) in the cell shown below.

![nluCredentials](doc/source/images/nluCredentials.png)

##### 5.1.2. Upload the Consumer Reviews of Amazon Products dataset and insert Pandas Dataframe

* Click on the **Assets** tab, and select **browse**, from the file uploader select the extracted file from [step 1](#1-download-the-dataset) named **Datafiniti_Amazon_Consumer_Reviews_of_Amazon_Products_May19.csv** from the **Consumer Reviews of Amazon Products**.

![uploadDataset](doc/source/images/uploadDatasetCp4d.gif) 

* Once the Dataset is uploaded, click on the cell which says _"Insert Customer Review Dataset here"_, click on **`Insert to code > Insert Pandas Dataframe`**. You will see the code to read the dataset in the cell. 

* Finally replace the variable name to **data** as shown.

![insertPandasDf](doc/source/images/insertPandasDfCp4d.gif)

##### 5.1.3. Insert the Customised version of Brazilian E-Commerce Public Dataset by Olist from Db2

* Select the cell which says _"Insert Customer Order Details Dataset here"_, click on **Connections** in the assets tab and select **`Insert to code > Insert Pandas Dataframe`** from your Db2 Connection variable. Select the Schema of your table and choose **DERIVEDDATA** and click on _Select_.

>NOTE: If you have used Db2 Instance then the schema name is your _Username_.

* Once the credentials are inserted, replace the variable name to **data2** as shown.

![insertPandasDf](doc/source/images/insertPandasDfForDBCp4d.gif)

##### 5.1.4. Insert Db2 Credentials into the Notebook

* Select the cell which says _"Insert Db2 Connection Credentials here"_, click on **Connections** in the assets tab and select **`Insert to code > Insert Credentials`** from your Db2 Connection variable.

* Once the credentials are inserted, replace the variable name to **`credentials_1`** as shown.

![insertDbCredentials](doc/source/images/insertDbCredentialsCp4d.gif) 

#### 5.2. Run the Notebook

After all the Preperations are done, we will run the Jupyter Notebook by Clicking on **`Cell > Run All`** as shown.

![runAllCells](doc/source/images/runAllCellscp4d.png)

**NOTE: It will take around 25 Min - 30 Min to complete the execution of entire notebook, please be Patient!**

### 6. Create Embedded Dashboard Service
### 7. Visualize the Dashboard
