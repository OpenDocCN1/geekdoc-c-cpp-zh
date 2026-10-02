
parameters tuning for both the submodel and the complete VE based on the least-squares optimization method (LSOM) in [29].

## 7.3.2.2 Inconsistency Caused Judgment

Assume that at tₙ, the PE and the VE are judged as inconsistent (i.e., ‖pₑ − pₐ‖ > Tₚ). To identify the inconsistency cause, take the time series of historical states of the PE under the same condition (i.e., C) as the reference. Represent the reference as Pₕₛ = (xₕₛ₁ … xₕₛᵢ … xₕₛₜ), where t is the parameter number, xₕₛᵢ is the time series for the i th parameter, denoted as xₕₛᵢ = (xₕₛᵢ(1) … xₕₛᵢ(q) … xₕₛᵢ(s))ᵀ, and s is the element number. Accordingly, for the i th parameter of pₐ (i.e., xᵢ) and pₑ (i.e., yᵢ), the time series from the current (i.e., tₙ) to a future moment (i.e., tₙ₊₁) are denoted as xₛᵢ = (xₛᵢ(1) … xₛᵢ(q) … xₛᵢ(s))ᵀ and yₛᵢ = (yₛᵢ(1) … yₛᵢ(q) … yₛᵢ(s))ᵀ, respectively. Denote Pₐₛ = (xₛ₁ … xₛᵢ … xₛₜ) and Pₑₛ = (yₛ₁ … yₛᵢ … yₛₜ) as the time series for pₐ and pₑ. Pₕₛ, Pₐₛ, and Pₑₛ are the multivariate time series. Measure the similarity of Pₐₛ and Pₕₛ, as well as Pₑₛ and Pₕₛ according to the correlation based dynamic time warping (CBDTW) described in Ref. [30], which considers the correlation between the variables and provides an accurate measurement. Based on the measurement result, judge the inconsistency cause. The process is shown in Fig. 7.7.

![](img/5042607b423be4a5ee3f15dae22cc5bb_155_0.png)

Figure 7.7 Similarity measurement.

## 7.3.2.3 Identification and Prediction of Fault Cause

- 1. **Gradual fault:** From step 4, before the gradual fault occurs completely, localize the fault cause in advance. It includes two phases, as shown in Fig. 7.8. In the training phase, extract the forewarning features for different fault causes from the historical data of PE and VE, including X, Y, and Z. Then train the prediction models, which fuse the features from both the PE and the VE, and relate them to the fault causes through methods such as the neural network. If the trained models can pass the accuracy test, they will be considered as good models and used for the prediction. In the prediction phase, input the forewarning features extracted from the real-time data of X, Y, and Z into the models and predict the cause.
- 2. **Abrupt fault:** From step 5, localize the components related to the abrupt fault first based on the deviation between PE and VE. Then check the components one by one through comparing their parameters from the VE with those from the PE, to finally identify the source of disturbances.

![](img/5042607b423be4a5ee3f15dae22cc5bb_156_0.png)

Figure 7.8 Model training and fault cause prediction.

## 7.3.3 Coevolution Mechanism

During DT-driven PHM, the PE, VE, and Ss evolve with each other continuously, as shown in Fig. 7.9. For PEi, VEi, and Ssi, i represents the i th interaction among the three parts.

The PE and the VE always make an effort to keep consistent with each other. Assume that PEi and VEi are consistent in the beginning. To distinguish the current “consistency” with others, it is labeled as “consistencyi.” However, since the states of PEi (denoted as pai) are continuous and variable, the states of VEi (denoted as pei) may appear to have deviated due to defects and limitations in the models. In this situation, model calibration service will be performed to calibrate the VEi to keep up with the PEi. After that, the new consistency (i.e., consistencyi+1) is reached. From consistencyi to consistencyi+1, the VE evolves to better understand the PE, which makes the VE provide more accurate data and models for the PHM. As to the other aspect, if random disturbances from the external environment (always unknown to VEi) exist on PEi, the deviation between pai and pei will also appear. The disturbances will be captured by the inconsistency cause judgment service and eliminated by the maintenance service to achieve new consistency. By this process, the disturbance sources are reduced gradually and the PE is more likely to operate as the expected process provided by the VE, which makes the faults of the PE more predictable.

With the accumulation of data, the functions of Ss are also updated and improved continuously, which makes Ssi evolve to Ssi+1. For example, since the fault cause prediction models in Section 7.3.2.3 can be

![](img/5042607b423be4a5ee3f15dae22cc5bb_157_0.png)

Figure 7.9 Coevolution mechanism of DT-driven PHM.

optimized online with more data obtained for training, the fault cause identification and prediction service based on the trained models is also refined accordingly.

## 7.4 CASE STUDY

### 7.4.1 Problem Description

A WT is complex equipment that transforms wind energy to mechanical and electrical energy. Since the WT usually works over decades and its working conditions are characterized by stochastic loading, rapidly varying torque, and a dusty environment, most components may fail and the failure rates are shown in Table 7.1 [31]. Hence, PHM is crucial to keep the WT operating reliably. However, some problems still exist as follows. Because of the harsh environment, it is not practical to access the WT all the time for prognosis and maintenance. The features extracted from the physical aspects are mainly used for fault cause identification or prediction, but features from the virtual side are ignored. Since signals from the physical aspect (e.g., the vibration signals) are easily interfered with by other sources, the diagnostic results can be affected [27]. To address the above issues, the DT-driven PHM is applied in the case study.

The gearbox and the yaw system are among the top three components that are prone to malfunctioning. The gearbox is used to transform the low speed drive from the wind power into high speed for the generator, and its failures are mainly caused by the gradual degradation of gears in it. The yaw system can align the nacelle with the wind direction to make the WT obtain the maximum wind energy. Failures of the yaw system

# Table 7.1 Fault rates of WT components

| Components | Failure rates | Components | Failure rates |
|---|---|---|---|
| Electrical control | 13% | Blades | 5% |
| **Gearbox** | **12%** | Brake system | 5% |
| **Yaw system** | **8%** | Control system | 2% |
| Entire turbine | 7% | Entire nacelle | 1% |
| Generator | 5% | Shaft/bearing | 1% |
| Hydraulic system | 5% | Others | 30% |
| Grid | 5% |  |  |

*Note:* The bold characters outstand the gearbox and yaw system which are among the top three components that are prone to malfunctioning. The two components are used to verify the proposed method in the following content, which can better illustrate the efficiency of the proposed method to some extent.

are mainly caused by the wind vane with mechanical structures, which are prone to damage by disturbances from the external environment (e.g., the abrupt drop of temperature). In this section, firstly, the DT of a WT is constructed according to Section 7.2, and the DT-driven PHM method in Section 7.3 is then applied to the yaw system and gearbox to deal with the abrupt fault and gradual fault, respectively.

### 7.4.2 Digital Twin-Driven PHM for Yaw System

The yaw system is part ④ of the physical WT in Fig. 7.3. In this case study, the fault of the yaw system is caused by the sudden disturbance from the environment and it leads to yaw error. Related symbols are listed in Table 7.2.

According to steps 1 and 2 in Section 7.3.2, with the constructed DT of the WT, the simulation and interaction are started. According to step 3, p_a and p_e are denoted as p_a = P_ao and p_e = P_eo, respectively. P_ao is calculated according to the output voltage and current collected from the voltage and current sensors deployed in part ⑤ (i.e., electronic control system) of the physical WT in Fig. 7.3. P_eo is simulated by the virtual WT based on the relation existing between W_s and P_eo [32]. The deviation is calculated according to Eq. (7.1). As ||p_e - p_a|| ≥ T_p, p_a and p_e are considered inconsistent.

||p_e - p_a|| = |P_ao - P_eo| / |P_ao| (7.1)

To identify the inconsistency cause, according to step 5, the historical power output under the same W_s is selected as the reference and denoted as P_ho. Time series of P_ho, P_ao, and P_eo in 600 s are taken out for comparison in Fig. 7.10, where the sampling interval is 10 s. Hence, P_hs, P_as, and P_es are denoted as P_hs = (P_ho(1)…P_ho(60))^T, P_as = (P_ao(1)…P_ao(60))^T, and P_es = (P_eo(1)…P_eo(60))^T, respectively. P_hs, P_as, and P_es are univariate time series. Through distance calculation, it is judged that P_es is similar

Table 7.2 A list of symbols of yaw system
Symbols of yaw system in physical WT | Symbols of yaw system in virtual WT
A_ay | Yaw angle | A_cy | Yaw angle
P_ao | Power output | P_co | Power output
W_d | Wind direction |  | 
W_s | Wind speed |  |
