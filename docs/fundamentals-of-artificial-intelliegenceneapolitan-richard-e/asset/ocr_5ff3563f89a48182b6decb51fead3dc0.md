or how humans have come to understand language. You are referred to a text such as [Pinker, 2007] for a discussion of these matters. Rather, we take a pragmatic, operational approach. We assume that we have some knowledge base concerning known facts about the domain of discourse. For example, if the domain of discourse is the blocks world in Section 4.2.2, then the knowledge base might contain the fact on(a,b), which means block a is on block b. We need to make the knowledge base understand our sentences in the sense that a declarative sentence can be interpreted as a concept that can be added to the knowledge base, and a question can be converted to a query that can be presented to the knowledge base, which can then be answered. For example, in the blocks world if you tell the system, “The block labeled c is on the table,” the system should understand this sentence and add on(c,table) to the knowledge base. If you ask the system, “What block is on block b,” the system should understand this question and answer a if on(a,b) is in the knowledge base. In the credit card domain, if you ask, “What is the balance on my account,” the system should understand this query, look up your balance, and report it to you. The “answer” can be an action. For example, if you ask “Can I speak to an operator,” the system should answer by routing you to an operator.

There are several steps involved in understanding a declarative sentence (or question). They are as follows:

+   1. **Parsing**: This step analyzes the syntactic structure of the sentence by verifying that it is syntactically correct, and by identifying the linguistic components and relationships such as subject, verb, and object. Parsing produces a **parse tree** that represents these relationships.
+   
+   2. **Semantic Interpretation**: This step produces a representation of the meaning of the sentence from the parse tree. We call this representation a **concept**.
+   
+   3. **Contextual Interpretation**: This step incorporates the concept into the knowledge base.

The relationships among these steps are shown in Figure 15.1. We discuss each step in turn.

# 15.1 Parsing

The sentence is parsed using a **grammar**, which is set of rules that determine the composition of clauses, phrases, and words in a language. We present our grammars using **Backus-Naur Form (BNF)**. A BNF grammar consists of the following:

+   1. A set of **terminal symbols**. These are the words in the language such as “block”, “on”, “speak”, and “operator”.
+   
+   2. A set of **nonterminal symbols**. These symbols represent linguistic concepts that categorize phrases in the language such as *NounPhrase* and *VerbPhrase*.