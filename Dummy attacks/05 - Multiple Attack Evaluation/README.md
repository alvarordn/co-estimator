# Multiple Attack Evaluation

This test case investigates the effects of launching **several simultaneous dummy false data injection attacks** targeting **different types of electrical magnitudes** (e.g., real power *P*, reactive power *Q*, or voltage *U*) at the same or different nodes in the system. Each attack affects a distinct measurement type, allowing us to assess how mixed-signal manipulation impacts detection and identification performance. The amplitude of both attacks is varied systematically using predefined "bands" to evaluate how combined perturbations affect estimator robustness. This helps determine the sensitivity of bad data detection algorithms when facing naive but multi-dimensional cyber threats.

The time instant is fixed at 10:00 AM, and the value of the hyper-parameter λ is set to 2.5, based on results from previous simulations. In contrast to earlier scenarios where each attack was assigned to a specific band independently, this version evaluates the impact of attacks over **randomly selected measurements**, with the **number of attacked measurements as a variable**.

## Amplitude Band Description

In this test case, only **two amplitude bands** are considered for the attack injections:

- **Band A**: ±15–20% deviation for *P*/*Q*, and ±1.5–2.0% deviation for *U*
- **Band B**: ±10–15% deviation for *P*/*Q*, and ±1.0–1.5% deviation for *U*

These narrower bands allow us to study the behavior of the detection and identification algorithms under more subtle manipulations. For each simulation, a certain number of measurements (e.g., 10) are randomly selected to be attacked, and their values are modified within one of the two defined bands.

Each simulation scenario involves varying the **number of attacked measurements** (from 3 to 18 measurements), while keeping the perturbation within a fixed band. This approach allows us to evaluate how detection and identification capabilities degrade or remain robust as the number of attacked measurements increases.

There are two main result files:

- `identification_15_20.json`: Results for attacks with deviations in Band A
- `identification_10_15.json`: Results for attacks with deviations in Band B

## `.json` File Structure

The structure of these `.json` files follows a nested dictionary format similar to previous test cases, with some adaptations due to the new focus on varying the number of attacked measurements:

- **First-level key**: Power factor (`090neg`, `090pos`, `100pos`)
- **Second-level key**: Time instant — fixed to `10` in our analysis
- **Third-level key**: Lambda value — fixed to `2.5`
- **Fourth-level key**: Number of attacked measurements (it ranges from `3` to `18`)
- **Fifth-level key**: A dictionary containing:
  - **Detection records** (for detection files):
    - `Detection`: List indicating for each simulation if the attack has been detected (`true`) or not (`false`).
  - **Identification metrics** (for identification files):
    - `Precision`: Average precision across all simulations.
    - `Recall`: Average recall across all simulations.
    - `Accuracy`: Average accuracy across all simulations.

Note that the **F1-score** can be derived from precision and recall. For each combination of power factor, time instant, lambda value, and number of attacked measurements, **1,000 simulations** have been conducted. Each simulation involves a random selection of measurements modified by the attack. In total, the results presented here are based on **45,000**.

## Naming Convention for Figures

The figures in this folder follow a structured naming convention to clearly identify the content of each plot. The filename format is:  
`<Mode>.pdf`  

where:

- **`<Mode>`**: Either `detection` or `identification`.

This naming system allows for easy categorization and retrieval of results based on the attack type and simulation parameters.