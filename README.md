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
- Any Database. In this Code Pattern we demonstrate using [Db2 on Cloud Pak for Data](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/cpd/svc/db2z/create_database_db2z.html)

# Steps
## Deploy to IBM Cloud

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
