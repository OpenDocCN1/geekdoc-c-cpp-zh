
+   13. G. Leugering. Domain decomposition of an optimal control problem for semi-linear elliptic equations on metric graphs with application to gas networks. *Applied Mathematics*, 8:1074–1099, 2017.
+   14. Günter Leugering, Alexander Martin, Martin Schmidt, and Mathias Sirvent. Nonoverlapping domain decomposition for optimal control problems governed by semilinear models for gas flow in networks. *Control and Cybernetics*, 46(3):191–225, 2017.

Taylor & Francis
Taylor & Francis Group
http://taylorandfrancis.com

## 3

## A Model to Assess the Role of Spatial Urban Configurations on Crowd Evacuation Dynamics During Terrorist Attacks

D. Provitolo, R. Lozi, and E. Tric

## CONTENTS

3.1 Introduction: Modern Terrorist Attacks........................................................................41
3.2 Weighted PCR System: A Model for Analyzing the Dynamics of Human Behavior During a Disaster........................................................................44
3.2.1 Network of Squares and Streets Modelling Spatial Urban Configurations ........44
3.2.2 Equations of the WPCR System on Each Node ......................................................45
3.2.3 Transitional Dynamics..............................................................................................47
3.3 Coupled WPCR System on a Network.............................................................................48
3.3.1 Flows and Bottleneck Coupling...............................................................................48
3.3.2 Fixed Points of the Three-Node System ...............................................................51
3.4 Influence of the Spatial Configuration on the Pace of Evacuation ..............................56
3.4.1 Scaling the Parameters............................................................................................56
3.4.2 Influence of the Intermediate Place Capacity on the Evacuation Dynamics......56
3.5 Conclusion ......................................................................................................................58
Acknowledgments ...............................................................................................................58
References............................................................................................................................59

### 3.1 Introduction: Modern Terrorist Attacks

Terrorism has always existed in history and has taken different forms: anarchist attacks, political attacks, or attacks by colonial states, such as the terrible Jallianwala Bagh massacre, which took place on April 13, 1919 in Amritsar, Punjab, when a crowd of non-violent protesters were fired upon by troops of the British Indian Army.

In this article we focus specifically on the behavior of populations facing new forms of terrorism, such as the attacks perpetrated by sects, groups or “lone wolves” that are becoming more and more prevalent. Three types of acts can be distinguished:

- Shooting and bombing attacks, for example in bus and subway stations (Madrid, Spain, 2004; Paris, France, 1995, 2015; Nigeria, 2014; Belgium, 2016; Kashmir, 2019), at airports (Brussels airport, 2016; Atatürk airport, 2016), in urban areas with simultaneous terrorist acts (Mumbai, India, 2008, with 12 coordinated shooting and bombing attacks lasting four days).
- Attacks using CBRN (chemical, biological, radiological, and nuclear weapons) such as the sarin gas attack on the Tokyo subway committed by the Aum sect (March 20, 1995) (Dauphiné and Provitolo 2013).
- Ad hoc weapons are now being employed, such as suicide planes flown into the World Trade Center (2001), lorries or cars that are simply driven directly through a crowd massed for a cultural event or strolling peacefully. This is in response to tightened police controls aiming to reduce bombing attacks. These attacks are most often led by “lone wolves,” who are difficult to detect beforehand and equally difficult to locate because they are “nested” among civilians. On July 14, 2016, 86 people who attended the Bastille Day fireworks on the “Promenade des Anglais” in Nice, France, were killed; 458 more were wounded.

These attacks, perpetrated in crowds, in frequented places, or on public transport at rush hour, give rise to diversified human reactions. One can observe behaviors of sideration (paralysing panic), of flight panic, of agitation in all directions, of reasoned flight, of sheltering, or mutually offered assistance (Crocq 2013), etc.

Except for sideration, sheltering and escape behaviors, whether taken under the influence of panic (flight panic) or of reason (reasoned escape), produce trajectories of displacement. When an attack happens, the topography of the area is also very important. The dynamics of human reactions and the associated displacements are indeed guided by the space and the alternatives that it offers, as displayed in Figure 3.1, especially in terms of evacuation, flight, and accessibility to refuge areas, such as safe places and squares.

There are few data available to identify the dynamics of the displacements associated with these behaviors. Of course, it is difficult to artificially reproduce a disaster, which would otherwise allow us to observe the diversity of human reactions that could occur, to follow the spatio-temporal dynamics, and to analyze the impact of spatial configurations on these dynamics. To overcome these limits, it is possible to develop mathematical models from which hypotheses are tested by means of a human behavior computer simulation model.

The Com2SiCa research team* proposed the Panic–Control–Reflex (PCR) model (Provitolo et al. 2015), as shown in Figure 3.2, which is a model that simulates the possible human behavior that can occur during sudden onset and unpredictable disasters, such as

![](img/81c56bc4b2fca1951aff5e0ab85b66be_64_0.png)

FIGURE 3.1
Street and places in Mediterranean city of Italy. (© D. Provitolo, March, 2019. With permission.)

* https://geoazur.oca.eu/en/research-geoazur/2158-com2sica-how-to-comprehend-and-simulate-human-behaviors-in-areas-facing-natural-disasters

## FIGURE 3.2

Graphic representation of the Panic-Control-Reflex behavior model (PCR) in the exceptional situation of disaster. (D. Provitolo et al. 2015. With permission.)

terrorist attacks. This model is formed by a system of ordinary differential equations to describe behavioral dynamics over time (Verdière et al. 2014, 2015, Cantin et al. 2016).

Neuroscience research explains that during a disaster, humans are rarely stuck in one type of behavior. The population switches between different behavioral states, some of which are the result of instinctive, others of reasoned, reaction.

As the brain switches from one behavioral state to another, in the context of terrorist attacks and therefore in a situation of sudden and unforeseen threat, the entire impacted population first adopts a behavioral reaction, Reflex r(t), under the influence of surprise and the suddenness of the event, before transiting to the Panic reflex behavior p(t), or Controlled behavior c(t) (Provitolo et al. 2015). Reflex r(t) and Panic p(t) behavior are managed by the reptilian brain: they are instinctive, automatic reactions, allowing one to react extremely quickly to the threat, either by being stunned and paralyzed r(t), or by fleeing as quickly as possible due to the panic fear p(t). Controlled behavior c(t) is managed by the pre-frontal cortex, which concerns reasoned and self-control reactions. These can take different forms during a catastrophe, for example, in the form of evacuation, escape, containment, sheltering, search for help, mutual aid, or, on the contrary, looting, etc. Despite their diversity, the PCR model aggregates all of these controlled behaviors.

In this article we propose an extension of the PCR model in order to take into account the influence of spatial configuration in the mathematical modeling of the dynamics of human reactions in the face of traumatic situations, such as terrorist attacks. We call this extended model the Coupled Weighted PCR (CWPCR).

In Section 3.2, we will present the Weighted Panic Control Reflex model in its graphic and mathematical form, as published by the Com2SiCa research team. This model is improved from the PCR model in order to take into account the role of spatial configurations on behavioral dynamics. In Section 3.3 we introduce the CWPCR model, which
