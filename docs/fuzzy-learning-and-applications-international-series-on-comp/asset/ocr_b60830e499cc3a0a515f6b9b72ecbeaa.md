# 2.3. Analog Core Implementation

![](bbox=[0.27, 0.15, 0.68, 0.32])

(a)

y_1 = y_1* (w_1* + I_OS*)

y_k = y_k* (w_k* + I_OS*)

y_N = y_N* (w_N* + I_OS*)

![](bbox=[0.5, 0.3, 0.75, 0.48])

(b)

Figure 2.12: (a) Singleton weighting concept; (b) controller output node.

other hand, parallel-connected unit transistors are used to realize the binary weighting and, thus, reduce systematic errors caused by the lack of symmetry. The bias current depicted by the dashed lines in Fig.2.12(a) is added to reduce speed degradations due to the increase of parasitic capacitance for large singleton values.

After singleton weighting, the rule block outputs are wired up to the output node where a current −∑_{1,N} y_k* I_OS* is added to remove the offset, thus obtaining equation (2.4).

# 2.3.2. Modifications for the Multiplexed Architecture

The architecture of the analog core in Fig.2.5 is similar to that in Fig.2.2, but just 2^M rules are needed here, and only two membership functions per input. Building blocks are also quite similar to those described above, although we should point out some differences derived from the specific multiplexing strategy. First, as mentioned in Section 2.2.3., only the thick part of the membership functions in Fig.2.4(b) is needed in each interval. Hence, the membership function circuit must be able to generate two pieces with slopes of opposite signs. This is achieved in the simplest way by a differential pair, as Fig.2.13(a) depicts. Moreover, the differential pair provides two complementary curves, which can be exploited to save the explicit complement implementation if we perform the minimum by means of a maximum-plus-complement circuitry