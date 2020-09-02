# How to reproduce

A reproduction is possible for everything except for the manually validated data contained in the SmartSHARK MongoDB dump. However, due to the time constraints we provide intermediate data at every step.
**To reproduce the JIT models and results in the paper, the first two steps can be skipped.**

## 0. System Requirements

- Git
- Python 3.6
- MongoDB 4.0 (only for the optional steps 1&2)

The replication of the results of the paper from the processed raw data requires only Python 3.6 and Git and should not be problematic without virtualization.

The full replication starting from the raw results cannot be reasonable performed using a single virtual machine/container, due to the large amount of data required and the computational effort involved. Therefore, we opted not to provide a virtual image for this part, but rather describe how an execution environment can be configured.


## 1. Reproduce SmartSHARK mining (Optional)

The data from the MongoDB dump can be reproduced via SmartSHARK. The data we use can be reproduced with the [serverSHARK](https://github.com/smartshark/serverSHARK) orchestration tool with the following plugins [vcsSHARK](https://github.com/smartshark/vcsSHARK), [mecoSHARK](https://github.com/smartshark/mecoSHARK), [rMineSHARK](https://github.com/smartshark/rMineSHARK), [issueSHARK](https://github.com/smartshark/issueSHARK), [linkSHARK](https://github.com/smartshark/linkSHARK), [labelSHARK](https://github.com/smartshark/labelSHARK) and [inducingSHARK](https://github.com/smartshark/inducingSHARK). Additionally the links between issues and commits as well as the issue types can be validated via a visualization frontend [visualSHARK](https://github.com/smartshark/visualSHARK).

The data collection process for the raw data is described in greater detail in [this paper](https://arxiv.org/abs/1911.08938). This raw data collection requires many CPU years for the collection of the metric data and PMD warnings for each commit in a repository. Moreover, manual validation of issue links and issue types must be performed for the full replication, which requires multiple months of manual data analysis by researchers. Therefore, we strongly recommend to download the dump of the MongoDB we provide (see Step 2). 


## 2. Reproduce JIT mining data (Optional)

To reproduce the JIT mining process the SmartSHARK MongoDB needs to be accessible for the mining tool. The dump is rather large and this may take some time.

```bash
wget https://user.informatik.uni-goettingen.de/~sherbol/replicationkits/replication-kit-emse-2020-defect-prediction-data/smartshark-mongodb-rel1.gz

mongorestore smartshark-mongodb-rel1.gz
```

After restoring the MongoDB the mining tool can be installed.

```bash
git clone https://github.com/atrautsch/Gierlappen
cd Gierlappen

# create venv and install requirements
python -m venv .
source bin/activate
pip install -r requirements.txt
```

A local snapshot of the git repository of each project is required. They need to be extracted from the GridFS contained in the MongoDB snapshot.
We provide a get_repositories.py that extracts the repositories, although it needs the host, port and credentials for the MongoDB first.

```bash
cd Gierlappen
source bin/activate

# configure mongodb access and local folder
vim get_repositories.py

# extract git snapshots
python get_repositories.py
```

After extracting the repositories the mining can be started. Every project has to be extracted like that. Please note that the command below must be modified with the correct credentials. 

```bash
cd Gierlappen
source bin/activate

python smartshark_mining.py --project PROJECT_NAME --path PATH_TO_REPOSITORY --file-check --label-name JLMIV+R --db-host SMARTSHARK_MONGODB_HOST --db-port SMARTSHARK_MONGODB_PORT --db-name SMARTSHARK_MONGODB_DATABASE --db-user SMARTSHARK_MONGODB_USER --db-pw SMARTSHARK_MONGODB_PASSWORD --db-auth SMARTSHARK_MONGODB_AUTHENTICATION_SOURCE
```


## 3. Reproduce models used in the paper

As reproducing the mining step is time and resource intensive we provide the mining results as CSV files [here](https://hdl.handle.net/21.11101/0000-0007-E7D1-8). They are sufficient to reproduce the models created and evaluated in the paper.

Install the replication kit and its dependencies.
```bash
git clone https://github.com/atrautsch/icsme2020_replication
cd icsme2020_replication

# create venv and install requirements
python -m venv .
source bin/activate
pip install -r requirements.txt
```

Fetch the raw mining data.
```bash
cd data
wget https://user.informatik.uni-goettingen.de/~trautsch2/icsme2020_mining_data.zip
unzip icsme2020_mining_data.zip
```

Run the Jupyter notebooks.

```bash
source bin/activate
cd notebooks
jupyter lab
```

To create and evaluate the models the TrainTest.ipynb and Interval.ipynb are needed. For RQ1 the Correlation.iypynb.


## 4. Reproduce figures used in the paper

The replication kit already contains calculated model data, if only the figures should be reproduced the mining data is not necessary and only the TrainTestEval.ipynb and IntervalEval.ipynb notebooks are necessary.
Running these produces the plots in the paper. They are saved in the figures folder.

```bash
git clone https://github.com/atrautsch/icsme2020_replication
cd icsme2020_replication

# create venv and install requirements
python -m venv .
source bin/activate
pip install -r requirements.txt
```

```bash
source bin/activate
cd notebooks
jupyter lab
```
