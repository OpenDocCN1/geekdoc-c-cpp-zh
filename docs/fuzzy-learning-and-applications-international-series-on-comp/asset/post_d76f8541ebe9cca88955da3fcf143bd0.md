
neuro-fuzzy scheduler to perform scheduling decision.

## 10.4 Work-Load Characterization

As mentioned above, to deal with the unpredictable nature of the work-load offered by the browsing process, we use a dynamic interval based approach where SIs are based on the limited a priori knowledge about the resource availability and the stored information being retrieved. In this section, we propose a set of three parameters that are used to characterize the capacity requirement profile of an SI; these include Required Amortized Capacity (RAC), Pre-fetch Activity Ratio (PAR) and Capacity Deviation (CD). RAC quantifies the capacity requirement of an SI while PAR and CD represent the destination buffering requirement. The algorithm (1) computes these parameters. In the following, we elaborate more on these parameters and the working of algorithm (1).

RAC corresponds to the minimum capacity requirement of an SI to ensure synchronization. It is important to recognize that RAC is not an arithmetic mean of the capacity requirement computed over the SI; as in an SI, AUSs can be scheduled earlier but cannot be made late. In fact, capacity averaging effect within an SI can only be achieved based on the SI’s work-load profile. Algorithm (1) uses a priori knowledge about the temporal relationships among the AUSs to compute the RAC value. In the following, we first outline details of algorithm (1) for the computation of RAC value.

Recall, from Section 10.2, that in order to facilitate synchronization, objects are segmented into AUSs of equal duration Δ. In algorithm (1), the term s_i/Δ represents the capacity requirement of an AUS_i with size s_i. Also, AUSs with the same presentation deadline are logically grouped together, as shown in Fig. 10.2. Let an SI consist of L such groups represented by the set {G_1, G_2, …, G_L} with G_i denoting the group of AUSs that belong to the temporal period [(i−1)Δ, iΔ). The capacity requirement of group G_i is given by Σ_{AUS_j ∈ G_i} s_j/Δ. Algorithm (1) analyses the L groups of AUSs within the SI and computes RAC_i which denotes the minimum capacity required to ensure a timely delivery of all AUSs up to the i th period (or over time interval [0, iΔ)). At the (i+1)st iteration, based on the value for RAC_i, the algorithm checks whether or not the AUSs belonging to group G_{i+1} can be transported with RAC_i capacity. In other words, it compares the value for RAC_i with the capacity requirement of G_{i+1}. If G_{i+1} does not demand an increase in the overall capacity requirement, the value for RAC_{i+1} is set to RAC_i. Otherwise, RAC_{i+1} is updated, by allowing pre-fetching of relevant information of the (i+1)st period, as detailed in algorithm (1).

The RAC parameter can be further explained using the SI profiles observed

```
Initialize:
$RAC_1 = \sum_{AUS_j \in \mathcal{G}_1} \frac{s_j}{\Delta};\; PAD = 0;\; PAP = 1;$ 
**for** $i := 2$ **to** $L$
  /* Does group $\mathcal{G}_i$'s AUSs increase value of traffic parameter $RAC$, if yes, update the parameter accordingly */
  $RAC_i = \max\left(RAC_{i-1}, \frac{RAC_{i-1}\Delta(i-1)+\sum_{AUS_j \in \mathcal{G}_i} s_j}{i\Delta}\right);$
  /* Is this a pre-fetching period?, if yes, update Pre-fetching Activity Period ($PAP$) and Pre-fetching Activity Density ($PAD$) values. */
  **if** $RAC_i != RAC_{i-1}$
    /* First update the $PAD$ value. */
    $PAD_i = (RAC_i - RAC_{i-1})i\Delta;$
    /* Now update the $PAP$ */
    $PAP = i;$
  **end**
**end**
/* $RAC$ is based on averaging effect up to $PAP$ */
$RAC = RAC_{PAP};$
/* Now compute Pre-fetching Activity Ratio $PAR$, which is a normalized version of the $PAP$ */
$PAP = \frac{PAP}{L};$
/* Capacity Deviation ($CD$) is proportional to the value of Pre-fetching Activity Density (PAD) value and is given by the following expression: */
$CD = \frac{\sum_{i=1}^{PAP} PAD_i}{PAP\Delta};$
```

### Figure 10.5 Computation of parameters characterizing an SI's work-load.

during browsing of the manufacturing hypermedia system example of Figure 10.1. Figure 10.6 depicts the capacity requirement profile of these SIs. In this figure, each SI is composed of eight multimedia objects. For a better illustration, the SI of Fig. 10.6(b) is produced as a result of the reverse playout of SI of Fig. 10.6(a). Such reversal does not change the arithmetic mean of the capacity requirement profiles for both SIs. However, SI of Fig. 10.6(a) contains relatively high activity at the beginning of the presentation. Hence, the minimum capacity requirement to transport this SI cannot be reduced by pre-fetching AUSs beyond time point a as indicated in the figure. On the

other hand, the SI of Fig. 10.6(b) starts with low activity and AUSs can be transmitted earlier to reduce the overall value of RAC. Consequently, for the SI of Fig. 10.6(a) RAC = 0.56 Mbps while the temporal inverse of the SI, as depicted in Fig. 10.6(b), yields RAC = 0.4 Mbps.

The algorithm (1) also computes the Pre-fetch Activity Period (PAP) parameter that characterizes the shape of an SI’s capacity requirement profile by identifying whether the SI contains higher activity at its beginning or at its end. For this purpose it keeps track of a pre-fetch activity index that stores the time up to which pre-fetch is possible. The PAP value of the SIs of Fig. 10.6 is also indicated in the figure. Note, since the SI of Fig. 10.6(a) has a relatively higher capacity activity at the beginning of the SI, pre-fetching is viable up to point a, as shown in this figure. Hence, PAP value for this example is given by a. The SI of Fig. 10.6(b) has relatively higher activity towards the end; the PAP extends towards the end of the SI. The algorithm then normalizes the PAP value and computes the Pre-fetch Activity Ratio (PAR) which is defined as PAR = PAP / L, where L represents the length of the SI. Note that PAR = 0.34 for the SI of Fig. 10.6(a) that has a relatively higher capacity activity at the beginning of the SI and PAR = 1 for the SI of Fig. 10.6(b) which has relatively higher activity towards the end.

The Capacity Deviation (CD) factor characterizes the deviation of an SI’s capacity requirement profile above the RAC value. The algorithm (1) computes the value for CD based on Pre-fetch Activity Density (PAD) factor for each pre-fetching Δ period. In algorithm (1), for the pre-fetching period Δi, RACi ≠ RACi−1. The density of the pre-fetch data during period i is given by the deviation of RACi value from RACi−1 value. In particular, PADi = (RACi − RACi−1)iΔ. Hence, given PADi ∀i = 1,2,⋯,L, we can compute

```
CD = (∑_{i=1}^{PAP} PAD_i) / (PAP Δ)
```

Clearly, the SI of Fig. 10.6(b) has much more deviation from the RAC value as compared with the SI of Fig. 10.6(a). The value of CD is 0.12Mbps in the formal case while it is 10kbps for the later.

In Section 10.6, parameters RAC, PAR and CD are used to describe the work-load of an SI. We provide fuzzy logic rules for selecting a scheduling mechanism that is expected to yield the best results for the given work-load and system state. In the following, we elaborate on the requirement of the neuro-fuzzy scheduler.

## 10.5 Dynamic Scheduling at the Server

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_335_0.png)

(a) Example SI with High RAC value

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_335_1.png)

(b) Example SI with Low RAC value

### Figure 10.6 SI profiles observed during browsing in Hypermedia System of 10.1.

Pre-orchestrated and stored nature of information, the presence of a large number of small objects and soft delivery requirements make multimedia Web

applications quite flexible to the networking scenarios. In this section, we formulate a dynamic scheduling problem where, at each SI, the multimedia server dynamically adapts to the non-stationary work-load. The objective is to minimize a multi-variable function for QOP degradation due to AUS losses. The scheduling problem is formally presented in the following subsection.

### 10.5.1 A Multi-criteria Scheduling Problem

The main functionality of the scheduler is to determine the order and time at which the AUSs should be transmitted over the given m channels. If the resources are severely constrained, the multimedia server needs to invoke an AUS filtering process. For this purpose, as discussed in Section 10.3.3, each AUSi is assigned an importance factor Ii which quantifies the relative importance of the AUSi within a group of AUSs. To formulate an objective function for the AUS filter, first define a filtering factor(Fi) as follows:

```
F_i = { 0 if AUS_i ∈ S, 1 otherwise. }
```

Here S represents the schedule obtained after observing AUS-filtering. In other words, IiFi represents the cost incurred when an AUSi is dropped at the server.

In addition of minimizing the number of AUSs dropped, the scheduler also needs to minimize the AUS losses due to deadline miss or destination buffer overflow. Let Σ Ld and Σ Lb, respectively, represent the total number of AUSs lost due to deadline misses and destination buffer overflow. Note that Σ Ld and Σ Lb are two conflicting objectives. Specifically, Σ Ld can be minimized by pre-fetching as much AUSs as possible. However, extensive pre-fetching may yield extremely high data (AUSs) losses due to buffer overflow.

For a given Scheduling Interval (SI), the scheduler's objective depends on the state of the system (resource availability) and the SI's work-load. For example, based on the state of the system and work-load of the SI, the scheduler needs to identify when to follow the AUS-filtering process, i.e., minimization of Σ IiFi objective. Similarly, if the SI's work-load is significantly less than the total capacity of the m channels, and the scheduler selects minimization of Σ Ld as the objective. Such a selection will yield a high number of losses due to buffer overflow condition. Hence, the objective of the scheduler is to minimize all types of AUS losses for every SI considered. In other words, the objective is to minimize the following:

```
∑_{SI} { ∑_{AUS_i ∈ SI} ( L_d + L_b + I_i F_i ) } . (10.2)
```
