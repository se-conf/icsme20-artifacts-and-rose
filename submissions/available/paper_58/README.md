A complete replication is rather complicated because we have a long chain of tools and resulting data that is aggregated/computed at each step.
Nevertheless, we describe the complete chain here and in INSTALL.md and provide intermediate results.

# Repository Mining

Parts of the raw data (static source code metrics, static analysis warnings, bug-reports as well as links between bug-reports and commits) were collected via the [SmartSHARK](https://smartshark.github.io) infrastructure.
The data also contains manually validated bug-report to commit links and bug-report types. This data is the result of a multi-year effort on our part to provide extensive and interlinked data for software engineering research.

SmartSHARK collects the data into a MongoDB, a dump of it is available [here](https://hdl.handle.net/21.11101/0000-0007-D827-A).


# Fine-grained just-in-time defect prediction data mining

To include fine-grained just-in-time defect prediction features and to traverse the commit graph while maximizing the available data by traversing every branch and keeping track of file states we use [Gierlappen](https://github.com/atrautsch/Gierlappen).
It utilizes the SmartSHARK MongoDB as well as a local checkout of the repository. The SmartSHARK MongoDB provides a git snapshot of the repository at the time the data was collected which we use.

The results of this mining process are available [here](https://hdl.handle.net/21.11101/0000-0007-E7D1-8). We provide the results directly because extracting the data takes about a week.


# Building and evaluating fine-grained just-in-time defect prediction models

This is part of the basic replication kit currently on [Github](https://github.com/atrautsch/icsme2020_replication). We provide jupyter notebooks that use the raw mining data created in the previous step (this takes about ~24h) to build and evaluate the defect prediction models.
Additionally, we provide the results as CSV as they are small enough. They can also be used to just reproduce the plots and values used in the paper.
