# End-To-End Timing Analysis and Optimization of Multi-Executor ROS 2 Systems

The repository is used to reproduce the evaluation from

*End-To-End Timing Analysis and Optimization of Multi-Executor ROS 2 Systems*

for RTAS 2024.

To replicate the experiment in the paper, please follow the instructions below, depending on whether you use the provided VM or install the required packages manually.

This document is organized as follows:
<!-- - [End-To-End Timing Analysis](#end-to-end-timing-analysis)
  - [How to use VM](#how-to-use-vm)
  - [Experiment Overview](#experiment-overview)
    - [How to run the experiments](#how-to-run-the-experiments)
    - [ROS2 system execution](#ros2-system-execution)
      - [Case Study](#case-study)
      - [Evaluation](#evaluation)
    - [ROS2 system simulation and upper bound analysis](#ros2-system-simulation-and-upper-bound-analysis)
      - [Case Study](#case-study-1)
      - [Evaluation](#evaluation-1)
    - [File Structure](#file-structure)
    - [Overview of the corresponding functions and algorithms](#overview-of-the-corresponding-functions-and-algorithms)
  - [Environment Setup](#environment-setup)
    - [Requirements](#requirements)
    - [Deployment](#deployment)
    - [System and run time details](#system-and-run-time-details)
  - [Miscellaneous](#miscellaneous)
    - [Authors](#authors)
    - [Acknowledgments](#acknowledgments) -->

## How to setup the VM

- Please download the [zip file](https://tu-dortmund.sciebo.de/s/1S6foIpL1Mhk9L5), which contains the virtual disk and the machine description.

- The credentials are: ros2end2end/rtas2024 (user/password).

- Start a terminal (Press CTRL+Shift+T) and run the following command:

```
./initialize.sh
```

- Follow the instructions in [Gurobi Installation](#gurobi-installation).

## How to setup the packages

- Start a terminal (Press CTRL+Shift+T) and run the following commands:

  ```
  git clone https://github.com/HarunTeper/ros2-end-to-end-distributed.git
  sudo apt -y install python3-pip
  pip install gurobipy
  ```

- Follow the instructions in [Gurobi Installation](#gurobi-installation).

## Gurobi Installation

These instructions are based on the state of the 15.02.2024 of the Gurobi webpage. For this evaluation, Gurobi 10.0.3 is required.

- Go the the following page: https://www.gurobi.com/.

- Register a new account if you do not already have one.

- Log in to your account.

- You should now be on your user home page https://portal.gurobi.com/iam/home.

- Request a license. For example, press the **Request a free academic license** button (https://www.gurobi.com/academia/academic-program-and-licenses/).

- Choose an **Academic Named-User License** and click on **Learn More**.

- Follow the steps described on the website (https://www.gurobi.com/features/academic-named-user-license/).

  - The following website provides a complete guide for the setup (https://support.gurobi.com/hc/en-us/articles/4534161999889-How-do-I-install-Gurobi-Optimizer).

  - Click the **Download Gurobi Optimizer** button and accept the EULA.

  - Download Gurobi 10.0.3, which is an older version and can be found below the current version of Gurobi 11.0.0.

  - Download the installer for your respective operating system. For the VM, it is the **gurobi10.0.3_linux64.tar.gz** file.

  - Extract the gurobi folder that is in your *Downloads* folder into your home directory.

  -  Set the paths of **GUROBI_HOME**, **PATH**, and **LD_LIBRARY_PATH**. A detailed description can be found here https://support.gurobi.com/hc/en-us/articles/13443862111761-How-do-I-set-system-environment-variables-for-Gurobi. Please note that this description may be based on an older version, and you may need to change the folder names according to the downloaded files.

  - For the VM, the following commands works for our configuration of the .bashrc:

    ```
    export GUROBI_HOME="/home/osboxes/gurobi1003/linux64"
    export PATH="${PATH}_${GUROBI_HOME}/bin"
    export LD_LIBRARY_PATH="${GUROBI_HOME}/lib"
    ```

- Revisit the page https://portal.gurobi.com/iam/home.

- Click on **Licenses**.

- Click on **Request** next to **Licenses**.

- Request a **Named-User Academic** license.

- Agree to the End User License Agreement.

- Click on **Confirm Request**.

- Click to copy the command **grbgetkey** including the key that is displayed.

- Open a terminal, copy and enter the command into the terminal. Accept any prompts that come up during this setup.

- To test the gurobi installation, open a terminal and run the following command:

  ```
  gurobi.sh
  ```

  If this command lists the configuration of your installation and opens a gurobi terminal, the installation is successful, and you may proceed to run the experiment.

## Experiment Overview
    
The experiment involves running the optimization of the evaluation.
Specifically, we provide a script that calculates the upper bound values (UB) of our system. The reference values can be found in the rightmost column in the table of our evaluation, and are as follows:

| Configuration | UB |
|---|---|
| DDS | - |
| Timer Periods | - |
| Policy | - |
| Assignment | - |
| Fix-Async | - |
| Fix-Sync | - |
| Fix-Assign | - |
| Baseline | - |

### How to run the experiments

Open a terminal and move to the folder of this repository.

Run the following command:

```
python3 main.py
```

After the script finished, the results are shown in the terminal.

From our experience, running the optimization requires less than one minute of computation.

### File Structure

    ros2-end-to-end-distributed
    ├── 
    │    
    └──
### Overview of the corresponding functions and algorithms

The file optimization.py corresponds to the optimization implementation and it includes comments that reference to the corresponding lemmas of the paper.

### System and run time details

As a reference, we utilize a machine running Ubuntu 22.04, with an AMD Ryzen 5900 12-Core Processor (12 Cores, 24 Threads) with 3,7GHz and 32GB RAM.

For the virtual machine, we enabled 4 cores and 4096 MB of RAM.

### Authors

* Harun Teper
* Tobias Betz
* Mario Günzel
* Dominic Ebner
* Georg von der Brüggen
* Johannes Betz
* Jian-Jia Chen

### Acknowledgments

This work has been supported by the Federal Ministry of Education
and Research (BMBF) in the course of the project 6GEM under
the funding reference 16KISK038.