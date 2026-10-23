
often also dispose of concepts for structured rule representation. Graphical UML modeling supports the inclusion of advanced modularization concepts such as packaging and diagram contextualization (Felfernig et al., 2000b; Felfernig and Zanker, 2000). Techniques for easy knowledge base evolution and maintenance (C5) are not primarily depending on the knowledge representation itself but more on additional meta-functionalities that support intuitive knowledge navigation and adaptation; nearly all representation formalisms can be equipped with such a functionality (Felfernig et al., 2013b). RBS have serious maintenance problems due to the dependence of product domain and problem solving knowledge. With the exception of RBS, all other representations follow a model-based paradigm (C6) that supports a clear separation of domain and problem-solving knowledge. RBS and constraint satisfaction algorithms have proven to support efficient problem solving on an industrial scale. For this reason, these approaches are evaluated better with regard to performance (C7). GCSP allows the determination of solutions for generative configuration problems; ASP and HB are also able to provide such functionalities (C8). With the exception of FM and UML, all approaches provide basic support for explanations (as to why a configuration could (not) be found). Dependencies between domain and problem solving knowledge in RBS and encodings in SAT (see Subsection 6.2.1) make these approaches less accessible for explanation techniques.

## 6.6 Conclusion

In this chapter we provided an overview of different configuration knowledge representation and reasoning techniques. These techniques were discussed on the basis of a timeline ranging from the rule-based configuration system R1/XCON implemented in the late 1970’s via different types of constraint representations and constraint reasoning approaches through to advanced knowledge representation and reasoning approaches that are applied nowadays for the definition and solution of configuration tasks.

## Acknowledgments

The work presented in this chapter was partially funded by the Austrian research promotion agency (grant numbers: 827587 and 825071).

## References

Amilhastre, J., Fargier, H., Marquis, P., 2002. Consistency restoration and explanations in dynamic CSPs - application to configuration. Artificial Intelligence 135 (1–2), 199–234.

Andersen, H., Hadzic, T., Pisinger, D., 2010. Interactive cost configuration over decision diagrams. Journal of Artificial Intelligence Research 37, 99–139.

Baader, F., Calvanese, D., McGuinness, D.L., Nardi, D., Patel-Schneider, P.F. (Eds.), 2003. The Description Logic Handbook: Theory, Implementation, and Applications. Cambridge University Press, New York, NY.

Bacchus, F., vanBeek, P., 1998. On the conversion between non-binary and binary constraint satisfaction problems. In: 15th National Conference on Artificial Intelligence (AAAI’98). Madison, Wisconsin, pp. 311–318.

Felfernig, A., Schubert, M., Zehentner, C., 2012. An efficient diagnosis algorithm for inconsistent constraint sets. Artificial Intelligence for Engineering Design, Analysis and Manufacturing (AI EDAM) 26 (1), 53–62.
Felfernig, A., Benavides, D., Galindo, J., Reinfrank, F., 2013a. Towards anomaly explanation in feature models. In: Workshop on Configuration. Vienna, Austria, pp. 117–124.
Felfernig, A., Reiterer, S., Stettinger, M., Reinfrank, F., Jeran, M., Ninaus, G., 2013b. Recommender systems for configuration knowledge engineering. In: Workshop on Configuration. Vienna, Austria, pp. 51–54.
Fleischanderl, G., Friedrich, G.E., Haselböck, A., Schreiner, H., Stumptner, M., 1998. Configuring large systems using generative constraint satisfaction. IEEE Intelligent Systems 13 (4), 59–68.
Freuder, E., 1997. In pursuit of the holy grail. Constraints 2 (1), 57–61.
Friedrich, G., Jannach, D., Stumptner, M., Zanker, M., 2014. Knowledge engineering for configuration systems. In: Felfernig, A., Hotz, L., Bagley, C., Tiihonen, J. (Eds.), Knowledge-based Configuration – From Research to Business Cases. Morgan Kaufmann Publishers, Waltham, MA, pp. 139–155 (Chapter 11).
Gebser, M., Kaminski, R., Ostrowski, M., Schaub, T., Thiele, S., 2009. On the input language of ASP grounder Gringo. In: Erdem, E., Lin, F., Schaub, T. (Eds.), Proceedings of the 10th International Conference on Logic Programming and Nonmonotonic Reasoning. Lecture Notes in Computer Science, Vol. 5373. Springer, Potsdam, Germany, pp. 502–508.
Gelfond, M., Lifschitz, V., 1988. The stable model semantics for logic programming. In: Kowalkowski, R.A., Bowen, K.A. (Eds.), Logic Programming: Proceedings of the 5th International Conference and Symposium. Seattle, WA, pp. 1070–1080.
Giunchiglia, E., Lierler, Y., Maratea, M., 2006. Answer set programming based on propositional satisfiability. Journal of Automated Reasoning 36 (4), 345–377.
Gomes, C., Kautz, H., Sabharwal, A., Selman, B., 2008. Satisfiability solvers. In: Handbook of Knowledge Representation. Foundations of Artificial Intelligence, vol. 3. Elsevier, New York, NY, pp. 89–134 (Chapter 2).
Günter, A., Kühn, C., 1999. Knowledge-Based Configuration - Survey and Future Directions. In: Puppe, F. (Ed.), XPS-99: knowledge based systems, proceedings 5th biannual german conference on knowledge based systems. Lecture Notes in Artificial Intelligence, Vol. 1570. Springer, Würzburg.
Hotz, L., Günter, A., 2014. KONWERK. In: Felfernig, A., Hotz, L., Bagley, C., Tiihonen, J. (Eds.), Knowledge-based Configuration – From Research to Business Cases. Morgan Kaufmann Publishers, Waltham, MA, pp. 281–295 (Chapter 24).
Hotz, L., Neumann, B., 2005. Scene Interpretation as a Configuration Task. Künstliche Intelligenz 3, 59–65.
Hotz, L., Wolter, K., 2014. Smarthome Configuration Model. In: Felfernig, A., Hotz, L., Bagley, C., Tiihonen, J. (Eds.), Knowledge-based Configuration – From Research to Business Cases. Morgan Kaufmann Publishers, Waltham, MA, pp. 121–135 (Chapter 10).
Hotz, L., Wolter, K., Krebs, T., Deelstra, S., Sinnema, M., Nijhuis, J., MacGregor, J., 2006. Configuration in Industrial Product Families - The ConIPF Methodology. IOS Press, Berlin.
Jannach, D., Zanker, M., Felfernig, A., Friedrich, G., 2010. Recommender Systems: An Introduction. Cambridge University Press, MA.
Janota, M., 2008. Do SAT solvers make good configurators? In: First Workshop on Analyses of Software Product Lines (ASPL08) of 12th International Software Product Lines Conference (SPLC08). Limerick, Ireland, pp. 10–14.
Janota, M., Botterweck, G., Grigore, R., Marques-Silva, J., 2010. How to complete an interactive configuration process? In: 36th Conference on Current Trends in Theory and Practice of Computer Science (SOFSEM 2010). Lecture Notes in Computer Science, vol. 5901. Springer, Špindlerův Mlýn, Czech Republic, pp. 528–539.
Jüngst, W., Heinrich, M., 1998. Using resource balancing to configure modular systems. IEEE Intelligent Systems 13 (4), 50–58.

Sinz, C., Haag, A., Narodynska, N., Walsh, T., Gelle, E., Sabin, M., Junker, U., O’Sullivan, B., Rabiser, R., Dhungana, D., Grünbacher, P., Lehner, K., Federspiel, C., Naus, D., 2007. Configuration. IEEE Intelligent Systems 22 (1), 78–90.

Soininen, T., Tiihonen, J., Männistö, T., Sulonen, R., 1998. Towards a general ontology of configuration. Artificial Intelligence for Engineering Design, Analysis and Manufacturing (AI EDAM) 12 (4), 357–372.

Soininen, T., Niemelä, I., Tiihonen, J., Sulonen, R., 2001. Representing configuration knowledge with weight constraint rules. In: Provetti, A., Son, T.C. (Eds.), 1st International Workshop on Answer Set Programming: Towards Efficient and Scalable Knowledge (AAAI Technical, Report SS-01-01). pp. 195–201.

Soloway, E., Bachant, J., Jensen, K., 1987. Assessing the maintainability of XCON-in-RIME: coping with the problem of very large rule-bases. In: Proceedings of the Sixth National Conference on Artificial Intelligence (AAAI-87). Seattle, Washington, pp. 824–829 July 13–17.

Stumptner, M., 1997. An overview of knowledge-based configuration. AI Communications 10 (2), 111–126.

Stumptner, M., Friedrich, G., Haselböck, A., 1998. Generative constraint-based configuration of large technical systems. Artificial Intelligence for Engineering Design, Analysis and Manufacturing (AI EDAM) 12 (4), 307–320.

Terashima-Marin, H., Ross, P., Valenzuela-Rendon, M., 2008. Hyper-heuristics for the dynamic variable ordering in constraint satisfaction problems. In: Genetic and Evolutionary Computation Conference (GECCO’08). Atlanta, Georgia, pp. 571–578.

Tiihonen, J., Soininen, T., Niemelä, I., Sulonen, R., 2003. A practical tool for mass-customising configurable products. In: Proceedings of the 14th International Conference on Engineering Design, Stockholm, Sweden, August 19–21, 2003, CDROM, p. 10 (Paper number: 1290).

Tiihonen, J., Heiskala, M., Anderson, A., Soininen, T., 2013. WeCoTin – A practical logic-based sales configurator. AI Communications 26 (1), 99–131.

Tsang, E., 1993. Foundations of Constraint Satisfaction. Academic Press, London, San Diego, New York.

Warner, J., Kleppe, A., 2003. The Object Constraint Language: Getting Your Models Ready for MDA, second ed. Addison-Wesley Longman Publishing, Boston, MA.
