$D = \{CV, D_1, D_2, \ldots, D_n\}$ of domains and a function $Dom$ that maps pairs of the form *(property name, type)* to elements of $D$. The sets $D_1, D_2, \ldots, D_n$ are called *atomic domains* (i.e., they contain numeric or symbolic values, but are distinct from $CV$). The name of a property variable is composed from the name of the originating component and the property name; for example, if property $p \in P$ is defined for component $c \in CV$, then the property variable is named $c.p$. Finally, $\Gamma$ is a finite set of generic constraints including activation and resource constraints.

GCSP representations allow the definition of *ports* that represent connection points between different components. In GCSPs ([Stumptner et al., 1998](#)), ports are represented by properties (attributes) that permit other components as values. *Partonomies* (part-of structures; see [Subsection 6.3.2](#)) can be represented on the basis of such port definitions. *Inheritance relationships* (related to a generation hierarchy) are represented on the basis of (generic) constraints that refer to component type domains.

*Example GCSP component type.* A component type $PC$ (P) can be represented as follows using a GCSP-style notation (see, e.g. [Stumptner et al., 1998](#)). This definition of the basic properties of a PC is related to the graphical configuration model depicted in [Figure 6.7](#). As can easily be seen, GCSP approaches have a more intuitive knowledge representation, which is inspired by object-oriented data models combined with constraints (see, e.g., [Bowen and Bahler, 1991](#); [Neumann 1988](#); [Puget and Albert, 1991](#)).

```
PC P DESCRIPTION:
    P.name := [String];
    P.price := [Integer];
    P.usage := {'internet','scientific','multimedia'};
    P.efficiency := {'A','B','C'};
    P.PORTS := {screen-of-pc-1[Screen], screen-of-pc-2[Screen],
    hdunit-of-pc-1[HDUnit], ...};
    P.screens := <screen-of-pc-1,screen-of-pc-2>;
    P.mb := <mb-of-pc-1>;
    P.hdunits := <hdunit-of-pc-1,hdunit-of-pc-2>;
```

GCSP constraints are represented in the context of a specific component type. As such this approach is very similar to constraint-including object-oriented languages such as the Unified Modeling Language (UML) ([Booch et al., 2005](#)) that includes the Object Constraint Language (OCL; [Warmer and Kleppe, 2003](#)). For an overview of the application of UML and OCL for configuration knowledge representation refer to [Felfernig (2007)](#) and [Felfernig et al. (2000a)](#). An example of a UML-based configuration model is introduced in [Subsection 6.3.2](#).

*Example GCSP constraint.* A GCSP constraint that describes the fact that the energy efficiency required by the user must be supported by the motherboard $mb$, can be represented as follows. This example shows how constraints can “navigate” through the component partonomy defined for the GCSP.

```
PC P DESCRIPTION:
    P.efficiency = P.mb.efficiency;
```

Usually, GCSP environments include a graphical front end that helps to define the configuration model more easily in an object-oriented fashion. Such an abstraction level improves the quality of