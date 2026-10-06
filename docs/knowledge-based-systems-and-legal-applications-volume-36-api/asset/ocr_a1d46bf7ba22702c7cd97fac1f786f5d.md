# Legal Applications of KBS

represented. Whereas LOD analysts made KANT nodes for each proposition and logical connector, as a rule would be represented by a number of nodes, the AS knowledge base had whole rules represented in a single node. All nodes had a title field.

In nodes that contained rules, our analysis and formalisation of knowledge typically generated three other fields. The field containing the least formalized entry might contain text from the source, citation of the reference (title and page number), comments explaining these peculiarities of the knowledge, and reminders to the analysts about changes which had been made or needed to be made to the node. There was usually a field containing an English-like, semi-formal rule which was written to represent the knowledge in the original field faithfully. The third field contained the rule in the toolkit language.

The point of having the three fields juxtaposed and in the same node was to facilitate the inspection of the transformations through the three stages.

Towards the end of the project, when the facilities of KANT and KBB had been combined, an ICL colleague wrote a special 'patch' to make it also possible for our structures to have a fourth field in these nodes, one containing the compiled version of the rule. This meant we were able to inspect the rule we actually contained and compare it to the one we sent to the compiler. This enabled us to identify where, for mistakes in placing parentheses propositions had been disregarded by the compiler. It was far easier to detect these truncated rules through inspection than through the creation and running of test examples.

A complex system of KANT structures was developed. It was able to serve as a 'progress chasing'/version control tool. It was able to show increasingly fine granularity of rules, i.e. where propositions in one rule were elaborated by other rules representing the original rule and all which refined their proposition. Other structures were designed so that refining rules were 'children' of the top-level rule. Links were made between nodes where terms with crucial technical/legal meanings were used and nodes containing definitions for these terms. An effective glossary was theirs. It served not only to explain the meaning of terms but also as a check that the same meaning permeated throughout.

In some cases it was possible to make links between the original source material and nodes which made use of that material. We had not been given permission to make an on-line version of the CPAG handbook, so a reference to the books was given when material from that source was first introduced.

It's fair to say that KANT and KBB provided extremely useful