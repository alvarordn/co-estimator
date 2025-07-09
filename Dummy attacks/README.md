# Dummy Attacks

This folder contains test cases simulating **dummy false data injection (FDI) attacks**, where raw measurements are altered without considering the physical or operational constraints of the power system. These attacks are typically used to evaluate the robustness of state estimation and bad data detection algorithms against naive or unsophisticated cyber threats.

These attacks can be categorized as:

- **Gross dummy attacks**: Large, unrealistic changes in measurements. Likely launched by attackers with little knowledge of power systems, and easily detectable by basic bad data detection (BDD) checks.
- **Mild dummy attacks**: Subtle changes that respect basic physical limits (e.g., voltage ranges, capacity bounds). These require more advanced detection techniques based on statistical analysis and model consistency checks.

## Test Case Overview

The following table summarizes the different test cases included in this folder:

| Case id     | Test Case                                | Description                                                                 |
|-----------|----------------------------------|-----------------------------------------------------------------------------|
|01       | Time Instant Evaluation | Evaluates how the timing of the attack—and consequently, the power output of the PV plant—affects the effectiveness of detection and identification strategies. Additionally, the tuning parameter (λ) of the Huber estimator is optimized to enhance robustness under such conditions|
|02       | Single Attack Amplitude Evaluation | Analyzes the impact of varying the amplitude of a single measurement attack |
|03       | Double Attack Amplitude Evaluation | Investigates the effect of concurrent attacks targeting two measurements, with identical magnitude (in terms of P, Q, U, or I), but applied at different locations within the system (the amplitude of the attacks is also studied) |
|04       | Combined Attack Amplitude Evaluation | Examines the impact of simultaneous attacks on two different magnitudes (P, Q, U, or I) measured at the same or different locations (the amplitude of the attacks is also studied) |
|05       | Multiple Attack Evaluation | Assesses system behavior under widespread dummy attacks across several measurements |
|06       | Single Attack considering Pseudomeasurements Evaluation | Evaluates whether the inclusion of pseudomeasurements improves state estimation accuracy under a single dummy attack    |
|07       | Multiple Attack considering Pseudomeasurements Evaluation | Investigates the effectiveness of pseudomeasurements in improving state estimation resilience under multiple dummy attacks  |


## Detailed Case Descriptions

### **Time Instant Evaluation (Case 01)**

This test case evaluates how the timing of the dummy attack affects the performance of detection and identification mechanisms. Since the power output of the PV plant varies over time depending on environmental conditions (e.g., irradiance), the impact of launching an attack at different operational states of the system is analyzed. Additionally, the tuning parameter (λ) of the Huber estimator is optimized to improve robustness under these time-varying conditions.

### **Single Attack Amplitude Evaluation (Case 02)**

This test case investigates the effects of injecting a single dummy false data injection attack targeting one measurement (e.g., real power *P*, reactive power *Q*, voltage *U*, or current *I*). The amplitude of the injected error is systematically varied to assess its detectability and the ability of the state estimator to correctly identify the anomaly. This helps determine the sensitivity of bad data detection algorithms to varying magnitudes of simple attacks.

### **Double Attack Amplitude Evaluation (Case 03)**

In this scenario, two simultaneous dummy attacks are applied to different measurements within the system. Both attacks have the same magnitude (in terms of *P*, *Q*, *U*, or *I*) but target distinct locations in the network. The amplitude of the attacks is varied across multiple test runs to evaluate how detection and identification systems respond to coordinated yet unsophisticated multi-point threats.

### **Combined Attack Amplitude Evaluation (Case 04)**

This case examines the impact of launching concurrent dummy attacks on two **different types** of measurements (e.g., voltage and current, or real and reactive power) either at the same or at different locations. The amplitude of both attacks is adjusted independently across simulations to study how combined variations affect detection accuracy and the overall reliability of state estimation under naive multi-signal manipulation.

### **Multiple Attack Evaluation (Case 05)**

This test case simulates widespread dummy attacks affecting several measurements simultaneously. The number of attacked measurements and the amplitude of each injected error are varied to assess the system's resilience when faced with large-scale, uncoordinated FDI attempts. Particular attention is given to how traditional and enhanced bad data detection methods perform under increased attack complexity.

### **Single Attack Considering Pseudomeasurements (Case 06)**

This case evaluates whether incorporating pseudomeasurements—such as load forecasts or historical values—into the state estimation process improves robustness against a single dummy attack. By varying the amplitude of the attack, the effectiveness of pseudomeasurements in mitigating the impact of erroneous data and enhancing estimation accuracy is analyzed.

### **Multiple Attacks Considering Pseudomeasurements (Case 07)**

Building upon Case 06, this test extends the analysis to multiple dummy attacks occurring simultaneously across different measurements. The amplitude of each attack is adjusted to evaluate how well pseudomeasurements support the estimator’s ability to maintain accuracy and detect anomalies under more complex attack scenarios.
