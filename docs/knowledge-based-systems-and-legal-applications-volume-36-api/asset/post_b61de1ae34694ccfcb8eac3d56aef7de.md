
## Legal Applications of KBS

### 8.5.3. Constraints and policy goals

This work is an application and to some extent an extension of the work of Sadri and Kowalski on integrity constraints in deductive databases. The benefit system has been designed to achieve many aims. These aims are liable to change over time and with successive governments. To give an example, a policy goal might be: if claimant earns more than a certain amount of money he/she should not receive any-contributory benefits. Provided that these aims or goals can be expressed in a logical formalism they can be treated as integrity constraints on the system as a whole. Updates to the knowledge base can be checked to ensure they are not inconsistent with these policy goals. This provides a machine assessment of the acceptability of an amendment to the knowledge base. For further information on the work see [Kowalski et al. 1987].

### 8.5.4. Support for knowledge base revision

This arose out of the work on the policy planner done for the feasibility prototype. An important task done by policy officers is to develop alternative solutions to problems that have been identified. Prototype 3 provides no support for this. Work was started on a tool to aid the policy officers in the task of finding edits that would achieve the stated goal. This is the structure within the rules to generate a tree of possible solutions. No attempt is made to assess the suitability of these solutions since this is the function of the existing parts of the prototypes. The scenario for the use of this system is that once the problem has been clearly identified and in association with the user generate a set of possible solutions. The user would then create an environment with each of the more reasonable solutions. The effects of these changes could then be experimented to ensure that other policy goals were not invalidated.

### 8.5.5. Extensions to the argumentation formalism

Work was planned for the final six months of the project to look into extensions of the argumentation form as to better support the construction of macro-arguments and meta-arguments. It was also expected that some progress could be made on turning arguments in the form into readable English text. The prolonged illness of the researcher who was to have done this meant that the work could not be pursued. However, a subsequent project led by Logica and partially supported by the UK Department of Trade and Industry, is looking at the use of argumentation in the design of safety critical software and will be looking at extensions to the argumentation form developed in the Alvey-DHSS Demonstrator.

## 8.6. THE FUTURE FOR DSS POLICY FORMULATION SUPPORT

The prototypes developed in the course of this project have, we believe, quite convincingly demonstrated the feasibility of providing this kind of advanced decision support for DSS policy makers. Nevertheless, there are many more aspects to the support that could be offered that are not apparent in P3 which we have given some, and sometimes consider-thought to. In this final section we consider some of before presenting our view of what an installed DSS policy formulation system might look like.

### 8.6.1. What to do with P3

Firstly, there are several sections of the functionality of P3 which were specified but were not implemented due to lack of programming resource. It would be possible to do further development to P3 to add the facility to use arguments in our argument format as queries to the logical model of the legislation. This would leave it still incomplete. To finish P3, the missing two stages of the policy process, evaluation and rationalization, would need to be added. There are also several more query types that should be implemented (such as compare, and statistics). The rule base revision tool specified for P3 could then be added to complete the specified functionality.

### 8.6.2. P4

Beyond the additions mentioned above, which would be necessary to finish P3, there are several extra facilities that could be included go beyond the P3 specification. We might think of a system with these additional features as P4. We can think of the extra features of P4 as being either developments to the P3 functionality or additions to P3. In the "developments" category we might have:

- 1. Improvements to the argument form. At present this allows the construction of networks (chains) of micro-arguments. Chains as well as micro-arguments are labelled and can be used in other arguments permitting a degree of meta-argumentation. There is no support for the construction of higher-level (macro) arguments, and there is no use of qualifiers in micro-arguments and is no typing of micro-arguments. All of these things are possible and it is possible to conceive of a support system making good use of such features.

- 2. More support for evaluation. In the present design, the evaluation stage is by far the most poorly supported. It is possible to add a higher degree of automation if we have a more developed argument form. Arguments of certain types (arguments from authority, say) could be ranked as of inherently lower validity than others (logical arguments, for instance), Argument qualifiers could form the basis of a Ranking. The attaching of cost and benefit weightings could also support automatic evaluation, and so on.

- 3. Support for solution generation. The planner in P0 and the rule base revision tool specified for P3 are both attempts to provide support for the policy-maker to select optimal changes to the legislation so as to effect a policy option. Neither is an ideal solution: the planner it relies heavily on heuristic knowledge that is inherently hard to maintain and the rule base revision tool, despite its generality, because its functionality is limited and probably quite difficult for a policy maker to use. A more generalized approach along the lines of the planner supported by guidance from the user might give a sufficiently powerful form of support.

- 4. Interaction with the logical model in English. The project has done some work on the expression of the knowledge base and of results from queries in a restricted English. For this side of the system to be more acceptable and useful to policy makers, more effort is required to enable English input and output when querying and editing the legislative model. To do this properly is beyond the state of the art but it is likely that a great deal can be achieved by making interaction the system's formalism painless for the user.

- 5. Improved support for problem structuring. P2 and P3 allow only strictly hierarchical decomposition of problems. This may be a useful discipline for the production of a final problem structure (in fact, this is one of the intuitions which motivated the design of KANT) but there are probably earlier stages in problem structure development where a looser format and more freedom to experiment with structures could be useful. There are also organizational and administrative functions which might usefully be included at this stage (e.g. circulation lists, access privileges to subproblems, etc.).

As well as these developments from the P3 'baseline' there are also a number of areas in which P3 offers no support whatsoever but we know that support would be required in an operational system. In particular, we might single out:

- 1. The storage and retrieval of arguments. Policy-makers would find this facility extremely valuable and it could lead to a considerable cost advantage. A putative P4 would need to address the issues involved in the management of large volumes of structured argumentation of which will contain text, some logic and some mixture. There will be some of this material which will need to be maintained with its links to the current legislation, past legislation and the past and present versions of the knowledge base. Links to a variety of other textual material (such as reports, commissioners' decisions, etc.) will also need to be maintained.

- 2. The process of commitment and maintenance of the knowledge base.
