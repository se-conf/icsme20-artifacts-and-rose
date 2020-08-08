# How to reproduce

A reproduction is possible for everything except for the manually validated data contained in the SmartSHARK MongoDB dump. However, due to the time constraints we provide intermediate data at every step.
**To reproduce the JIT models and results in the paper, the first two steps can be skipped.**


## Reproduce SmartSHARK mining

The data from the MongoDB dump can be reproduced via SmartSHARK. The data we use can be reproduced with the [serverSHARK](https://github.com/smartshark/serverSHARK) orchestration tool with the following plugins [vcsSHARK](https://github.com/smartshark/vcsSHARK), [mecoSHARK](https://github.com/smartshark/mecoSHARK), [rMineSHARK](https://github.com/smartshark/rMineSHARK), [issueSHARK](https://github.com/smartshark/issueSHARK), [linkSHARK](https://github.com/smartshark/linkSHARK), [labelSHARK](https://github.com/smartshark/labelSHARK) and [inducingSHARK](https://github.com/smartshark/inducingSHARK). Additionally the links between issues and commits as well as the issue types can be validated via a visualization frontend [visualSHARK](https://github.com/smartshark/visualSHARK).

This is the most time consuming process, we provide a SmartSHARK MongoDB dump that can be used to skip this step.


## Reproduce JIT mining data
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

After extracting the repositories the mining can be started.
Every project has to be extracted like that.

```bash
cd Gierlappen
source bin/activate

python smartshark_mining.py --project PROJECT_NAME --path PATH_TO_REPOSITORY --file-check --label-name JLMIV+R --db-host SMARTSHARK_MONGODB_HOST --db-port SMARTSHARK_MONGODB_PORT --db-name SMARTSHARK_MONGODB_DATABASE --db-user SMARTSHARK_MONGODB_USER --db-pw SMARTSHARK_MONGODB_PASSWORD --db-auth SMARTSHARK_MONGODB_AUTHENTICATION_SOURCE
```


## Reproduce models used in the paper

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

To create and evaluate the models the TrainTest.ipynb and Interval.ipynb are needed. For RQ1 the Correlation


## Reproduce figures used in the paper

The replication kit already contains calculated model data, if only the figures should be reproduced the mining data is not necessary and only the TrainTestEval.ipynb and IntervalEval.ipynb notebooks are necessary.

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