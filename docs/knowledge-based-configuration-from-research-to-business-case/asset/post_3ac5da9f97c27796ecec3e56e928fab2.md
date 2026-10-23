
consequences of assignments to other variables and the order of variable assignments does not affect constraints. Nowadays, basic constraint technologies are provided by open source constraint libraries such as CHOCO, JACOP, and MINION.

A major characteristic of many configuration domains is the need of component-oriented configuration knowledge representations (Mittal and Frayman, 1989). In order to assure the maintainability of the configuration model, component types and their relationships are treated as first class entities within an object model; that is component types and relationships are not represented as variables and constraints but as component types and generic constraints (see Hotz et al., 2014).

Without any claim to completeness, we want to mention the following “early” environments that supported a component-oriented knowledge representation: COSSACK (Frayman and Mittal, 1987), (Wright et al., 1993), COCOS (Stumptner et al., 1994), Beologic (Skovgaard, 1996), Trilogy (Franke, 1996), Selectica, Caméléon (Aldanondo et al., 2000), SAP (Haag, 1996), and further developments of the PLAKON configurator (Cunis et al., 1991; Günter and Cunis, 1992; Neumann, 1988; see also Haag, 2014).

## 2.3 Mainstream Configuration Environments

Today, component-oriented technologies are widely used for the representation and solving of configuration tasks. Promising results with the early systems and a cut in prices by several orders of magnitude due to the transition from classic AI environments to mainstream environments triggered further developments (and also redevelopments), which ended in industrial-strength configuration environments such as Tacton (Orsvärn and Axling, 1999), ConfigIT (Moeller et al., 2001), EngCon (further development of KONWERK; see Hotz and Günter, 2014; Ranze et al., 2002), and ILOG; see Junker and Mailharro, 2003; Mailharro, 1998. At the same time, configuration environments were increasingly integrated into ERP (enterprise resource planning) solutions; examples are SAP (Haag, 1998), BAAN (Yu and Skovgaard, 1998), and ORACLE. ERP systems and supply chain integration made configuration a mainstream technology simply due to the fact that ERP systems were already widely used.

Complex configuration tasks need *generative configuration approaches*; this is the generation of components (instances of component types) and corresponding constraints (instances of generic constraints) on demand. This capability is a further development of early component-oriented configuration approaches. Component-oriented knowledge representations and generative problem solving are crucial for complex domains such as telecommunication (Fleischanderl et al., 1998; Stumptner et al., 1998,

- ³ www.emn.fr
- ⁴ www.osolpro.com
- ⁵ minion.sourceforge.net
- ⁶ www.trilogy.com
- ⁷ www.selectica.com
- ⁸ www.cameleon-software.com
- ⁹ www.sap.com
- ¹⁰ Chapter 27.
- ¹¹ Chapter 24.
- ¹² Now: www.ibm.com
- ¹³ www.oracle.com

![](img/214a17cc1f5bbf0914497c7414128438_36_0.png)

FIGURE 2.2

Siemens railway interlocking hardware.

![](img/214a17cc1f5bbf0914497c7414128438_36_1.png)

FIGURE 2.3

Example of gear drives that are parts of drive control systems arranged and dimensioned by the DSD (Drive Solution Designer) configurator. DSD is implemented with the configuration tool EngCon (see Krebs, 2014, Chapter 23). Such drives are used for printing and sorting machines or automated saws. The variability in these domains stems from a large number (thousands) of different engines, gears, controllers, and other components and their variants.

1994), railway interlocking (see Falkner and Schreiner, 2014¹⁴), cabin-layouts (Kopisch and Günter, 1992), the automotive industry (Pargamin, 2002), and drive systems (Ranze et al., 2002). Most of these configuration environments do support generative problem solving. A screenshot of railway interlocking hardware is depicted in Figure 2.2; drive systems are shown in Figure 2.3.

The increasing size and complexity of configuration models (and corresponding configurations) triggered the development of further technologies. Approaches such as binary decision diagrams (BDDs; Andersen et al., 2010) and solution automata (Amilhastre et al., 2002) allow efficient reasoning especially in nongenerative configuration settings. Diagnosis and repair algorithms help users to overcome inconsistent situations (Felfernig et al., 2012; Junker, 2004; Sinz et al., 2007) in an efficient fashion (Card et al., 1991). Increasing model complexity triggered the development of graphical development and test environments that helped to increase understandability and maintainability of configuration knowledge bases (Aldanondo et al., 2000; Felfernig, 2007; Felfernig et al., 2004, 2000, 2013b; Haug, 2010). Today’s commercial environments provide graphical notations that allow the formulation of partonomies, taxonomies, and related constraints (sometimes also denoted as business rules).

In addition to constraint-based approaches, Answer Set Programming (ASP) became a paradigm for configuration knowledge representation (Aschinger et al., 2012; Friedrich et al., 2011; Myllyniemi et al., 2005; Simons et al., 2002; Soininen et al., 2001; Tiihonen et al., 2003, 2013). ASP maps a logic-based configuration model onto propositional logic theories and solves them with SAT-solvers (see Hotz et al., 2014).¹⁵ Due to a first order logic-based knowledge representation, ASP allows a component-oriented representation of configuration tasks, and thus is a potential alternative to constraint-based approaches. The configuration system WeCoTin (Tiihonen et al., 2013) was implemented on the basis of this technology and tested against several application domains. The commercial version of WeCoTin is VariSales—(see Tiihonen and Anderson, 2014).¹⁶

## 2.4 Mass Customization Toolkits

The goal of mass customization is to efficiently provide customers with what they want, when they want it, and at a competitive price (see Piller and Blazek, 2014).¹⁷ This widespread business requirement triggered the demand for technologies that intelligently support customers (end users) in autonomously configuring (codesign) products and services that fit their wishes and needs. Configurators deployed in such application scenarios are often referred to as mass customization toolkits (Aldanondo and Vareilles, 2008; Franke and Piller, 2003).

Enabling customers to configure products and services on their own triggered the development of personalization technologies that provide services such as the automated recommendation of parameter values, whole (sub-) configurations, and questions of interest for the user (Ardissono et al., 2003; Chevaleyre et al., 2007; Cöster et al., 2002; Domshlak et al., 2000; Falkner et al., 2011; Felfernig and Burke, 2008; Felfernig et al., 2013a; Stegmann et al., 2003; Tiihonen and Felfernig, 2010). Furthermore, configurators were enabled to recommend alternative parameter settings in situations where no solution

¹⁴ Chapter 16.
¹⁵ Chapter 6.
¹⁶ Chapter 26.
¹⁷ Chapter 9.

could be found for the given set of customer requirements (Felfernig et al., 2009, 2012; Junker, 2004; Sinz et al., 2007). For an overview of the application of recommendation technologies in configuration scenarios refer to Tiihonen et al. (2014).¹⁸ An example of a mass customization toolkit is mi adidas,¹⁹ which supports the configuration of individualized shoes (see Piller and Blazek, 2014).

Besides supporting customers in finding products and services that fit their wishes and needs, mass customization toolkits are also exploited for the identification of new requirements emerging in the customer community. On the one hand, such requirements can be derived by analyzing customer interactions with the mass customization toolkit, and on the other hand, customers themselves can be integrated into a company’s new product development processes. Both of these approaches exploiting customer knowledge for new product development are related to the concept of open innovation (Chesbrough, 2003); that is to systematically integrate customers into a company’s value chain. A nice example of an open innovation toolkit is introduced by Piller et al. (2004), who present a community-based environment for the cooperative development of computer games. In this context, an open innovation toolkit supports the generation of new game components without the need of programming knowledge.

## 2.5 Conclusion

In this chapter, we provided an outline of configuration-related historical developments. These developments can be briefly characterized as follows:

- From initial applications as rule-based expert systems,
- Via early model-based configurators, which allow a clear separation of domain knowledge and problem-solving knowledge,
- To mainstream model-based configuration environments integrated in supply chains and ERP systems,
- And mass customization toolkits.

The history of configuration reflects many different developments that ultimately lead to industrial strength configuration technologies. As such, configuration can be seen as one of the most successful application areas of Artificial Intelligence technologies.

We are aware of the fact that not all configuration-related developments could be considered in this chapter, and refer you to further related work, for example, on resource-based configuration (Heinrich and Jüngst, 1991; Jüngst and Heinrich, 1998), functional approaches (Stein, 1995), description logic-based configuration (McGuinness and Wright, 1998; Wright et al., 1993), hybrid configuration (Günter, 1995; Hotz, 2009; Junker and Mailharro, 2003; McGuinness and Wright, 1998; Wright et al., 1993), and related topics that are discussed in Chapter 3. For further historical remarks, refer to overviews such as Forza and Salvador (2002), Günter and Kühn (1999), Jannach et al. (2007), Sabin and Weigel (1998), Soininen et al. (1998), and Stumptner (1997).
