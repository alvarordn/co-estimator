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

### **Time Instant Influence**
- **Description**: This test case evaluates how the exact moment in which the attack is injected into the system influences the detection and identification performance. It explores whether certain time instants make the system more vulnerable or resilient to dummy attacks due to load variations, observability conditions, or estimator dynamics.

### **Single Attack Amplitude Influence**
- **Description**: A single measurement is manipulated with varying amplitudes. The goal is to assess how the magnitude of the perturbation affects detection thresholds and identification accuracy.

### **Double Attack Amplitude Influence**
- **Description**: Two different measurements are simultaneously attacked with controlled amplitudes. This scenario helps understand how the interaction between multiple attacked measurements impacts detection and identification mechanisms.

### **Combined Attack Amplitude Influence**
- **Description**: Multiple attacks with different magnitudes are applied simultaneously to various measurements. This allows for analyzing how combinations of mild and gross attacks affect overall system integrity and estimator performance.

### **Multiple Attack Influence**
- **Description**: A large number of measurements are attacked simultaneously. This case mimics a distributed attack strategy and tests the estimator’s ability to detect and identify attacks under high stress conditions.

### **Single Attack Pseudomeasurements Evaluation**
- **Description**: A single dummy attack is applied on a pseudomeasurement (i.e., an external forecast or historical value used in the estimation process). This helps evaluate how such attacks propagate through the system and affect the final state estimate.

### **Multiple Attack Pseudomeasurements Evaluation**
- **Description**: Multiple dummy attacks are introduced into different pseudomeasurements. This scenario studies the vulnerability of the estimator when critical external inputs are compromised.
