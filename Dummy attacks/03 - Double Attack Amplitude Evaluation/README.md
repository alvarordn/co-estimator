# Double Attack Amplitude Evaluation

This test case investigates the effects of launching **two simultaneous dummy false data injection attacks** targeting different measurements (e.g., real power *P*, reactive power *Q* or voltage *U*) at distinct locations in the system. Both attacks have the **same magnitude type** (e.g., both target *P*, or both target *Q*), but occur at different nodes. The amplitude of both attacks is varied systematically using predefined "bands" to assess how combined perturbations affect detectability and identification accuracy. This helps evaluate the robustness of bad data detection algorithms when facing coordinated, yet naive multi-point threats. The value of the hyper-parameter λ is modified across multiple scenarios to evaluate estimator performance under various conditions.

## Amplitude Band Description

In this test case, the amplitude of each attack is defined using predefined "bands". Each band corresponds to a specific range of percentage deviation from the original measurement value. There are 8 bands in total (numbered 0 through 7), where each number corresponds to a different level of perturbation intensity. The exact percentage ranges depend on the type of electrical magnitude being attacked (*P*/*Q* or *U*).

Below is a table summarizing the mapping between band numbers and percentage deviations:

| Band Number | *P* or *Q* Range (%) | *U* Range (%)     |
|-------------|-----------------------|--------------------|
| 0           | 80 – 85               | 98.0 – 98.5        |
| 1           | 85 – 90               | 98.5 – 99.0        |
| 2           | 90 – 95               | 99.0 – 99.5        |
| 3           | 95 – 100              | 99.5 – 100.0       |
| 4           | 100 – 105             | 100.0 – 100.5      |
| 5           | 105 – 110             | 100.5 – 101.0      |
| 6           | 110 – 115             | 101.0 – 101.5      |
| 7           | 115 – 120             | 101.5 – 102.0      |

The result files are named according to the format: `{mode}_{band1}_{band2}.json`, where `{band1}` and `{band2}` refer to the amplitude band of each individual attack, and `{mode}` specifies if it includes detection or identification results. For example, `identification_2_5.json` contains results for simulations where one attack was injected using band 2 and the other using band 5 and the results gathered are those of identification scenarios.

## `.json` File Structure

The result files have a `.json` extension and are divided into two types: **detection** and **identification**. Detection files are prefixed with the word `detection` and indicate, out of the total number of simulations performed, in which of them a cyberattack was detected, without specifying the exact measurement or set of measurements attacked. Identification files are prefixed with `identification` and include various performance metrics that evaluate the accuracy of attack identification. These metrics are described in detail below.

The `.json` file is structured as a nested dictionary with the following hierarchy:

- **First-level key**: Power factor (`090neg`, `090pos`, `100pos`)
- **Second-level key**: Time instant (`08`, `10`, `13`)
- **Third-level key**: Lambda value — a set of `50` values uniformly distributed in the interval `[0.01, 10]`
- **Fourth-level key**: Electrical magnitude attacked (`P`, `Q`, or `U`)
- **Fifth-level**: A dictionary containing:
  - **Detection records** (for detection files):
    - `Detection`: List indicating for each simulation if the attack has been detected (`true`) or not (`false`).
  - **Identification metrics** (for identification files):
    - `0`: Scenarios in which the attack has been correctly detected.
    - `1`: Scenarios in which the attack has been detected but at least one healthy measurement was incorrectly flagged.
    - `2`: Scenarios in which the attack has not been detected.
    - `3`: Scenarios in which a healthy measurement was falsely identified as attacked.
    - `Precision`: Average precision across all simulations.
    - `Recall`: Average recall across all simulations.
    - `Accuracy`: Average accuracy across all simulations.

Note that the **F1-score** can be derived from precision and recall. For each combination of power factor, time instant, lambda value, and electrical magnitude, **1,000 simulations** have been conducted. Each simulation involves a random selection of measurements modified by the attack. In total, the results presented here are based on **1,350,000 simulation runs**.

## Naming Convention for Figures

The figures in this folder follow a structured naming convention to clearly identify the content of each plot. The filename format is:\
`<Mode>` _ `<Magnitude>` _ `<PowerFactor>`.pdf\
where:

- **`<Mode>`**: Either `detection` or `identification`.
- **`<Magnitude>`**: The type of electrical magnitude that was attacked (`U` for voltage, `P` for active power, and `Q` for reactive power).
- **`<PowerFactor>`**: The power factor used during the simulation (`090neg`, `090pos`, or `100pos`).

This naming system allows for easy categorization and retrieval of results based on the attack type and simulation parameters.
