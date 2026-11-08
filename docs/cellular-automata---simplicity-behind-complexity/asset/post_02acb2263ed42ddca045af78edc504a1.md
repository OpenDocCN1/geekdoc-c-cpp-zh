
![](img/55ff3770fcfe64effe3c90a4d4692fa6_130_0.png)

Fig. 12. Snapshot of the cellular automata model output: the red background is the blood stream, the uninfected cells are in blue, the HIV in black, the infected cells in green, and the antibodies in white.

![](img/55ff3770fcfe64effe3c90a4d4692fa6_130_1.png)

Fig. 13. Blood-Tor system simulation results.

randomly. The time limit of uninfected cells was set to seven (in the previous case it was set at four iterations). If the number of iterations is smaller than 70, then the reproduction time can be chosen as 14 iterations. If the number of iterations is greater than or equal to 70, then the reproduction time decreases during the next iterations. If the number of iterations is greater than 90, then the number of uninfected cells placed at each iteration decreases. The result of this choice reflects the failure of the immunological system. That is, the immune system of the human individual loses the capacity to fight the viruses.

The BTS simulation results become, in this case, very close to actual HIV biological dynamics. They show strong qualitative similarities during all the natural history of HIV infection dynamics, as Figs. 11 and 14 clearly show.

![](img/55ff3770fcfe64effe3c90a4d4692fa6_131_0.png)

Fig. 14. Extended Blood-Tor system simulation results.

It is well known that AIDS is a disease that can be treated using appropriate drugs, but no absolute cure mechanism has been found yet. Some antiretroviral therapy uses reverse transcriptase inhibitors, others fight against an enzyme that is essential for the formation of infectious virus particles from infected cells called viral protease. All anti-HIV drugs aim at preventing the virus from reproducing, but they do not kill virus particles or infected cells (Nowak, 1999). Inspired in Zorzenon dos Santos & Coutinho (2001) CA model, Sloot et al. (2002) proposed a CA model incorporating drug therapy. Its main ingredients are destruction of previously emerged spatial patterns (wave-like and solid-like structures) and reconstruction of new spatial patterns (wave-like structures) due to incorporation of the drug therapy concept. The CA model integrates three different therapy procedures into one model and the simulations show a qualitative correspondence to clinical data. Shi et al. (2008) presented a CA model for HIV dynamics and drug treatment. It includes the virus replication cycle and mechanisms of drug therapy. Viral loads, its effect on infection rate, and the role of latently infected cells in sustaining HIV infection are among the aspects that are explored and incorporated in the model. The dynamics from the model qualitatively match clinical data. In the next section, we present the cellular automaton model for the HIV infection dynamics with antiretroviral therapy (Jafelice et al., 2009).

## 5. Cellular automata of the HIV evolution in the blood stream of positive individuals with antiretroviral therapy

The Blood-Tor-System, detailed in section 4, simulates the behavior of HIV infection dynamics in the blood stream of HIV positive human individuals who have not received any antiretroviral therapy. This section addresses the Bloodstream-Toroidal system when treatment is taken into account. Its purpose is to model and simulate the HIV dynamics in the blood stream of individuals subject to antiretroviral therapy.

To simulate the antiretroviral therapy the BTS system adopts fuzzy parameters due to the imprecise nature of how the individuals respond to the antiretroviral therapy. When accounting for antiretroviral therapy, the cellular automaton model assumes that the viruses do not infect all CD4+ cells because only a portion of CD4+ cells are usually infected. The period of virus replication is delayed, similarly as it happens in positive HIV individuals blood stream. The fuzzy parameters depend on the medication potency and on the adhesion of the individuals to the treatment. Adhesion to treatment means how individuals follow the correct medication prescription of the therapy. Adhesion is a very complex issue because it involves many factors that affect the ability of the individuals to comply with the antiretroviral therapy. Many factors can interfere in the regime prescribed, including the number of hours that individuals sleep, how strict they are with meals, medication schedules and how healthy their social life is. Information about medication potency can be obtained from medical doctors using their knowledge from clinical trials, clinical experience and knowledge published in the relevant literature. Along with clinical experience, the model increases the CD4+ level and decreases the viral load to simulate the antiretroviral therapy. The next subsection briefly reviews the concept of fuzzy set and fuzzy rule-based systems.

### 5.1 Basic concepts of fuzzy set theory

The literature on uncertainty has grown considerably during these last years, especially in the areas of system modeling, optimization, control, and pattern recognition. Recently, several authors have advocated the use of fuzzy set theory to address epidemiology problems (Barros et al., 2003; Jafelice et al., 2004; 2005; Ortega et al., 2003) and population dynamics (Krivan & Colombo, 1998). Since the advent of the HIV infection, several mathematical models have been developed to describe the HIV dynamics (Murray, 1990; Nowak & Bangham, 1996; Nowak, 1999). Here, we suggest the use of fuzzy set theory (Zadeh, 1965) to deal with the uncertain, imprecise nature of the virus dynamics.

First, we recall that a fuzzy set A on a universal set X is a membership function A that assigns to each element x of X a number A(x) between zero and one to indicate the degree of membership of x in A. Therefore, the membership function of the fuzzy set A is a function A : X → [0, 1]. It is interesting to note that a conventional set A on X is a particular instance of a fuzzy set for which the membership function is the characteristic function of A, that is, χ_A : X → {0, 1}.

Second, we remind the reader that a concept that plays a key role in fuzzy set theory is fuzzy rule-based systems (FRBS) (Pedrycz & Gomide, 1988). The structure of FRBS is shown in Fig. 15.

![](img/55ff3770fcfe64effe3c90a4d4692fa6_133_0.png)

Fig. 15. Structure of fuzzy rule-based systems.

A FRBS has four components: an input processor, a collection of fuzzy rules called fuzzy rule base (or rule base for short), a fuzzy inference machine, and an output processor. These components process real-valued inputs to provide real-valued outputs as follows.

- **Input Processor (Fuzzification).** Here, inputs are encoded into fuzzy sets on the respective universes of the input variables. For numerical inputs, the approach commonly used is to transform a real-valued input into a fuzzy singleton. Expert knowledge plays an important role to build the membership functions for each fuzzy set associated with the inputs.
- **Rule Base.** This is a knowledge-encoding component of fuzzy rule-based systems, a collection of fuzzy conditional propositions in the form of If-then rules. Fuzzy rules are an effective means to encode expert knowledge expressed through linguistic statements. In general, If-then rules describe relationships between linguistic variables such as *If adhesion to treatment is low and medication potency is high then period of virus reproduction is fast and percentage of infected CD4+ cells is high*. In fuzzy set theory, a variable (e.g. *adhesion to treatment*) whose value is a linguistic term (e.g. *low*) is called a linguistic variable (Pedrycz & Gomide, 1988).
- **Fuzzy Inference.** The fuzzy inference machine performs approximate reasoning using the compositional rule of inference. A particular form of fuzzy inference that is of interest in this paper is the Mamdani method (Mamdani, 1976; Mamdani & Assilian, 1999), derived from the max-min composition (Pedrycz & Gomide, 1988).
