# Time Instant Influence

Blah

## `data.json` File Structure

The result files have a `.json` extension and there are two types of results: detection and identification. Detection files are prefixed with the word "detection" and indicate, out of the total number of simulations performed, in which of them a cyberattack was detected, without specifying the specific measurement or set of measurements attacked. On the other hand, identification files are prefixed with the word "identification" and provide various metrics evaluating the perfomrance in that specific scenario, which are described in detail below.

The `data.json` file is a nested dictionary with the following structure:

- **First level key**: Percentage of attacked measurements (`5`, `10`, `20`, `40`)
- **Second level key**: Test case number (`0` to `9`)
- **Third level**: Dictionary containing `Detction` records for the detection evaluation or containing the following evaluation metrics for identification within scenarios:
  - `Precision`
  - `Recall`
  - `Accuracy`
  - `F1-score`
  - `Z` (Root mean square difference between unmodified measurements and tool estimates)
  - `Norm2` (Root mean square difference between real state and tool state estimation)
  - `NormInf` (Maximum difference between real state and tool state estimation)

For each combination of attack percentage and test case, 20 simulations have been conducted, with each simulation involving a random selection of measurements modified by the attack. In total, the results presented here are based on **800 simulation runs**.

## Naming Convention for Figures

The figures in this folder follow a structured naming convention to clearly identify the content of each plot. The filename format is:\
`<Mode>`_`<Magnitude>`_`<Node>`_`<Scenario>`.pdf\
where:

- **`<Mode>`**: Detection or identification.
- **`<Magnitude>`**: The type of electrical magnitude that was attacked (`U` for voltage, `P` for active power, `Q` for reactive power and `I` for current).
- **`<Node>`**: The identifier of the node where the attack was performed.
- **`<Scenario>`**: The scenario under which the test was conducted:
  - `with_MT`: Measurements from the MV feeders are included.
  - `wo_MT`: No measurements from the MV feeders are available.
  - `with_PSM`: Pseudo-measurements of active power were used based on upstream and downstream data.

This naming system allows for easy identification of the attack type, location, and test conditions directly from the figure filename.

