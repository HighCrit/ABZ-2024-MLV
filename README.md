# Introduction
[ABZ](https://abz-conf.org) is a yearly conference with a case study on the topic of Formal Analysis. This repository contains an attempt at modelling the [2024's case study](https://abz-conf.org/site/2024/casestudy/) ([GitHub](https://github.com/foselab/abz2024_casestudy_MLV)) regarding the Mechanical Lung Ventilator (MLV) in [mCRL2](https://mcrl2.org). Which was done as a part of a course for my Masters. The model in this repository mainly concerns itself with the Controller's communication with the sensors and valves. The behaviour of which has been verified using modal mu-calculus formulas that can be found in the properties directory in the root.

# Building & Verifying
In order to run the verification of the model, one needs to have the [mCRL2](https://mcrl2.org) tool-set installed. After which the following command can be run to convert the model into a Linear Process Specification (LPS).
```sh
mcrl22lps ./mlv_single_cycle.mcrl2 mlv_single_cycle.lps
```
Then, to convert this to a Labelled Transition System (LTS) the following command needs to be executed:
```sh
lps2lts mlv_single_cycle.lps mlv_single_cycle.lts
```
Optionally, the following arguments can be provided `--threads=n` to construct the LTS using multiple threads, and `--verbose` to periodically print information in the console.

Finally, the following command will verify the model using a formula specified by `<formula_path>` in:
```sh
lts2pbes -f <formula path> mlv_single_cycle.lts | pbes2bool
```

# Additional Options
The generated LTS from the previous section can be reduced modulo strong bisimularity by running:
```sh
ltsconvert -ebisim mlv_single_cycle.lts mlv_single_cycle.bisim.lts
```
To get general information regarding the LTS, the following command can be run to get, among other things, the amount of states, actions, and transitions. 
```sh
ltsinfo mlv_single_cycle.lts
```
