# Smart Attacks

This folder contains test cases simulating **smart false data injection (FDI) attacks**, where the manipulated measurements are crafted to follow the physical and operational constraints of the power system. These attacks aim to bypass traditional detection mechanisms by maintaining consistency with the system model.

Smart attacks typically require advanced knowledge of the grid topology and operating conditions, making them more sophisticated and harder to detect than dummy attacks.

## Test Scenarios

Three scenarios have been considered. All tests were conducted with the photovoltaic plant operating at 13:00 hours (a time of high irradiance), under a power factor of 0.9 capacitive.

The three scenarios reflect different assumptions regarding the availability of measurements in the medium-voltage feeders of the PV plant:

- **Scenario 1**: Measurements from the MV feeders are included (`with_MT`).
- **Scenario 2**: No measurements from the MV feeders are available (`wo_MT`).
- **Scenario 3**: Pseudo-measurements of active power are generated based on upstream and downstream measurements (`with_PSM`).

These scenarios allow for the evaluation of the estimator’s performance under varying data availability conditions.

## `data.json` File Structure

The `data.json` file is a nested dictionary with the following structure:

- **First level key**: Percentage of attacked measurements (`5`, `10`, `20`, `40`)
- **Second level key**: Test case number (`0` to `9`)
- **Third level**: Dictionary containing the evaluation metrics:
  - `Precision`
  - `Recall`
  - `Accuracy`
  - `F1-score`
  - `Z` (Root mean square difference between unmodified measurements and tool estimates)
  - `Norm2` (Root mean square difference between real state and tool state estimation)
  - `NormInf` (Maximum difference between real state and tool state estimation)


## Naming Convention for Figures

The figures in this folder follow a structured naming convention to clearly identify the content of each plot. The filename format is:\
`<Magnitude>`_`<Node>`_`<Scenario>`.pdf\
where:

- **`<Magnitude>`**: The type of electrical magnitude that was attacked (`U` for voltage, `P` for active power, `Q` for reactive power and `I` for current).
- **`<Node>`**: The identifier of the node where the attack was performed.
- **`<Scenario>`**: The scenario under which the test was conducted:
  - `with_MT`: Measurements from the MV feeders are included.
  - `wo_MT`: No measurements from the MV feeders are available.
  - `with_PSM`: Pseudo-measurements of active power were used based on upstream and downstream data.

This naming system allows for easy identification of the attack type, location, and test conditions directly from the figure filename.
## Test case description


| Case id | Target node | Magnitude | Deviation | Objective                     |
|---------|-------------|-----------|-----------|-------------------------------|
| 0       | LV0102      | U         | 98%       | Trip an inverter              |
| 1       | POI         | Q         | 80%       | Trip an inverter              |
| 2       | POI         | U         | 98%       | Trip an inverter              |
| 3       | POI         | U         | 102%      | Trip an inverter              |
| 4       | POI         | Q         | 80%       | Economic loss                 |
| 5       | POI         | Q         | 120%      | Economic loss                 |
| 6       | POI         | P         | 80%       | Economic loss                 |
| 7       | POI         | P         | 120%      | Economic loss                 |
| 8       | POI         | U         | 98%       | Economic loss                 |
| 9       | POI         | U         | 102%      | Economic loss                 |

Each case is described next:

### **Case 0**
- **Description**: This test case aims to simulate an attack that could trigger the disconnection of an inverter due to overvoltage. To achieve this, the attack sets the inverter's voltage below the measured value, potentially causing an overvoltage condition that leads the inverter to trip.
- **Target**: LV0102 setting its voltage to a 98 % of the measured value.

### **Case 1**
- **Description**: This test case simulates an inverter trip caused by manipulating the reactive power measurement at the Point of Interconnection (POI). The attack sets a lower reactive power value than the actual measurement, prompting the Power Plant Controller (PPC) to request additional reactive power from the inverters. This can lead to a voltage rise and potentially leads an inverter to trip.
- **Target**: POI setting the reactive power to a 80 % of the measured value.

### **Case 2**
- **Description**: This test case achieves an inverter trip by modifying the voltage measurement at the Point of Interconnection (POI) through an attack that sets a lower voltage value than the actual measurement. If the inverters operate under a Q-V control strategy, they will respond by injecting additional reactive power, which can cause the voltage to rise excessively and ultimately lead to an inverter trip.
- **Target**: POI setting the voltage to a 98 % of the measured value.

### **Case 3**
- **Description**: This test case also targets the voltage measurement at the Point of Interconnection (POI), but in this case, the attack sets a higher voltage value than the actual measured voltage. If the inverters operate under a Q-V control strategy, they will react by absorbing reactive power in an attempt to lower the voltage. This can lead to an excessive voltage drop elsewhere in the system and potentially trigger an undervoltage disconnection.
- **Target**: POI setting the voltage to a 102 % of the measured value.

### **Case 4**
- **Description**: This test case aims to cause a malfunction in the plant without triggering any disconnections, but with a significant economic impact. By setting a reactive power value lower than the actual measurement, the Power Plant Controller (PCC) may demand additional reactive power from the inverters, leading them to inject more reactive power into the grid than required by the system operator. This can result in penalties or financial losses due to inefficient operation. 
- **Target**: POI setting the reactive power to a 80 % of the measured value. 

### **Case 5**
- **Description**: This test case also aims to disrupt plant operation without causing any disconnections, but with potential economic consequences. By setting a reactive power value higher than the actual measurement, the Power Plant Controller (PCC) may reduce its demand for reactive power from the inverters. This can lead to an insufficient injection of reactive power into the grid, potentially resulting in penalties or operational inefficiencies due to non-compliance with the system operator’s requirements.
- **Target**: POI setting the reactive power to a 120 % of the measured value.

### **Case 6**
- **Description**: This test case aims to cause a malfunction in the plant without triggering any disconnections, but with potential economic consequences. By setting an active power value lower than the actual measurement, the Power Plant Controller (PCC) may request additional active power production from other sources or inverters. This can lead to inefficient operation, unbalanced load distribution, or penalties if the plant fails to meet its scheduled generation targets.
- **Target**: POI setting the active power to a 80 % of the measured value. 

### **Case 7**
- **Description**: This scenario also intends to disrupt plant operation without causing disconnections. By setting an active power value higher than the actual measurement, the PCC may reduce its dispatching setpoint or curtail production unnecessarily. This can result in underproduction relative to available resources, leading to lost revenue or penalties due to mismatched generation commitments.
- **Target**: POI setting the active power to a 120 % of the measured value.

### **Case 8**
- **Description**: This test case aims to cause a malfunction in the plant without triggering any disconnections. By setting a voltage value lower than the actual measurement at the POI, the System Operator might respond by requesting additional reactive power injection to raise the voltage. This can lead to unnecessary stress on inverters, inefficient operation, or economic penalties due to deviations from optimal control strategies.
- **Target**: POI setting the voltage to a 98 % of the measured value. 

### **Case 9**
- **Description**: This scenario also seeks to disrupt plant operation without causing disconnections. By setting a voltage value higher than the actual measurement at the POI, the System Operator may reduce the voltage control setpoint or instruct inverters to absorb reactive power unnecessarily. This can result in an undesired voltage drop elsewhere in the network and potential economic losses due to inefficient or incorrect grid management decisions.
- **Target**: POI setting the voltage to a 102 % of the measured value. 
