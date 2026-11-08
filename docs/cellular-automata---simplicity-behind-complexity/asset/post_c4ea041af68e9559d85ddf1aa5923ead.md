
- Common Dynamic Structure of Canada Lynx Populations Within Three Climatic Regions, *Science* 285(5430): 1071–1073.
- Stenseth, N. C., Falck, W., Chan, K.-S., Bjørnstad, O. N., O’Donoghue, M., Tong, H., Boonstra, R., Boutin, S., Krebs, C. J. & Yoccoz, N. G. (1998). From patterns to processes: Phase and density dependencies in the Canadian lynx cycle, *Proceedings of the National Academy of Sciences of the United States of America* 95(26): 15430–15435.
- Strain, M. C. & Levine, H. (2002). Comment on “dynamics of HIV infection: A cellular automata approach”, *Phys. Rev. Lett.* 89(21): 219805.
- Ueda, H., Iwaya, Y., Abe, T. & Kinoshita, T. (2006). A cellular automata model considering diversity associated with HIV infection, *Artificial Life and Robotics* 10: 73–76.
- Wangersky, P. J. (1978). Lotka-Volterra population models, *Annual Review of Ecology and Systematics* 9(1): 189–218.
- Yazdanpanah, Y. (2009). Multidrug resistance: a clinical approach, *Current Opinion in HIV & AIDS* 4(6): 499–506.
- Ying, H., Lin, F., MacArthur, R., Cohn, J., Barth-Jones, D., Ye, H. & Crane, L. (2007). A self-learning fuzzy discrete event system for HIV/AIDS treatment regimen selection, *Systems, Man, and Cybernetics, Part B: Cybernetics, IEEE Transactions on* 37(4): 966–979.
- Zadeh, L. A. (1965). Fuzzy sets, *Information and Control* 8(3): 338–353.
- Zhang, Z., Tao, Y. & Li, Z. (2007). Factors affecting hare-lynx dynamics in the classic time series of the Hudson Bay Company, Canada, *Climate Research* 34(2): 83–89.
- Zorzenon dos Santos, R. M. & Coutinho, S. (2001). Dynamics of HIV infection: A cellular automata approach, *Phys. Rev. Lett.* 87(16): 168102.

## CA in Urban Systems and Ecology: From Individual Behaviour to Transport Equations and Population Dynamics

José Luis Pualifito  
*Universidad de Mendoza*  
*Argentina*

### 1. Introduction

One way of seeing Cellular Automata (CA) is as cell-based computational models for describing the evolution of spatially distributed systems. Each cell represents a “local” state of the system that can vary according to its past states and to the present states of a “vicinity” of cells, following some set of relations known as “transition rules”.

More important than how these transition rules are (i.e. linear, non linear, discrete, etc.), is that distant parts of such system can interact one to another only through its neighbours; in other words, what we are actually considering in CA models, is that the system obeys the *principle of locality*. For this seems to be the case of most systems in nature, CA models have found potential applicability in a wide variety of phenomena, ranging from macroscopic scales, like urban systems, down to microscopic scales like in solid state physics. J. F. Nystrom (2001) has even argued in favour of the idea that fundamental laws of physics should arise from simple transition rules of some Universal CA, in a structured space following R. Buckminster Fuller’s synergetic geometry.

This brings us to a central point, which is that, in nature, space is as essential as time for describing any process; disregarding if we are more interested in watching at the temporal behaviour of certain group of state variables or if we are more interested in taking static pictures of some distributed properties in space, there will be always a spatiotemporal evolution process taking place behind.

A good example are urban and environmental systems; social scientists have been discussing since long ago how population and economy of regions interact and evolve through the years, while geographers and urban analysts have been doing it looking at its spatial structures. Both have contributed in equal parts to our present understanding of sustainable development. However, can economists explain development without considering where was located the infrastructure support? or can urbanists explain the structure of a city without considering the historical circumstances? Both views tend to describe one aspect of the evolution looking at the other as frame constrains, usually given in terms of literal stories. The same happens in many other fields of science treating with complexity.

A more modern view stands on the growing availability of informatics tools, and pushes towards constructing spatiotemporal models. But this is not a simple task; most attempts flow amongst “top-down” approaches, based on continuity equations in partial derivatives - including fractional order diffusion equations for explaining behaviours with long-range dependency (Angulo J.M. et al. 2001)- and “bottom-up” approaches, mostly given by discrete rule-based CAs (Park S. and Wagner D. F., 1997). While the former go more for the classic type, which puts emphasis in an extensive view of the system (that is in its behaviour and consistency as a whole), the latter are more of the evolutionary type, giving more emphasis to a detailed view, trying to describe self-organization and innovation proper of complexity.

However, as discrete space-time models have become more attractive, due to the intensive use of dynamical raster GIS (Geographic Information Systems) (Batty, M; 1996; Mitas L. 1997 et al.; Park S. and Wagner D. F., 1997), different kinds of CAs, as well as seamless discrete-continuous approaches, are opening new theoretical avenues.

For instance, as regards mobile agent-based CAs, the number of agents (population) grows initially from implanted “seeds” reproducing and spreading on the back cells, in accordance with transition rules and information on their development capability held in different GIS layers (Batty M. and Torrens P., 2001).

Not far from these, some seamless continuous/discrete approaches face the modelling problem in terms of a particle-field duality, just as in the path sampling method used in physics for solving continuity equations (Mitasova, H. and Mitas L., 2000). Multidimensional complexity can be treated herein by means of particles and fields in different scales. Likewise, some approaches use spatiotemporal convolution equations with kernels limited in space (i.e., Gaussian or similar), or even space-variant kernels (heterogeneous) (Wilde C., 2001), in a way that complex spatiotemporal processes are described as the propagation of dispersive or non-dispersive wave packets.

The distinctive feature of the seamless and mobile agent-based CAs models is that they use particles - or rather pseudo-particles - as an attempt to match the continuum response of an extensive view with the discrete and evolutionary behaviour of a detailed view; these can be considered as descriptions halfway between classical physics kinetics and unstable system dynamics. Issues to be primarily considered herewith are: a reduction in the amount of information involved, the interlacing of layers or embedding of contributing models, as well as the setting of scales for representative particles of the included processes.

The modelling of ecological systems offers also good examples; the emergence of complex spatiotemporal patterns in the population dynamics of certain species has been since long time of great interest in Ecology. Random walking and diffusion equations are used to describe the movement of animals in their own environment, and to forecast their spatial distribution under the influence of the diverse territorial heterogeneities (Jeanson R. et al., 2003). Such models are founded on a regular basis but there is still a long conceptual way to go.

Complex spatiotemporal patterns in the activities carried out by some social insects, such as ants and termites, reveal that individuals can collectively do better at performing tasks than isolated. This is not only observed in the typical pattern scales, usually far larger than the size of individuals, but also in their shape, featuring arrangements in various delicate and regular structures. Despite individual randomness and limitations, collective structures arise effectively in response to several functional and adaptive requirements (protection against predators, the substrate of social life and reproduction, thermal regulation, etc.) (Theraulaz G. et al., 2003).

Twenty years of research have revealed that the origin of hierarchical complexity is more a consequence of the multiplicity of individual responses to stimuli, derived of relatively
