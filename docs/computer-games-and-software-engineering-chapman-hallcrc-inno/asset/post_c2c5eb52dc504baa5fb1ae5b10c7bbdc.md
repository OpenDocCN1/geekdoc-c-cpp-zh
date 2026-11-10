
![](img/8edd7838aa9e4a0d883fcf44f4b667a0_89_0.png)

FIGURE 3.7  A tailored tabular use case specification for the example Test Game.

## 3.3.3 Formal Model

### 3.3.3.1 XML

XML is a formal, textual, document markup language originally designed to easily distribute information across the World Wide Web (W3C 2006). XML has been selected for use in this work for the following reasons:

- *XML is formal and concise.* The specification for XML includes a formal grammar specification using Extended Backus–Naur Form notation. The grammar gives a comprehensive syntax for XML and provides a means for all XML documents to be checked for well-formedness. A well-formed XML document allows a parser that conforms to the XML grammar specification to parse and manipulate data from the document without error.

- **XML documents are human legible.** Because markup text in an XML document can be customized, the XML document may be written with descriptive names that allow humans to easily understand the type of data that is stored. Comments may also be used to provide further description within the document without impacting the syntax of the document. The feature is important because the XML documents may also serve as a record of the transformation to verify successful model transformation.

- **Writing programs to process XML documents is straightforward.** XML documents are text-based documents that can be parsed to extract data and manipulation as necessary. Many programming languages provide standard libraries for data manipulation in the XML documents.

- **XML supports a wide variety of applications.** XML is a widespread language now being used in multiple applications in multiple industries.

### 3.3.3.2 SimSYS XML Game Script

The tabular, semiformal notation is transformed into a single XML file that can be loaded into the SimSYS Game Play Engine. Part of the XML file is illustrated in Table 3.1; the XML schema definition for the game is defined. The transformation is done one part at a time, using tags to organize the content. For example, the Challenge's one question is related to subject-specific topics in SE Design and transferable skills described in the tabular specification (What kind of knowledge is in the Challenge?); these

**TABLE 3.1 XML Partial Representation of the Test Game Challenge**

```xml
1.1 ...
<!-- Act 1, Scene 1, Screen 1, Challenge 1 -->
<challengeStructure>
    <gameElement xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance" xsi:type = "prop">
    <gameElement xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance" xsi:type = "IDENTIFIER">
        <id> challenge1 </id>
    <challengeItemList>
    <item>
<!-- What kind of knowledge is in the challenge? -->
<domainKnowledgeList>
    <domainKnowledge>software engineering</domainKnowledge>
    <area>Software Design</area>
    <topic_list>
        <topic>General_Design_Concepts</topic>
        <topic>Context_of_Software_Design</topic>
        <topic>Software_Design_Process</topic>
        <topic>Software_Design_Re-use</topic>
    </topic_list>
</domainKnowledgeList>
<transferableKnowledgeList>
    <transferableKnowledge>analysis
    </transferableKnowledge>
    <transferableKnowledge>critical_thinking
    </transferableKnowledge>
    <transferableKnowledge>problem_solving
    </transferableKnowledge>
</transferableKnowledgeList>
<!-- How is the knowledge being assessed? -->
    <expression>dialog</expression>
    <learningTaxonomyList>
        <learningTaxonomy>knowledge</learningTaxonomy>
        <learningTaxonomy>application
        </learningTaxonomy>
    </learningTaxonomyList>
<!-- Challenge item-->
<!-- The challenge item has a stem, with zero or one
text (description or vignette), zero or more images,
and a question. -->
<!-- stem description-->
<stemDescription>
    <type>
        <typeName>InformationBox</typeName>
        <event>
            <eventName>NONE</eventName>
            <animation>FADEIN</animation>
            <time>QUICK</time>
        </event>
        <color>YELLOW</color>
        <location>UR</location>
    </type>
<!-- -->
<name> Option1 </name>
<location> UUL </location>
<color> Yellow </color>
<text> Strategy Pattern </text>
<!-- Hint -->
<type>
    <typeName> InformationBox</typeName>
    <name> Hint1 </name>
    <eventName> HOVER</eventName>
    <location> UUL </location>
    <color> Yellow </color>
    <text>The Strategy pattern defines a family
          of algorithms, encapsulates each one, and
          makes them interchangeable; algorithms are
          selected at runtime. It is a behavioral
          pattern. </text>
</type>
<!-- Evaluation -->
<evaluation> Incorrect </evaluation>
<!--Reward -->
<reward>NONE</reward>
<type>
    <!-- Feedback -->
    <typeName> MessageBox </typeName>
    <location> UC </location>
    <color> Yellow </color>
    <text>: Sorry - the correct answer is the
          bridge pattern</text>
</type>
</stemOption>
...
</stemOptionList>
</item>
...
</ChallengeItemList>
...
```

are represented in XML using two kinds of tags to define lists of topics (`<domainKnowledgeList>`, `<transferableKnowledgeList>`). The next tags define the assessment approach for the question, How is the knowledge being assessed? The question with four answer options—evaluation, hints, rewards, and feedback—follow in the XML file. Although the file is quite long, it is straightforward to read; the manual mapping from the semiformal tabular model to the XML is time consuming, but not too difficult.

## 3.4 CONCLUSIONS AND FUTURE WORK

The SimSYS approach to engineering SEGs is an iterative, three-step approach that is model based and integrates learning objectives from the earliest stages in the game development. The approach begins with an informal narrative, like a storyboard, which is subsequently transformed into a tailored semiformal UML use case model (with visual and tabular specifications) and finally into formal models. Our first formal model uses XML; the XML is the game specification that can be loaded and tested in the SimSYS Game Play Engine. In applying the three-step approach to engineering a collection of test games, we have found it to be straightforward, but labor intensive. In particular, the formal XML model required a significant amount of time to create; manually testing the games was also time consuming.

An Intelligent Automated Game Generation module is currently under investigation to alleviate the effort in populating the informal narrative and semiformal models (template instantiation) and automatically generate the XML models. We also plan to explore the transformation of the semiformal model into a statechart representation that can be loaded, animated, or simulated with the existing commercial tool support (e.g. IBM 2012), providing a complementary verification approach.

We recognize that the validation of the approach is limited to our preliminary prototyping work (symbolic test games, software engineering test games). Additional validation is needed, both by continuing our own project and by external educational game researchers and educators to explore issues such as the scalability of the approach to larger games and collections of related games.

## REFERENCES

- Abran, A., Moore, J.W., and Bourque, P. (2004). *Guide to the Software Engineering Body of Knowledge (SWEBOK): 2004 Version.* IEEE Computer Society, Los Alamitos, CA. Appendix D.

- Adams, E. (2010). *Fundamentals of Game Design.* 2nd edition. New Riders Publishing, Berkeley, CA.

- Anderson, Jr., E.G. and Morrice, D.J. (2000). Simulation game for teaching service-oriented supply chain management: Does information sharing help managers with service capacity decisions? *Production and Operations Management* 9: 40–55.

- Anderson, L. W., Krathwohl, D. R., et al. (Eds.) (2001). *A Taxonomy for Learning, Teaching, and Assessing: A Revision of Bloom's Taxonomy of Educational Objectives.* Allyn & Bacon (Pearson Education Group). Boston, MA.

- Braithwaite, B. and Schreiber, I. (2008). *Challenges for Game Designers.* Charles River Media, Boston, MA.

- Chen, F. and Samoengraja, R. (2000). The stationary beer game. *Production and Operations Management* 9: 19–30.

- Cooper, K. and Longstreet, C.L. (2012a). Towards model-driven game engineering for serious educational games: Tailored use cases for game requirements. *Proceedings of the IEEE 17th International Conference on Computer Games*, Louisville, KY, July 30–August 1, pp. 208–212.

- Cooper, K. and Longstreet, C.L. (2012b). Towards model-driven game engineering in SimSYS: Requirements for the Agile software development process game. Technical report, co-published UTDCS-06-12. The University of Texas at Dallas, Richardson, TX; MU-CII-01-12 Marquette University, Milwaukee, WI. March.

- Cooper, K., Nass, E., and Longstreet, C.L. (2014). Towards model-driven requirements engineering for serious educational games: Informal, semi-formal, and formal models. *Proceedings of the 20th International Working Conference on Requirements Engineering: Foundation for Software Quality*, Essen, Germany, April 7–10, pp. 17–22.

- Crookall, D. and Saunders, D. (Eds.) (1989). Toward an integration of communication and simulation. In *Communication and Simulation from Two Fields to One.* Multilingual Matters, Clevedon.

- Dantas, A.R., Barros, M.O., and Werner, C. (2005). Simulations models applied to game-based training for software project managers. *Process Simulation and Modeling Workshop*, St. Louis, MO, May 14–15, pp. 110–116.

- Dempsey, V.J., Haynes, L.L., Lucassen, B.A., and Casey, M.S. (2002). Forty simple computer games and what they mean for educators. *Simulation and Gaming* 33(2):157–168.

- Deterding, S., Dixon, D., Khaled, R., and Nacke, L. (2011). From game design elements to gamefulness: Defining "gamification". *Proceedings of the 15th International Academic Mindtrek Conference*, Tampere, Finland, September 28–30, pp. 9–15.

- Gee, J.P. (2003). *What Video Games Have to Teach Us about Learning and Literacy?* Macmillan, New York.
