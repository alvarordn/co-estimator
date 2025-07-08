# co-estimator

This repository contains the results of the power systems state estimation developed by USE for the **COCOON** European project.

## Repository Structure

The code and results are organized into multiple folders, each representing a specific test case or scenario. Each folder follows a consistent internal structure:
/test_case_name\
│\
├── data/ # JSON files containing results from simulation tests\
├── figs/ # Graphical representations (plots, charts, etc.) of the test results\
└── README.md # Interpretation and explanation of the test case and its results


### `data/` Folder
Contains `.json` files with the output data generated from the simulations. These files can be used for further analysis or validation.

### `figs/` Folder
Includes visualizations of the simulation results in image format (PDF). These plots help in understanding trends, anomalies, and overall system behavior.

### `README.md`
Each test case includes its own `README.md` file, offering an interpretation of the simulation, key findings, and any relevant notes for understanding the results.

All test cases are analyzed from two perspectives: **detection** and **identification**. 

- In the **detection** phase, the focus is on determining whether a cyberattack has occurred or not. This involves evaluating the system's ability to distinguish between normal operation and compromised scenarios.

- In the **identification** phase, the objective is to identify which specific measurement(s) have been manipulated by the attacker. This allows for a deeper understanding of the attack vector and its impact on the system.

For both aspects, relevant metrics are provided that quantify the performance of the detection and identification processes, as well as their effects on the accuracy of the state estimation.