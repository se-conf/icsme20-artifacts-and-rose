# Artifact for "Static source code metrics and static analysis warnings for fine-grained just-in-time defect prediction"

We describe how the results of our work can be replicated. We note that the complete replication of results starting from the raw data is very time consuming, due to the many tools required and the large amount of raw data required. Therefore, we also provide the pre-processed data. This data is provided as the replication kit on [Github](https://github.com/atrautsch/icsme2020_replication), including all analysis scripts. Using the replication kit on  with the supplied data is sufficient to replicate all results presented in the paper. 

## Raw Repository Data

Our analysis is based on raw data that we collected with [SmartSHARK](https://smartshark.github.io). The data is available in a MongoDB. A dump of the MongoDB is available [here](https://hdl.handle.net/21.11101/0000-0007-D827-A). 

The raw data was collected as part of our work on [this paper](https://arxiv.org/abs/1911.08938).

## Fine-grained just-in-time defect prediction data mining

To include fine-grained just-in-time defect prediction features and to traverse the commit graph while maximizing the available data by traversing every branch and keeping track of file states we use [Gierlappen](https://github.com/atrautsch/Gierlappen).
Gierlappen utilizes the SmartSHARK MongoDB as well as a local checkout of the repository. The SmartSHARK MongoDB provides a git clone of the repository at the time the data was collected which we use to ensure consistency between the raw data and the git clone. 

The results of this mining process are available [here](https://hdl.handle.net/21.11101/0000-0007-E7D1-8). We provide the results directly because extracting the data takes about a week. All analysis in the paper are performed using this pre-processed data. 


## Building and evaluating fine-grained just-in-time defect prediction models

This is part of the basic replication kit currently on [Github](https://github.com/atrautsch/icsme2020_replication). We provide jupyter notebooks that use the raw mining data created in the previous step (this takes about ~24h) to build and evaluate the defect prediction models. Additionally, we provide the results as CSV as they are small enough. They can also be used to just reproduce the plots and values used in the paper.
