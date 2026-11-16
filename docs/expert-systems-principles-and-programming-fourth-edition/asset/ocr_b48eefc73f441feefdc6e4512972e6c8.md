# Figure 4.21 Some Types of Graphs

![](bbox=[0.05, 0.09, 0.88, 0.42])

analogy to a space is the scope of a module or package in a structured language. For example, the Figure 4.18 FRE node can be considered a space with structure shown in Figure 4.19.

The power of semantic nets comes in modeling statements. In fact, Hendrix first developed them for expressing natural language in his Ph.D. dissertation. Statements are like the propositions of evidence and hypotheses that make up the nodes of inference nets. As a simple example of a partitioned semantic net for a statement, consider “there is a computer with a color screen.” Notice that this is an existential statement because of the “there is” quantifier.

Figure 4.22 shows the partitioned semantic net expression of this statement using three spaces. SPACE-1 consists of some general related concepts about computers. SPACE-2 consists of the particular computer we are talking about, which has been given the identifier COMPUTER-1. SPACE-3 consists of the specific relation COMPONENTS-OF-1, which has as its object the specific COLOR-SCREEN-1 that we are concerned about. Each arc labeled element shows that one state is an element of another. The arc labeled entity shows which specific computer is the entity with the specific color screen.

The advantage of a partitioned semantic net is shown by a portion of a PROSPECTOR rule for STIR using FMGS evidence as shown in Figure 4.23. The rule can be stated as “If there is an entity named E-1 whose cardinality is ABUNDANT and is composed of INTRUSIVE ROCKS, then the consequent is the rule of Suggestive Texture of Igneous Rocks.” Note that the diagram has been simplified by not including the requirement that the antecedent also have a fine to medium grain size.