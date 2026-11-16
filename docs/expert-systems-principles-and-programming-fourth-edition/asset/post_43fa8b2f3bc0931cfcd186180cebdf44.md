
between utility programs in the environment. Some tools do not even require the user to write any code. Instead, the tool allows a user to enter knowledge by examples from tables or spreadsheets and generates the appropriate code itself.

- shell—A special-purpose tool designed for certain types of applications in which the user must supply only the knowledge base. The classic example of this is the EMYCIN (empty MYCIN) shell. This shell was made by removing the medical knowledge base of the MYCIN expert system.

MYCIN was designed as a backward-chaining system to diagnose disease. By simply removing the medical knowledge, EMYCIN was created as a shell containing knowledge about other kinds of consultative systems that use backward chaining. The EMYCIN shell demonstrated the reusability of the essential MYCIN software such as the inference engine and user interface. This was a very important step in the development of modern expert system technology because it meant that an expert system would not have to be built from scratch for each new application. Today the field of expert systems tools is quite competitive with many features and GUIs available.

There are many ways of characterizing expert systems such as representation of knowledge, forward or backward chaining, support of uncertainty, hypothetical reasoning, explanation facilities, and so forth. Unless a person has built a number of expert systems, it is difficult to appreciate all of these features, especially those found in the more expensive tools. The best way to learn expert systems technology is to develop a number of systems with an easy-to-learn language and then invest in a more sophisticated tool if you need its features.

## 1.9 ELEMENTS OF AN EXPERT SYSTEM

The elements of a typical expert system are shown in Figure 1.6. In a rule-based system, the knowledge base contains the domain knowledge needed to solve problems coded in the form of rules. While rules are a popular paradigm for representing knowledge, other types of expert systems use different representations, as discussed in Chapter 2.

An expert system consists of the following components:

- user interface—the mechanism by which the user and the expert system communicate.
- explanation facility—explains the reasoning of the system to a user.
- working memory—a global database of facts used by the rules.
- inference engine—makes inferences by deciding which rules are satisfied by facts or objects, prioritizes the satisfied rules, and executes the rule with the highest priority.
- agenda—a prioritized list of rules created by the inference engine, whose patterns are satisfied by facts or objects in working memory.
- knowledge acquisition facility—an automatic way for the user to enter knowledge in the system rather than by having the knowledge engineer explicitly code the knowledge.

## Figure 1.6 Structure of a Rule-Based Expert System

![](img/2c460d4de56b7ffaad3834eee20beaa0_46_0.png)

The knowledge acquisition facility is an optional feature on many systems. In some expert systems tools, the tool can learn by rule induction through examples and automatically generate rules. Other methods such as ID3, C4.5, C5.1, artificial neural networks, and genetic algorithms have been used in machine learning to generate rules. The major problem with machine learning to generate rules is that there is no explanation as to why this was created. Unlike a human who can explain the reason for a rule, machine learning systems have never been able to explain their actions and so unpredictable results may occur. However, the examples are generally from tabular-spreadsheet-type data better suited to decision trees. General rules constructed by a knowledge engineer can be much more complex than the simple rules from rule induction.

Depending on the implementation of the system, the user interface may be a simple text-oriented display or a sophisticated high-resolution, bit-mapped display. High-resolution displays are commonly used to simulate a control panel with dials and displays.

The knowledge base is also called the **production memory** in a rule-based expert system. As a very simple example, consider the problem of deciding to cross a street. The productions for the two rules are as follows, where the arrows mean that the system will perform the actions on the right of the arrow if the conditions on the left are true:

```
the light is red -> stop
the light is green -> go
```

The production rules can be expressed in an equivalent pseudocode IF-THEN format as:

```
Rule: Red_light
IF
the light is red
THEN
stop
```

```
Rule: Green_light
IF
the light is green
THEN
go
```

Each rule is identified by a name. Following the name is the IF part of the rule. The section of the rule between the IF and THEN part of the rule is called by various names such as the antecedent, conditional part, pattern part, or left-hand-side (LHS). The individual condition:

the light is green

is called a conditional element or a pattern.

The following are some examples of rules from the classic systems:

### MYCIN system for diagnosis of meningitis and bacteremia (bacterial infections)

```
IF
The site of the culture is blood, and
The identity of the organism is not known with certainty, and
The stain of the organism is gramneg, and
The morphology of the organism is rod, and
The patient has been seriously burned
THEN
There is weakly suggestive evidence (.4) that
the identity of the organism is
pseudomonas
```

### XCON/R1 for configuring DEC VAX computer systems

```
IF
The current context is assigning devices to
Unibus modules and
There is an unassigned dual-port disk drive
and
The type of controller it requires is known
and
There are two such controllers, neither of
which has any devices assigned to it, and
The number of devices that these controllers can support is known
THEN Assign the disk drive to each of the controllers, and Note that the two controllers have been associated and each supports one drive
```

In a rule-based system, the inference engine determines which rule antecedents, if any, are satisfied by the facts. Two general methods of inferencing are commonly used as the problem-solving strategies of expert systems: forward chaining and backward chaining. Other methods used for more specific needs may include means-ends analysis, problem reduction, backtracking, plan-generate-test, hierarchical planning and the least commitment principle, and constraint hierarchy.

Forward chaining is reasoning from facts to the conclusions resulting from those facts. For example, if you see that it is raining before leaving home (the fact), then you should take an umbrella (the conclusion).

Backward chaining involves reasoning in reverse from a hypothesis, a potential conclusion to be proved, to the facts that support the hypothesis. For example, if you have not looked outside and someone enters with wet shoes and an umbrella, your hypothesis is that it is raining. In order to support this hypothesis, you could ask the person if it was raining. If the response is yes, then the hypothesis is proven true and becomes a fact. As mentioned before, a hypothesis can be viewed as a fact whose truth is in doubt and needs to be established. The hypothesis can then be interpreted as a goal to be proven.

Depending on the design, an inference engine will do either forward or backward chaining or both. For example, CLIPS is designed for forward chaining, PROLOG programs backward chaining, and the version of CLIPS called Eclipse developed by Paul Haley does both forward and backward chaining. The choice of inference engine depends on the type of problem. Diagnostic problems are better solved with backward chaining while prognosis, monitoring, and control are better done by forward chaining. However, there is a memory size and execution speed penalty involved in using a more enhanced tool since more code is involved in creating the tool. CLIPS was designed to be “lean and mean” so that it would execute as fast as possible and be suitable for deployed applications in small memory devices such as ROM. Although people who use desktop computers with 512 megs of RAM don’t normally think about this, developing a product such as an intelligent remote control or microwave oven requires ROM for cheap permanent memory. The cost of memory goes down with size so it is desirable to use as little memory as possible in consumer devices to be competitive. CLIPS can actually generate a C code executable that is small and easily burnt into a small ROM.

The working memory may contain facts regarding the current status of the traffic light such as “the light is green” or “the light is red.” Either or both of these facts may be in working memory at the same time. If the traffic light is working normally, only one fact will be in memory. However, it is possible that both facts may be in working memory if there is a malfunction in the light. Notice the
