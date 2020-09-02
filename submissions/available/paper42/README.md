# GenSlice

**GenSlice** is a generalized semantic history slicing framework which puts several history
slicing techniques (including [CSlicer](https://github.com/ntu-SRSLab/CSlicer) and Definer) 
developed over the years under a uniform lens
and provides a systematic approach for comparisons and analyses.

This artifact contains the replication package for the paper "GenSlice: Generalized Semantic History 
Slicing", and raw results from the experiments described in the paper.
The replication package can be obtained from: <https://github.com/Chenguang-Zhu/icsme20-artifact>.
The artifact is also freely accessible at a permanent DOI link: <https://doi.org/10.21979/N9/LPHCUS>.

#### Pre-requisites

There are two pre-requisites for running GenSlice artifact:  
1. Clone the Git repo of the artifact: https://github.com/Chenguang-Zhu/icsme20-artifact
2. Install docker version 19.03.12

#### 1. Directory Structures
```
📦 icsme20-artifact
 ┣ 📂 file-level
 ┃ ┣ 📂 buildscripts
 ┃ ┣ 📂 definer-configs
 ┃ ┣ 📂 example-poms
 ┃ ┣ 📂 orig-configs
 ┣ 📂 genslice
 ┃ ┣ 📜 cslicer-1.0.0-jar-with-dependencies.jar
 ┃ ┣ 📜 genslice.py
 ┃ ┣ 📜 glimpse.py
 ┃ ┣ 📜 split_commits.py
 ┃ ┗ 📜 update_paths.py
 ┣ 📜 Dockerfile
 ┣ 📜 LICENSE
 ┣ 📜 README.md
 ┣ 📜 clean.sh
 ┣ 📜 run_all.sh
 ┗ 📜 run_demo.sh
 ```

| Directories         | Descriptions                                                                        |
|---------------------|-------------------------------------------------------------------------------------|
| file-level          | Scripts and configuration files required by GenSlice, outputs are also written here |
| genslice            | GenSlice source code and CSlicer/Definer binary                                     |
| Dockerfile          | Dockerfile used to build an experimental environment with GenSlice installed        |
| run_all.sh          | Script for reproducing the full experiment                                          |
| run_demo.sh         | Script for running a demo case                                                      |

#### 2. Build Docker image

Assuming Docker is installed, run the following command at the root directory.

```bash
docker build -f Dockerfile -t genslice .
```

#### 3. Run demo case

We demonstrate the history slicing operator sequences on one example: CSV-159.  
Time estimation: ~20 mins on an Intel Core i7-8650U CPU @ 1.90GHz × 8 machine with 16 GB RAM.

```bash
docker run --name genslice-demo -i -t genslice --rm -v `pwd`:/Scratch
./run_demo.sh
```

This script executes all the seven optimal sequences (SD, SCD, CSD, DSD, CDSD, DSCD, CDSCD) and stores their semantic history slicing results in corresponding log files:  
- file-level/output/split-definer/CSV-159.log
- file-level/output/split-cslicer-definer/CSV-159.log
- file-level/output/cslicer-split-definer/CSV-159.log
- file-level/output/definer-split-definer/CSV-159.log
- file-level/output/cslicer-definer-split-definer/CSV-159.log
- file-level/output/definer-split-cslicer-definer/CSV-159.log
- file-level/output/cslicer-definer-split-cslicer-definer/CSV-159.log

The end of each log file looks like the following:

```text
[OUTPUT] |H*| = 2  
[STATS] ************** Stats **************  
[STATS] history.preprocess : 0.732  
[STATS] insert.edge : 0.0  
[STATS] total : 19.508  
[STATS] total.time : 20.59  
[STATS] test.run : 3.52  
[STATS] extract.time : 0.0  
[STATS] call.graphs : 0.212  
[STATS] hunk.fail : 2  
[STATS] pre.comp.fail : 14  
[STATS] test : 5  
[STATS] hstar.length : 2  
[STATS] iteration : 6  
[STATS] ***********************************  
[Split Exec Time]: 82.60289740562439  
[CSlicer Exec Time]: 29.742250204086304  
[Definer Exec Time]: 31.010393381118774  
[Total Exec Time]: 143.35554242134094  
Total Changed Lines: 81
```

The last line shows the size of the final history slice, measured in
number of changed (+/-) lines. For CSV-159, you will see that all the
seven log files have the same number: 81.

The result means that in this case, all seven optimal sequences yield
the same result, which is 1-minimal semantic history slice (RQ2).

#### 4. Reproduce full experiment results for all cases presented in the paper

Run all the sequences (RQ2 and RQ3) on all the 28 functionalities used in our experiment.
Time estimation: ~40.5 hours on an Intel Core i7-8650U CPU @ 1.90GHz × 8 machine with 16 GB RAM.

```bash
docker run --name genslice-all -i -t genslice --rm -v `pwd`:/Scratch
./run_all.sh
```

This script executes 13 sequences (C, D, SC, CD, DSC, CDSC, SD, SCD,
CSD, DSD, CDSD, DSCD, CDSCD) on all 28 functionalities and stores
their semantic history slicing results in corresponding log
files. Each log file has the same structure as the above example.

The full set of raw log files generated from our experiments are available at
<https://doi.org/10.21979/N9/LPHCUS> (`raw-results.tar`).

Some extra results are available on GenSlice website (<https://sites.google.com/view/genslice>).

If you would like to use GenSlice in your research, please cite our ICSME'20 paper.

```latex
@inproceedings{Zhu2020GGS,
  author = {Zhu, Chenguang and Li, Yi and Rubin, Julia and Chechik, Marsha},
  booktitle = {Proceedings of the 36th IEEE International Conference on Software Maintenance and Evolution (ICSME)},
  month = sep,
  title = {{GenSlice}: Generalized Semantic History Slicing},
  year = {2020}
}
```
