
![](img/67fa924962ee21b3590be9f3b10d9fe7_473_0.png)

Figure 15.9 A derivation of the semantic interpretation on(a,b) from the sentence “a on b”.

Applying this predicate to “b” we have the following:

```
on(x,b) = λyλx on(x, y) (b).
```

Figure 15.9 shows the parse tree deriving the semantic interpretation on(a,b) from the sentence “a on b”.

We have shown how to hard-code semantic interpretations into the parse tree. Zelle and Mooney [1996] developed CHILL, which is a program that learns semantic interpretations from examples.

## 15.3 Concept/Knowledge Interpretation

Semantic interpretation of a sentence produces a unit of information such as the logical statement on(a,b). In the final step, concept/knowledge or contextual interpretation, the item of information is incorporated into the knowledge base. For example, suppose our world or knowledge base consists of two rooms, Room 1 and Room 2; Room 1 has a table and the blocks in that room are situated on the table as shown on the left in Figure 15.10; and in Room 2 has no table and the blocks in that room are situated as shown on the right in Figure 15.10. If our semantic interpretation is on(a,b), how do we know whether to place block a on block b in Room 1 or Room 2? Linguists handle the problem using the notion of a situation, which is a particular set of circumstances in the world. The situation keeps track of everything that has happened so far. In the current example, the situation includes not only the placement of the various blocks in the rooms, but also that the robot is currently in Room 1.

![](img/67fa924962ee21b3590be9f3b10d9fe7_474_0.png)

Contextual Interpretation

Figure 15.10 In the current situation, the robot is in Room 1.

So the contextual interpretation of on(a,b) is to place block a on block b in Room 1.

## 15.4 Information Extraction

We close with an application of language understanding, namely information extraction. An information extraction system takes as input a body of text, and extracts from it facts concerning pre-specified topics of interest. Figure 15.11 shows an example of how such a system proceeds. The purpose of this particular system is to extract information relative to the domain of natural disasters. The desired information is represented by a template that contains the precise attributes we want to retrieve. In this case they are as follows: Event, Date, Time, Location, Damage, Estimated Losses, and Injuries. In the example in Figure 15.11, the text consists of a paragraph that might appear

April 4 Dallas – Early last evening a tornado swept through an area northwest of Dallas, causing extensive damage. Witnesses confirm that the twister occurred without warning at approximately 7:15 pm and destroyed two mobile homes. The Texaco station at 102 Main street, Farmers Branch, Texas, was also severely damaged, but no injuries were reported. Total property damages are estimated to be $350,000.

Information Extraction System

| Event: | tornado |
| Date: | 4/3/2011 |
| Time: | 19:15 |
| Location: | Farmers Branch; northwest of Dallas; Texas; USA |
| Damage: | mobile homes (2); Texaco station (1) |
| Estimated Losses: | $350,000 |
| Injuries: | none |

Figure 15.11 An example of an information extraction system in the domain of natural disasters.

in the local newspaper about an earthquake in Dallas, and the information extracted consists of all the information about the earthquake.

After discussing the various useful applications of information extraction, we present an architecture for an information extraction system.

### 15.4.1 Applications of Information Extraction

Today information extraction often concerns mining desired facts from information appearing on the Web. Applications involve monitoring newspapers and other articles to learn details of natural disasters, terrorist events, political affairs, business ventures, scientific discoveries, etc. Another application involves summarizing free-form patient records to extract symptoms, test results, treatments, and diagnoses. Yet another application concerns the automatic classification of documents such as legal documents.

![](img/67fa924962ee21b3590be9f3b10d9fe7_476_0.png)

Figure 15.12 Architecture for an Information Extraction System.

### 15.4.2 Architecture for an Information Extraction System

Various approaches have been tried in the development of an information extraction system. At one extreme, systems were developed that simply performed keyword matching with no linguistic analysis at all. At the other extreme, systems processed the text using all the natural language understanding techniques developed in this chapter, including syntactic analysis, semantic interpretation, and contextual interpretation.

Cardie [1997] described what evolved as a standard architecture for an information extraction system. That architecture appears in Figure 15.12. We discuss each component of the architecture in turn.

- 1. Tokenization and tagging: In this step each word is disambiguated or tagged regarding its part of speech.
- 2. Sentence analysis: This stage performs syntactic analysis and finds and labels semantic entities relevant to each extraction topic. For example, in the natural disaster domain, the system identifies events, locations, names, injury expressions, time expressions, and money expressions. The goal of sentence analysis in an information extraction system is not to produce a complete parse tree as is the case in a standard natural language understanding program. Rather, the system does **partial parsing**, which involves only developing as much structure as is needed to accomplish the information extraction task. A partial parser looks for fragments of recognizable texts such as noun groups and verb groups.
- 3. Extraction: In the extraction phase, the system concentrates on identifying the information that is relevant to the particular domain. For example, in the natural disaster domain, it identifies events (tornado) and locations (“area” and “northwest of Dallas”).
- 4. Merging: In the merging phase, the system tries to resolve whether different entities discovered in the text are the same entity. For example, in the text concerning the tornado in Dallas, the system might resolve that “tornado” and “twister” refer to the same entity. The purpose here is to enable the system to associate information in two different statements with one entity. For example, in the case of the tornado, we have the text “a tornado swept...causing excessive damage,” and “the twister occurred without warning....and destroyed two mobile homes.” Once we identify that “tornado” and “twister” are the same entity, we know that the tornado caused excessive damage and destroyed the two mobile homes.
- 5. Template Generation: In the template phase, the extracted information is mapped to attributes required by the template.

Cardie [1997] discusses algorithms for implementing the architecture just presented.

## 15.5 Discussion and Further Reading

There is much more to the field of natural language understanding than the introduction provided here, both at theoretical and algorithmic levels. Two popular texts on the subject are [Allen, 1995] and [Jurafsky and Martin, 2009]. The former text had long been the standard, while the latter one is more current in that it covers the advances in statistical techniques that have occurred recently. Natural language understanding is a sub-field of **natural language processing (NLP)** , which concerns both understanding natural language input and producing natural language output. The latter text mentioned above, namely [Jurafsky and Martin, 2009], covers both aspects of NLP.

## EXERCISES

### Section 15.1

Exercise 15.1 Show that any context-free grammar can be transformed into a grammar in Chomsky normal form.

Exercise 15.2 Using the CFG in Table 15.1, parse these sentences and show the resultant parse trees:

- 1. A big man loves the monkey.
- 2. The fat monkey can read the right book.
- 3. The man loves the left and the monkey loves the right.

Exercise 15.3 Modify Algorithm 15.1 so that it produces a parse tree.

Exercise 15.4 Implement Algorithm 15.1 and use it to parse the sentences in Exercise 15.2

Exercise 15.5 Show two different parse trees for each of the sentences in Example 15.2.

Exercise 15.6 Using the grammar in Table 15.3, show the table produced by the CYK algorithm when parsing each of the following sentences:

- 1. y y x x x
- 2. x x y x x
- 3. x y y y y.

Exercise 15.7 Implement the CYK algorithm.

Exercise 15.8 Show that the time complexity of the CYK algorithm is \(\theta(mn^3)\), where \(m\) is the number of rules and \(n\) is the number of words in the sentence.

Exercise 15.9 Using the PCFG in Table 15.4, compute probabilities of the sentences in Exercise 15.2.

Exercise 15.10 Using the LPCFG in Table 15.5, obtain the parse tree and compute the probability of this sentence:

The man sleeps quiet.

### Section 15.2

Exercise 15.11 Augment the grammar in Table 15.1 with semantics, and use the augmented grammar to obtain semantics for the sentences in Exercise 15.2.
