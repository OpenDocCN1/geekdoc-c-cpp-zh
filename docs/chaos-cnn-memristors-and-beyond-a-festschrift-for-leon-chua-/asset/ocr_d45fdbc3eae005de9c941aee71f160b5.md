parameters because broken wave fronts seal at the initiation site and the wave does not develop wave breaks. The model displays reentrant dynamics for smaller neighbourhood sizes. Unidirectional block at the initiation site generates spiral waves. In contrast to the simple Greenberg-Hastings model used in earlier studies, reentrant activity is often initiated from a single active cell. Here, the mechanism for unidirectional propagation in the randomized CA is asymmetry in connectivity at the single cell level (see Fig. 2). The spiral tip tends to increase its meander as fatigue accumulates. The spiral tip eventually collides with the boundary of the simulation grid, terminating activity. This process repeats for some parameters, giving rise to a bursting rhythm. A parameter space map for the different dynamic regimes of this model is given in [5].

# 6. Network Bursting in CAs in the Absence of Reentry

The cellular automata model can also display triggered activity for large neighbourhood sizes. We explored the dynamics of the CA discussed in the last section, but here a small subset of cells beat with a fixed period randomly chosen within an interval instead of having all cells have a low probability of spontaneously firing [6]. Oscillators are phase reset when excited by neighbouring cells. Triggering in the model occurs when a wave acts to synchronise pacemakers, which increases the probability of subsequent synchronous activations. Pacemakers desynchronize over time because faster pacemakers fire before others and are subsequently refractory to phase resetting. We quantified the dynamics of the model by running the simulation for a large number of randomly assembled grids for different neighbourhood sizes. The potential for a grid to generate triggered bursting was measured by initiating a wave at one edge of the grid, and testing whether a triggered wave is generated after a short interval. The probability for generating spiral wave bursts is highest at r = 1.65 while the probability for triggered target wave generation is highest at r = 2.1 [6]. Triggered waves occur relatively infrequently: spontaneous reentry occurs in three times as many randomly generated simulation grids [6]. In contrast to spiral wave bursting, triggered wave bursting does not require addition of a fatigue term for spontaneous termination.

# 7. Conclusions

Initiation of bursting in CAs depends on the interplay between local differences in geometry and the connectivity of the network. Although cardiac tissue may be more accurately represented at the cell level with biophysically realistic continuous partial and ordinary differential equation models, the computational efficiency of CAs make them well suited for modelling the effects of randomly distributed heterogeneities, asymmetries in connectivity and variation in local spontaneous activity. The inherent stochasticity of paroxysmal cardiac arrhythmias such as nonsustained ventricular tachycardia may be a reflection of similar variability at microscopic space scales. If so, CAs can give valuable insights into arrhythmogenesis in diseased tissue.

# Acknowledgments

Gil Bub acknowledges support from the UK Medical Research Council and the BHF Centre of Research Excellence, Oxford (RE/08/004). Alvin Shrier and Leon Glass thank NSERC, MITACS (Mpprime) and the Canadian Heart and Stroke Foundation for financial support.

# References

+   [1] Alonso S, Barr M & Kapral R (2009). Effective medium approach for heterogeneous reaction-diffusion media. *J Chem Phys* **131**, 214102.
+   
+   [2] Billette J, Metayer R & St-Vincent M (1988). Selective functional characteristics of rate-induced fatigue in rabbit atrioventricular node. *Circ Res* **68**, 790–799.
+   
+   [3] Bub G, Shrier A & Glass L (2002). Spiral wave generation in heterogeneous excitable media. *Phys Rev Lett* **88**(5), 058101 (1–4).
+   
+   [4] Bub G & Shrier A (2002). Propagation through heterogeneous substrates in simple excitable media models. *Chaos* **12**(3), 747–753.
+   
+   [5] Bub G, Shrier A & Glass L (2005). Global organization of dynamics in oscillatory heterogeneous excitable media. *Phys Rev Lett* **94**, 028105 (1–5).
+   
+   [6] Bub G, Tateno K, Shrier A & Glass L (2003). Spontaneous initiation and termination of complex rhythms in cardiac cell culture. *J Cardiovasc Electrophysiol* **14**(10), s229–s236.
+   
+   [7] Bueno-Orovio A, Cherry EM & Fenton FH (2008). Minimal model for human ventricular action potentials in tissue. *J Theor Biol* **253**(3), 544–560.
+   
+   [8] Chay TR (1990). Electrical bursting and intracellular Ca²⁺ oscillations in excitable cell models. *Biol Cybern* **63**, 15–23.