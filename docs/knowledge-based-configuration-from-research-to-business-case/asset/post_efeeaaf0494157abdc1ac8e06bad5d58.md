
to be detected at a very early stage and, equally importantly, ensures that the configurations remain stable from one version to the next. This feature is particularly important for railway applications, where all installations—and therefore all changes to existing installations—must run through intensive quality assurance and validation procedures.

There are two groups of regression tests: small test cases, which test partial configurations with respect to one constraint each (typically designed during development), and large test cases comprising many different features in order to get a high coverage of various configurations and values (typically designed by the integration team at the start of the project). Of course, all these tests must be checked and possibly adapted when change-requests are implemented in a new version.

The advantages of using a standard IDE (integrated development environment) such as Eclipse are exploited: It supports knowledge engineering with state-of-the-art editors (code completion, diagrams, etc.), debugging facilities, test environment, and version control.

Iterative and incremental processes for knowledge engineering are important practices to guarantee customer satisfaction and high quality. In particular, they are necessary for correctly modeling the domain and product details as information from various sources has to be integrated: written technical specifications for the numerous parts of the configurable product, (tacit) knowledge of all involved engineers, different languages and representations (e.g., semistructured natural language, logical, graphical). Thus, the early and continuous involvement of domain experts during development of the configurator is crucial for success.

## 16.5 Results

The amount of configurator code concerning the core task of knowledge representation and reasoning is often overestimated. In the configurator described in this chapter, the model and constraints comprise only about 20% of the source code. The rest of the code deals with the user interface (UI), the generation of outputs (BOMs, documents, CAD drawings, manufacturing plans, etc.), and testing of the whole application.

The layered architecture facilitates reuse considerably. The code size of a typical variant is approximately 10% of the whole application code (a small value, considering that railway companies in different countries have quite different requirements). Standardizing the model and UI (i.e., omitting those packages in the variant layer or reducing them to customization via tables or only overriding certain constraints) has reduced the number of code lines for variants by 40%. Thus, the development time of variants could be significantly reduced as well.

Constraints help the user to avoid mistakes, reducing integration cycles and system test time. Rules and solving steps create objects and set values automatically, leading to productivity increases for the user by a factor of 10 and higher, compared to configuration tools used earlier:

- For a specific country variant, the configuration effort of the first version of an interlocking system could be reduced from eight to two weeks.
- A similar speed-up of 70% for the core configuration process was evaluated in a study of the Siemens business unit responsible for a new type of interlocking system in a country where several stations had to be equipped. They compared the tool for the new technology (which included tables with customer information) with an existing tool for a similar technology.
- With the help of the configurator variant for a new axle counter system (developed in less than a year’s work), the degree of automation with solvable constraints and rules was so high that 95% of the configuration could be derived within a few seconds, once the station layout had been drawn in the tool (requiring only a few hours’ work). Although such a system is much smaller than an interlocking system, it still consists of 50 classes with 300 attributes and associations and 200 constraint definitions. Average configurations consist of 2,000 instances, 30,000 variables, and 30,000 constraint instantiations.

Multistep upgrades have reduced development time for the upgrade by an estimated 50% of the upgrade coding time, as well as the users’ time for upgrading configurations to 1/N for each upgrade, N being the difference between source and target version numbers (i.e., the number of single-step upgrades).

## 16.6 Conclusion

The sections above have presented the rationale and impacts of using product configuration technologies in a configurator framework for large-scale industrial systems (railway interlockings). All in all, development could be accelerated compared to an alternative where only standard object-oriented programming languages would have been used:

- Multiple usage of constraints (for checking, filtering, explanation, and repair) as well as their compact format reduced the size of the corresponding code parts by approximately 30%.
- Maintenance is easier due to the declarative representation of the constraints (separation from solving algorithms).
- Schema evolution and automatic database upgrade could be implemented more easily.
- Training time of new knowledge engineers was reduced to approximately one half.
- Compared to an analogous rule-based system, an estimated 20% of bugs were avoided.

Thus, configuration technologies can definitely help to reduce project costs.

## References

Asikainen, T., Männistö, T., Soininen, T., 2006. A unified conceptual foundation for feature modeling. In: 10th International Software Product Line Conference (SPLC 2006), IEEE Computer Society, Baltimore, MD, pp. 31–40.

Falkner, A., Fleischanderl, G., 2001. Configuration requirements from railway interlocking stations. In: 17th International Joint Conference on Artificial Intelligence (IJCAI-2001), Configuration Workshop, Seattle, WA, pp. 15–17.

Falkner, A., Haselböck, A., 2013. Challenges of knowledge evolution in practice. AI Communications 26 (1), 3–14.

Falkner, A., Haselböck, A., Schenner, G., Schreiner, H., 2007. Benefits from three configurator generations. In: Innovative Processes and Products for Mass Customization (Proceedings of the joint conference of the International Mass Customization Meeting 2007 (IMCM’07) and International Conference on Economic, Technical and Organizational Aspects on Product Configuration Systems (PETO’07). Series on Business Informatics and Application Systems, vol. 3. GITO, pp. 89–103.

Fleischanderl, G., Friedrich, G.E., Haselböck, A., Schreiner, H., Stumptner, M., 1998. Configuring large systems using generative constraint satisfaction. IEEE Intelligent Systems 13 (4), 59–68.

Friedrich, G., Ryabokon, A., Falkner, A.A., Haselböck, A., Schenner, G., Schreiner, H., 2011. (Re)configuration based on model generation. Second Workshop on Logics for Component Configuration (LoCoCo 2011), Perugia, Italy, pp. 26–35.

Haselböck, A., Schenner, G., 2014. S'UPREME. In: Felfernig, A., Hotz, L., Bagley, C., Tiihonen, J. (Eds.), Knowledge-based Configuration – From Research to Business Cases. Morgan Kaufmann Publishers, Waltham, MA, pp. 263–269 (Chapter 22).

## Tacton: Use of Tacton Configurator at FLSmidth

Klas Orsvärn* and Morten H. Bennick†
*Tacton, Stockholm, Sweden
†FLSmidth, Copenhagen, Denmark

Abstract: FLSmidth is a leading vendor of equipment for cement plants, with a long experience of using software to support product configuration in making proposals as well as in order processing. This paper describes their experience implementing Tacton Configurator, integrated with various other systems such as SolidWorks 3D CAD, SmartPlant 3D, Mathcad, and legacy ERP. Integration was found to be a critical success factor. Other critical success factors were the use of a powerful constraint-solver engine as well as product experts dedicated to configuration modeling. We describe the identified business benefits such as improved productivity, shorter lead times, standardization, higher quality, and increased market share.

## 17.1 Introduction

FLSmidth is the world’s leading supplier of complete cement plants, as well as a leading supplier of plants and equipment for minerals processing. We begin by describing the company and its business. We briefly describe their previous experiences of using configurators and why Tacton Configurator was chosen to replace them. One critical success factor was the use of a powerful constraint-solver, thus, we describe the advantages and some of the important requirements of such a configurator. The company has appointed a dedicated team of engineers to take care of most of the configuration modeling. Integrations to related business and engineering systems are important for reaching the full benefits of configuration systems (Tiihonen and Soininen, 1997). We describe the integrations of FLSmidth at a high level. Finally, we describe the identified business benefits and draw some conclusions.

## 17.2 FLSmidth Company Introduction

Headquartered in Copenhagen, Denmark, FLSmidth employs approximately 14.000 people around the world, most of whom are engineers. Although most of the products are designed by FLSmidth, most of its manufacturing is outsourced to suppliers.

FLSmidth strives continually to improve efficiency and quality. For that reason, the company has been at the forefront of industrial equipment vendors in using software to support engineering and handling of product data. FLSmidth has acquired a lot of companies that supply related equipment, which exemplifies a strong trend in the industrial equipment sector; to consolidate and become a one-source supplier of a complete end-to-end manufacturing process solution. This also means that staff
