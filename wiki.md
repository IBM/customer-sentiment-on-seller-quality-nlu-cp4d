# Short Title

Customer Sentiment on seller quality with NLU on Cloud Pak for Data

# Long Title



# Author
* [Manoj Jahgirdar](https://www.linkedin.com/in/manoj-jahgirdar-6b5b33142/)
* [Smruthi Raj Mohan](https://www.linkedin.com/in/smruthi-raj-mohan-143088145/)
* [Srikanth Manne]()
* [Manjula Hosurmath](https://www.linkedin.com/in/manjula-g-hosurmath-0b47031)

# URLs

### Github repo

* https://github.com/IBM/customer-sentiment-on-seller-quality-nlu-cp4d/

# Summary


# Technologies

* [Analytics](https://developer.ibm.com/technologies/analytics/): Uncover insights with data collection, organization, and analysis.
* [Machine learning](https://developer.ibm.com/technologies/machine-learning/): Teach systems to learn without them being explicitly programmed.
* [Natural Language Understanding](https://developer.ibm.com/technologies/natural-language-processing/): Build apps that can interpret unstructured data and analyze insights.
* [Python](https://developer.ibm.com/technologies/python): An open-source interpreted high-level programming language for general-purpose programming.

# Description



# Flow

<!--add an image in this path-->
![architecture](doc/source/images/architecture.png)

<!--Optionally, add flow steps based on the architecture diagram-->

1. Create a connection for the refined data in db2 into IBM Watson Studio project in Cloud Pak for Data
2. Setup Jupyter Notebook that reads the dataset from the IBM db2 Connection
3. Run the Algorithm from Jupyter notebook that computes the seller rating with the help of Watson Natural Language Understanding on Cloud Pak for Data
4. Visualise insights from the data using Watson Embedded Dashboard on Cloud Pak for Data

# Instructions

> Find the detailed steps for this pattern in the [readme file](https://github.com/IBM/customer-sentiment-on-seller-quality-nlu-cp4d/blob/master/README.md)


# Components and services

* [IBM Natural Language Understanding](https://cloud.ibm.com/catalog/services/natural-language-understanding): Use advanced NLP to analyze text and extract meta-data from content such as concepts, entities, keywords, categories, sentiment, emotion, relations, and semantic roles.

* [IBM Watson Studio](https://cloud.ibm.com/catalog/services/watson-studio): Watson Studio democratizes machine learning and deep learning to accelerate infusion of AI in your business to drive innovation. Watson Studio provides a suite of tools and a collaborative environment for data scientists, developers and domain experts.

* [IBM Machine Learning](https://cloud.ibm.com/catalog/services/machine-learning): IBM Watson Machine Learning is a full-service IBM Cloud offering that makes it easy for developers and data scientists to work together to integrate predictive capabilities with their applications.
