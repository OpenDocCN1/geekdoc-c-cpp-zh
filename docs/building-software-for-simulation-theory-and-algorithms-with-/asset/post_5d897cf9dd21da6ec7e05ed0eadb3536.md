
![](img/df6085a1b35edf9c9ea818a5c66ccad9_343_0.png)

More generally, a system morphism from a big system with set of states Q, inputs X, outputs Y, time base T, state transition function Δ, and output function Λ to a small system described by Q', X', Y', T', Δ', and Λ' comprises three functions

g : <X', T'> → <X, T>
h : Q̃ →_onto Q', where Q̃ ⊆ Q
k : Y →_onto Y'

that satisfy

h(Δ(q, g(x'))) = Δ'(h(q), x')   (C.1)
k(Λ(q)) = Λ'(h(q))   (C.2)

where q ∈ Q̃ and x' ∈ X'. The function g transforms an input trajectory for the small system into an input trajectory for the big system. The function h transforms a subset of the states of the big system to states of the small system in such a way that all of the small system's states are covered (i.e., the function h is onto). The function k does the same thing as h, but for the sets of output.

Equations C.1–C.2 are illustrated in Figure C.1. The idea is that the following two procedures produce identical results:

- 1. Provide to the big system a suitably transformed input for the small system, compute the resulting state of the big system, and transform this into a state of the small system.
- 2. Transform the initial state of the big system into a state for the small system and apply the same input as above to compute a new state for the small system.

A useful fact is that if the trajectories are decomposable into generator segments, then a homomorphism constructed on that set of generators implies a homomorphism of the complete system (see, e.g., Ref. 157). The primitive segments for discrete-time and discrete-event systems satisfy this requirement. For instance, every trajectory of a discrete-time system can be constructed by concatenating trajectories of unit length. Hence, these constitute generators for the system. The functions h and g can now be applied to the single-step transition function δ as follows, where x' is now a generator segment:

h(δ(q, g(x'))) = δ'(h(q), x')   (C.3)

Equation C.3 implies Equation C.1 and is often a more practicable tool for constructing homomorphisms.

### C.2 SINUSOIDAL STEADY-STATE ANALYSIS

Changes in the speed, output power, and excitation voltage of an electric generator occur much more slowly than do the changes in voltages and currents in transmission wires, capacitor banks, and other electrical equipment. It is therefore convenient in the analysis of generator dynamics to avoid dynamic models of purely electrical devices and use instead simpler algebraic models. For this purpose, it is assumed that these devices always see a sinusoidal voltage and current characterized by A sin(ωt + θ). The amplitude A and phase angle θ may vary with time, but the frequency ω is fixed. Justification for these assumptions can be found in almost any textbook on power systems engineering or the analysis of electric circuits (see, e.g., Ref. 52 or 97). This assumption simplifies the calculation of currents and voltages in the transmission network by considering only instantaneous changes in amplitudes and phase angles. We proceed as follows:

- 1. Each sinusoidal source is replaced by a *phasor* A cos θ + jA sin θ. With a slight abuse of notation, this is abbreviated A∠θ¹.
- 2. Inductors L, resistors R, and capacitors C are replaced with complex impedances jωL, (jωC)⁻¹, and R, respectively. This produces a network containing only complex impedances Z that satisfy Ohm’s law when the currents I and voltages V are phasors: V = IZ. The complex power at a device is S = VI^\*. The real part of S is called *real power* and the imaginary part, *reactive power*.
- 3. Voltages at nodes and currents in branches are calculated using the mesh current or node voltage method.

¹ In fact, A∠θ = A cos(ωt + θ) and A cos θ + jA sin θ is the phasor transform of that sinusoid. In most cases, the use of A∠θ for the phasor does not cause confusion.

There is a slight incongruence when using this method of analysis in conjunction with dynamic models of the generators. The transmission system model is constructed by assuming that the power signal has a fixed frequency. However, the synchronous machine model has a frequency that varies. In fact, frequency variation at the generators appears on the transmission lines and everywhere else, but they are ignored when calculating line currents and node voltages. Changes in the generator frequencies cannot be similarly eliminated because it drives change in the machines’ phase angles, and these phase angles determine how power flows from the generators to the loads. Nonetheless, this method of calculation is very practical and widely used.

## REFERENCES

- 1. *IEEE Standard for Distributed Interactive Simulation—Application Protocols.* IEEE Standard 1278.1a-1998, Aug. 1998.
- 2. M. Abrash, *Michael Abrash's Graphics Programming Black Book*, Special ed., Coriolis Group Books, 1997.
- 3. F. L. Alvarado, *Is system control entirely by price feasible?* Proc. 36th Annual Hawaii Int. Conf. System Sciences, Jan. 2003, pp. 6–9.
- 4. A. Ames, A. Abate, and S. Sastry, *Sufficient conditions for the existence of zeno behavior,* Proc. 44th IEEE Conf. Decision and Control and European Control (ECC 2005), Dec. 2005.
- 5. A. D. Ames, *A Categorical Theory of Hybrid Systems,* PhD thesis, Dept. Electrical Engineering and Computer Sciences, Univ. California, Berkeley, 2006.
- 6. J. Arrillaga and N. R. Watson, *Computer Modelling of Electrical Power Systems,* Wiley, 2001.
- 7. W. R. Ashby, *An Introduction to Cybernetics,* Chapman & Hall, 1956.
- 8. F. J. Barros, *Dynamic structure discrete event system specification: A new formalism for dynamic structure modeling and simulation,* Proc. 27th Winter Simulation Conf. (WSC '95), 1995, pp. 781–785.
- 9. F. J. Barros, *Modeling formalisms for dynamic structure systems,* ACM Trans. Model. Comput. Simulation 7(4):501–515 (1997).
- 10. C. Barz, R. Göpfarth, P. Martini, and A. Wenzel, *A new framework for the analysis of simultaneous events,* Proc. 2003 Summer Computer Simulation Conf. (SCSC'03), July 2003.
- 11. T. Beltrame, *Design and Development of a Dymola/Modelica Library for Discrete Event-Oriented Systems Using DEVS Methodology*, Master's thesis, ETH Zürich, Dept. Computer Science, Inst. Computational Science, 2006.
- 12. F. T. Bergmann and H. M. Sauro, Comparing simulation results of SBML capable simulators, *Bioinformatics* 24(17):1963–1965 (2008).
- 13. H. Bersini and V. Detour, Asynchrony induces stability in cellular automata based models, in R. A. Brooks and P. Maes, eds., *Artificial Life IV*, MIT Press, 1994, pp. 382–387.
- 14. F. P. Brooks, *The Mythical Man-Month and Other Essays on Software Engineering*, Dept. Computer Science, Univ. North Carolina at Chapel Hill, 1975.
- 15. R. Brown, Calendar queues: A fast O(1) priority queue implementation for the simulation event set problem, *Commun. ACM* 31(10):1220–1227 (1988).
- 16. W. Cai, F. B. S. Lee, and L. Chen, An auto-adaptive dead reckoning algorithm for distributed interactive simulation, *Proc. 13th Workshop on Parallel and Distributed Simulation (PADS '99)*, 1999, pp. 82–89.
- 17. L. P. Carloni, R. Passerone, A. Pinto, and A. L. Sangiovanni-Vincentelli, Languages and tools for hybrid systems design, *Found. Trends Electron. Design Automation* 1(1/2):1–193 (2006).
- 18. C. D. Carothers, K. S. Perumalla, and R. M. Fujimoto, Efficient optimistic parallel simulations using reverse computation, *ACM Trans. Model. Comput. Simulation* 9(3):224–253 (1999).
- 19. F. E. Cellier, *Continuous System Modeling*, Springer, 1991.
- 20. F. E. Cellier and F. Kofman, *Continuous System Simulation*, Birkhauser, 2005.
- 21. B. Chapman, G. Jost, and R. van der Pas, *Using OpenMP: Portable Shared Memory Parallel Programming*, MIT Press, 2007.
- 22. R. N. Charette, Why software fails, *IEEE Spectrum* 42(9):42–49 (Sept. 2005).
- 23. Y. K. Cho, B. P. Zeigler, and H. S. Sarjoughian, Design and implementation of distributed real-time DEVS/CORBA, *Proc. 2001 IEEE Int. Conf. Systems, Man, and Cybernetics*, 2001, Vol. 5, pp. 3081–3086.
- 24. Y. K. Cho, J. H. Kim, and T. G. Kim, DEVS framework for component-based modeling/simulation of discrete event systems, *Proc. 2002 Summer Computer Simulation Conf.*, July 2002, pp. 210–215.
- 25. A. C. Chow, B. P. Zeigler, and D. H. Kim, Abstract simulator for the parallel DEVS formalism, *Proc. 5th Annual Conf. AI, Simulation, and Planning in High Autonomy Systems*, 1994, pp. 157–163.
- 26. A. Chung, H. Chow, and B. P. Zeigler, Parallel DEVS: A parallel, hierarchical, modular, modeling formalism, *Proc. 26th Winter Simulation Conf.*, 1994, pp. 716–722.
- 27. J. R. Clymer, *Simulation-Based Engineering of Complex Systems*, 2nd ed., Wiley, 2009.
- 28. D. Cornforth, D. G. Green, D. Newth, and M. Kirley, Do artificial ants march in step? Ordered asynchronous processes and modularity in biological systems, in *Artificial Life VIII*, MIT Press, 2002, pp. 28–32.
- 29. B. A. Cota and R. G. Sargent, A modification of the process interaction world view, *ACM Trans. Model. Comput. Simulation* 2(3):109–129 (1992).
- 30. M. C. D'Abreu and G. A. Wainer, M/CD++: Modeling continuous systems using Modelica and DEVS, *Proc. 13th IEEE Int. Symp. Modeling, Analysis, and Simulation of Computer and Telecommunication Systems (MASCOTS '05)*, 2005, pp. 229–238.
