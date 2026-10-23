
## FIGURE 24.1

KONWERK knowledge base browser: specialization hierarchy (left) and one selected concept.

![](img/214a17cc1f5bbf0914497c7414128438_313_0.png)

browser (see Figure 24.2), the elaboration net (an incrementally increasing net of partly configured objects; Figure 24.3), and the agenda (Figure 24.4).

KONWERK is written in Common Lisp (Steele, 1984), CLOS (Common Lisp Object System; Keene, 1989, including the Metaobject Protocol; Kiczales et al., 1991), and CLIM (Common Lisp Interface Manager)¹³ for the user interface.

¹³bauhh.dyndns.org.

## FIGURE 24.4

KONWERK agenda browser: configuration steps are listed with the step type (left), the property (middle), and the instance (right).

![](img/214a17cc1f5bbf0914497c7414128438_316_0.png)

## FIGURE 24.5

The cabin-layout configurator XKL, which allows the placement of cabin equipment like seats, kitchens, toilettes in view of customer wishes, technical constraints, legal constraints, and optimality criteria. This application mainly considered configuration with spatial aspects.

![](img/214a17cc1f5bbf0914497c7414128438_316_1.png)

interpretation system (the configurator) to generate high-level interpretations such as “place-cover” or “lay-dinner-table-for-two” (see Hotz and Neumann, 2005, and Figure 24.6).

The heterogeneity of the considered applications, which include several of the specified aspects, ensure the usability of KONWERK for a wide range of application problems.

![](img/214a17cc1f5bbf0914497c7414128438_317_0.png)

## FIGURE 24.6

Example of a scene interpretation constructed with KONWERK. Gray observed objects (one plate, two saucers, and one cup) and iconified hypothesized objects with possible spatial positions computed by component and constraint models describing dish-layouts. Taken from Hotz and Neumann (2005).

## 24.6 Conclusion

This chapter provides an overview of the hybrid configuration system KONWERK. By combining several knowledge representation and reasoning techniques, KONWERK can be used for complex configuration applications. Experiences gained with KONWERK can be summarized as: Quick prototype creation, high acceptance of the knowledge base, and no application-specific user interface.

## Acknowledgments

Besides the authors, main contributors for the core modules of KONWERK were Frank Buhr, Bernd Neumann, Manfred Kopisch, and Thomas Vietze. Project partners contributed in enhancement modules and applications.

## References

Baader, F., Calvanese, D., McGuinness, D.L., Nardi, D., Patel-Schneider, P.F. (Eds.), 2003. The Description Logic Handbook: Theory, Implementation, and Applications. Cambridge University Press, New York, NY.

Cunis, R., Günter, A., Strecker, H. (Eds.), 1991. The PLAKON-Book. Informatik-Fachberichte, vol. 266. Springer, London (in German: Das PLAKON-Buch).

Felfernig, A., Reiterer, S., Reinfrank, F., Ninaus, G., Jeran, M., 2014. Conflict detection & diagnosis in configuration. In: Felfernig, A., Hotz, L., Bagley, C., Tiihonen, J. (Eds.), Knowledge-based Configuration – From Research to Business Cases. Morgan Kaufmann Publishers, Waltham, MA, pp. 73–87 (Chapter 7).

Funke, B., Müller, K., Sebastian, H.-J., Thaerigen, M., 1994. Innovative design by integration of expert system technology with multi-criteria decision making and fuzzy systems. In: Moving Towards Expert Systems Globally in the 21st Century, 2nd World Congress on Expert Systems. Cognizant Communication Offices, Lisbon, Portugal, pp. 263–272.

Gülden, O., Hotz, L., 1997. Integrating resource-oriented and structure-oriented configuration with KONWERK. In: 11th Workshop Planen und Konfigurieren (PuK-97) im Rahmen der 4. Deutschen Tagung Wissensbasierte Systeme (XPS-97). Bad Honnef.

Günter, A., 1995. Knowledge-based Configuration (Wissensbasiertes Konfigurieren). Infix, St. Augustin, Germany (in German).

Günter, A., Cunis, R., 1992. Flexible control in expert systems for construction tasks. Journal of Applied Intelligence 2 (4), 369–385.

Günter, A., Hotz, L., 1995. Conflict resolution with knowledge-based backtracking and repair-statement. In: Günter, A. (Ed.), Wissensbasiertes Konfigurieren. Infix, St. Augustin, pp. 181–192 (in German: Auflösung von Konfigurationskonflikten mit Wissensbasiertem Backtracking und Reparaturanweisungen).

Hollmann, O., Wagner, T., Günter, A., 2000. EngCon: a flexible domain-independent configuration engine. In: 14th European Conference on Artificial Intelligence (ECAI 2000), Configuration Workshop, Berlin, Germany, pp. 94–96.

Hotz, L., 2000. Frame-based Knowledge Representation for Configuration, Analysis, and Diagnoses of Technical Systems. Dissertation, University of Hamburg, Germany (in German: Frame-basierte Wissensrepräsentation für Konfigurierung, Analyse und Diagnose technischer Systems).

Hotz, L., Neumann, B., 2005. Scene interpretation as a configuration task. Künstliche Intelligenz 3, 59–65.

Hotz, L., Wolter, K., 2013. Beyond physical product configuration – configuration in unusual domains. AI Communications 26 (1), 39–66.

Hotz, L., Wolter, K., 2014. Smarthome configuration model. In: Felfernig, A., Hotz, L., Bagley, C., Tiihonen, J. (Eds.), Knowledge-based Configuration – From Research to Business Cases. Morgan Kaufmann Publishers, Waltham, MA, pp. 121–135 (Chapter 10).

Hotz, L., Wolter, K., Krebs, T., Deelstra, S., Sinnema, M., Nijhuis, J., MacGregor, J., 2006. Configuration in Industrial Product Families – The ConPF Methodology. IOS Press, Berlin, Germany.

Hotz, L., Felfernig, A., Günter, A., Tiihonen, J., 2014a. A short history of configuration technologies. In: Felfernig, A., Hotz, L., Bagley, C., Tiihonen, J. (Eds.), Knowledge-based Configuration – From Research to Business Cases. Morgan Kaufmann Publishers, Waltham, MA, pp. 9–19 (Chapter 2).

Hotz, L., Felfernig, A., Stumptner, M., Ryabokon, A., Bagley, C., Wolter, K., 2014b. Configuration knowledge representation and reasoning. In: Felfernig, A., Hotz, L., Bagley, C., Tiihonen, J. (Eds.), Knowledge-based Configuration – From Research to Business Cases. Morgan Kaufmann Publishers, Waltham, MA, pp. 41–72 (Chapter 6).

Jannach, D., Zanker, M., Felfernig, A., Friedrich, G., 2010. Recommender Systems: An Introduction. Cambridge University Press.

Keene, S.E., 1989. Object-Oriented Programming in Common Lisp: A Programmer’s Guide to CLOS. Addison-Wesley, Boston, MA.

Kiczales, J., Bobrow, D.G., des Rivières, J., 1991. The Art of the Metaobject Protocol. MIT Press, Cambridge, MA.

Kopisch, M., Günter, A., 1992. Configuration of a passenger aircraft cabin based on conceptual hierarchy, constraints and flexible control. In: Belli, F., Radermacher, F. (Eds.), Industrial and Engineering Applications of Artificial Intelligence and Expert Systems (IEA/AIE-92). Lecture Notes in Computer Science, vol. 604. Springer, Paderborn, pp. 421–430.

Krebs, T., 2014. encoWay. In: Felfernig, A., Hotz, L., Bagley, C., Tiihonen, J. (Eds.), Knowledge-based Configuration – From Research to Business Cases. Morgan Kaufmann Publishers, Waltham, MA, pp. 271–279 (Chapter 23).

Kühn, C., 2000. Modeling structure and behaviour for knowledge based software configuration. In: Sauer, J. (Ed.), 14th Workshop, New Results in Planning, Scheduling and Design (PuK2000), Berlin, Germany.

Mackworth, A., 1977. Consistency in networks of relations. Artificial Intelligence 8 (1), 99–118.

Marcus, S., Stout, J., McDermott, J., 1987. VT: an expert elevator designer that uses knowledge-based backtracking. AI Magazine 8 (4), 41–58.

Mittal, S., Frayman, F., 1989. Towards a generic model of configuration tasks. In: 11th International Joint Conference on Artificial Intelligence (IJCAI-89), vol. 2, Detroit, MI, pp. 1395–1401.

Neumann, B., 1988. Configuration expert systems: a case study and tutorial. In: Bunke, H.O. (Ed.), Proceedings of the 1988 SGAICO Conference on Artificial Intelligence in Manufacturing, Assembly, and Robotics. Oldenbourg, Munich, pp. 27–68.

Oehler, P., 2000. Knowledge-based construction of mixed analog/digital systems. Dissertation, J.W. Goethe-Universität, Frankfurt, Germany (in German: Wissensbasierte Konstruktion gemischt analog/digitaler Systeme).

Oehler, P., Grimm, C., Waldschmidt, K., 2002. A methodology for system-level synthesis of mixed-signal applications. IEEE Transactions on Very Large Scale Integration (VLSI) Systems 10 (6), 935–942.

Pfitzer, K., 1993. Case-based configuration of technical systems (Fallbasierte Konfigurierung technischer Systeme). Künstliche Intelligenz 7/93, 24–30.

Ricci, F., Rokach, L., Shapira, B., Kantor, P., 2011. Recommender Systems Handbook. Springer.

Rossi, F., vanBeek, P., Walsh, T. (Eds.), 2006. Handbook of constraint programming. Foundations of Artificial Intelligence. Elsevier, Amsterdam, The Netherlands.

Schröder, C., Möller, R., Lutz, C., 1996. A partial logical reconstruction of PLAKON/KONWERK. In: Baader, F., Bürckert, H.-J., Günther, A., Nutt, W. (Eds.), Proceedings of the Workshop on Knowledge Representation and Configuration WRKP’96. No. D-96-04 in DFKI Documents, pp. 55–64.

Schumann, S., Schumann, O., 2008. Modeling uncertainty with the configuration tool KONWERK. In: Steinmuller, J., Langner, H., Ritter, M., Zeidler, J. (Eds.), 15 Years Artificial Intelligence at the TU Chemnitz. Chemnitzer Informatik-Berichte, TU Chemnitz, pp. 33–44.

Sebastian, H.-J., 1996. Intelligent systems for configuration problems. In: Sebastian, H.-J., Antonsson, E. (Eds.), Fuzzy Sets in Engineering Design and Configuration. International Series in Intelligent Technologies, vol. 9. Springer, US, pp. 89–232.

Steele, G.L.J., 1984. COMMON LISP: The Language. Digital Press, Bedford, MA.

Tiihonen, J., Felfernig, A., Mandl, M., 2014. Personalized configuration. In: Felfernig, A., Hotz, L., Bagley, C., Tiihonen, J. (Eds.), Knowledge-based Configuration – From Research to Business Cases. Morgan Kaufmann Publishers, Waltham, MA, pp. 167–179 (Chapter 13).

Tsang, E., 1993. Foundations of Constraint Satisfaction. Academic Press, London, San Diego, New York.

Wolter, K., 2003. Supporting the orientation and navigation of users in the process of configuring complex products. Master’s thesis, Universität Hamburg, Fachbereich Informatik, Hamburg (in German: Unterstützung der Orientierung und Navigation von Benutzern im Prozess der Konfiguration von komplexen, variantenreichen Produkten).
