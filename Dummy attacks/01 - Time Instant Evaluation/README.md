# Time Instant Evaluation

This test case evaluates how the timing of the dummy attack affects the performance of detection and identification mechanisms. Since the power output of the PV plant varies over time depending on environmental conditions (e.g., irradiance), the impact of launching an attack at different operational states of the system is analyzed. Additionally, the tuning parameter (λ) of the Huber estimator is optimized to improve robustness under these time-varying conditions.

## `.json` File Structure

The result files have a `.json` extension and are divided into two types: **detection** and **identification**. Detection files are prefixed with the word `detection` and indicate, out of the total number of simulations performed, in which of them a cyberattack was detected, without specifying the exact measurement or set of measurements attacked. Identification files are prefixed with `identification` and include various performance metrics that evaluate the accuracy of attack identification. These metrics are described in detail below.

The `.json` file is structured as a nested dictionary with the following hierarchy:

- **First-level key**: Power factor (`090neg`, `090pos`, `100pos`)
- **Second-level key**: Time instant (`08`, `10`, `13`)
- **Third-level key**: Lambda value — a set of `50` values uniformly distributed in the interval `[0.01, 10]`
- **Fourth-level key**: Electrical magnitude attacked (`P`, `Q`, or `U`)
- **Fifth-level**: A dictionary containing:
  - **Detection records** (for detection files):
    - `Detection`: List indicating for each ismulation if the attack has been detected (`true`) or not (`false`).
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
- **`<Magnitude>`**: In the case of identification results, it refers to the type of electrical magnitude that was attacked (`U` for voltage, `P` for active power, and `Q` for reactive power).
- **`<PowerFactor>`**: The power factor used during the simulation (`090neg`, `090pos`, or `100pos`).

This naming system allows for easy categorization and retrieval of results based on the attack type and simulation parameters.

