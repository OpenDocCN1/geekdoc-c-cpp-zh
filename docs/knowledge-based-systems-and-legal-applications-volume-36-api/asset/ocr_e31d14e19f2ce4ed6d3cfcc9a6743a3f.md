# The Representation of Law in Computer Programs

with developing practical aids, normally to help in the analysis of legal problems which are primarily governed by case law.

This section describes two early projects which have attempted to combine reasoning by rules with the decisions of previous cases. Both were conducted as doctoral projects. They are Jeffrey Meldman's study in the tort of assault and battery [Meldman 1975, 1977; see also Cook et al. 1981], and Anne Gardner's treatment of offer and acceptance in contract law [Gardner 1983, 1984, 1985]. As mentioned in the historical overview, they can be wisely considered together. Other projects investigating techniques for reasoning with case law are described separately in 1.15 and 1.16.

# 1.15. Meldman

Jeffrey Meldman, in his doctoral project at MIT, designed a system to perform a 'simple kind of legal analysis' on cases involving assault and battery [Meldman 1975, 1977; see also Cook et al. 1981]. The analysis was based on a (tiny) fictitious body of legal sources Corpus Juris Mechanicum (CJM) extracted from a standard textbook on tort by Prosser. The sources comprised a collection of 'legal doctrines' and a set of cases and their decisions. Both were to be represented in the same way, in a kind of semantic network. The user would present a semantic network describing some hypothetical set of facts and the system would determine the extent to which these facts 'fell within legal doctrines by syllogism' (applied its rules to the facts) or 'near to these doctrines by analogy.' (Meldman was careful to stress that his system supported a very simplified form of analogy.) During this process, the system would ask the user for any additional facts that it needed to perform the analysis. It would then report its conclusions, justified by reference to the legal sources in CJM.

Meldman's system was designed to be executed by a system called OWL [Szolovits et al. 1977], though it was never implemented. Later, a program based on Meldman's design was implemented by King [1976] who placed more emphasis on reasoning by analogy than Meldman did originally.

There are three main features that characterize Meldman's system: the nature of the legal sources represented, the choice of representational formalism, and the general approach to legal analysis and the treatment of case law specifically.

A standard text like Prosser's on tort has a special status in (English and American) common law systems. It presents the author's commentary and personal analysis of some area of law, and therefore is only a secondary source of law; but eventually it is referred to extensively and takes on such authority that it becomes effectively the source in its particular area. It contains a collection of the most