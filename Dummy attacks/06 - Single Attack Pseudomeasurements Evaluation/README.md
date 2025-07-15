# Single Attack Considering Pseudomeasurements Evaluation

This test case investigates the impact of **including pseudomeasurements** in the state estimation process, particularly in **Medium Voltage (MV) feeders**, where real measurements may be sparse or unavailable. The evaluation focuses on how different data configurations affect the detection and identification performance of a **single false data injection attack**.

Three scenarios are considered:
1. **With measurements**: Real measurements are available and used in the MV feeders (`withMV`).
2. **Without measurements**: No measurements are assumed to be present in the MV feeders (`woMV`).
3. **With pseudomeasurements**: Active power pseudomeasurements are generated for the MV feeders based on aggregated information from downstream nodes (bottom-up) and upstream nodes (top-down)  (`withPSM`).

The goal is to evaluate whether the inclusion of pseudomeasurements improves estimator robustness and bad data detection capabilities under attack conditions.

The value of the hyper-parameter λ is fixed at **2.5**, based on results from previous simulations. 
## Amplitude Band Description

In this test case, each attack is injected using one of eight predefined amplitude bands. Each band corresponds to a specific percentage deviation from the original measurement value, depending on the type of electrical magnitude being attacked (*P*/*Q* or *U*).

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

The result files are named according to the format: `{mode}_{scenario}_{band}.json`, where `{mode}` refers to identification or detection results, {scenario} refers to the availability of measurements in the MV feeders and `{band}` refers to the amplitude band used for the single attack. For example, `identification_withMV_5.json` contains results for simulations where the attack was injected using band 5 and considering measurements in the MV feeders.

## `.json` File Structure

The result files have a `.json` extension and are divided into two types: **detection** and **identification**. Detection files are prefixed with the word `detection` and indicate, out of the total number of simulations performed, in which of them a cyberattack was detected, without specifying the exact measurement or set of measurements attacked. Identification files are prefixed with `identification` and include various performance metrics that evaluate the accuracy of attack identification. These metrics are described in detail below.

The `.json` file is structured as a nested dictionary with the following hierarchy:

- **First-level key**: Power factor (`090neg`, `090pos`, `100pos`)
- **Second-level key**: Time instant (`08`, `10`, `13`) 
- **Third-level key**: Electrical magnitudes attacked (`P`, `Q`, `U` or `I`)
- **Fourth-level**: A dictionary containing:
  - **Detection records** (for detection files):
    - `Detection`: List indicating for each simulation if the attack has been detected (`true`) or not (`false`).
  - **Identification metrics** (for identification files):
    - `Precision`: Average precision across all simulations.
    - `Recall`: Average recall across all simulations.
    - `Accuracy`: Average accuracy across all simulations.
    - `F1`: Average F1-score across all simulations.
    - `norm2`: Root mean square difference between real state and tool state estimation.
    - `normInf`: Maximum difference between real state and tool state estimation.
    - `z`: Root mean square difference between unmodified measurements and tool estimates.


For each combination of power factor, time instant, electrical magnitude attacked and mode, **100 simulations** have been conducted. Each simulation involves a random selection of a single measurement modified by the attack. In total, the results presented here are based on **10,800 simulation runs**.

## Naming Convention for Figures

The figures in this folder follow a structured naming convention to clearly identify the content of each plot. The filename format is:  
`<Mode>` _ `<PowerFactor>` _ `<Magnitude>.pdf`  

where:

- **`<Mode>`**: Either `detection` or `identification`.
- **`<PowerFactor>`**: The power factor used during the simulation (`090neg`, `090pos`, or `100pos`).
- **`<Magnitude>`**: In the case of identification results, the type of electrical magnitude that was attacked (`U` for voltage, `P` for active power, `I` for current, and `Q` for reactive power).

This naming system allows for easy categorization and retrieval of results based on the attack type, simulation parameters, and data availability scenario.