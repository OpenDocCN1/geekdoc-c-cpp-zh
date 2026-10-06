
![](img/fd9daa466aa6610f0ebd57e2ccc632c5_246_0.png)

# Analysing texts for knowledge based systems

The one in Figure 11.1 showed the complexity of welfare provision. Three sectors (represented by bold ovals) provided welfare - central government, local government, and the private sector. All three were involved in education, health and housing (represented by the irregular outlines), the problems as our users might express them. Provision is made by 'cash', rebates or allowances, services and provision in kind. Distinctions such as 'medical needs' catered for by the NHS through 'health needs' catered for by the local authority social services department are likely to be a source of confusion about where to go for. The welfare world is complex, as here, without including most of the social security benefits.

This was one of the diagrams which made it apparent that there would be several kinds of knowledge needed in the Advice System knowledge base. Details about the features of the benefits - for example, the period payment covered, in that period a payment was made, whether there a limit to how low a benefit could be claimed, benefit rates and conditions of eligibility — were what we called 'static' knowledge. Static knowledge would be put in the system by the knowledge bases and altered only as a maintenance task typically when regulations or rules for benefits changed.

The system would hold this as a hierarchy of classes (with their attributes) and rules. This knowledge would not change during an advice session with a user and would be the same for all users. This knowledge was later referred to Gilbert's work on question and answer types [Gilbert 1987] as domain-level knowledge. Theory-level knowledge, knowledge about why the benefit system is as it is, would also be static knowledge in the sense the term is used here. Details relating to a particular person or claim could not be built into the system in the same way. It would not be the same for all users. There would have to be some mechanism to allow the user to put these details during an advice session. If, unlike the Advice System, a system were built with stored personal material, a mechanism would be needed to retrieve it from store or read it into the system until the user indicated what he or she wanted advice about. The objects which held this knowledge were instances of the class. This would alter during an advice session, thus dynamic knowledge seemed an appropriate label.

Personal characteristics, even persistent ones such as a person's sex, and historical information were dynamic in this sense. This was case-level information in Gilbert's scheme.

The procedural knowledge, relating to actions, was the third kind of knowledge identified. A design decision was made to have this knowledge handled by the planner rather than the inference engine underlying the toolkit which handled the dynamic and static knowledge. Procedural knowledge was, therefore, analysed separately. In the end, however, much of it was represented in the ‘non-procedural’ knowledge base, that contained static and dynamic knowledge characterized above, as classes and rules.

## Claiming a Welfare Benefit: part of the picture

| Personal Characteristics | | | |
| :--- | :--- | :--- | :--- |
| Historical | Current | | employment |
| | employment status | receiving | social security benefits |
| residence/nationality | marital status | provision from | other benefits |
| employment record | age | | other sources of income |
| benefit record | | | |
| contributions record | sex | | |
| | Persistent | A person | for general daily needs |
| qualifies as a claimant for benefit | | medical needs | food |
| | | finds self | health needs | best |
| | specifically satisfies criteria for a benefit | | housing needs | transport |
| | | in a situation | educational needs | clothing |
| recognised as on for | | | |
| which there is provision | PERCEIVES NEED | | |
| | | HAS NECESSARY KNOWLEDGE/SKILL | | |
| | | IS NOT INHIBITED | | |
| | | PERCEVES UTILITY | for |
| after waiting period | at appropriate | CIRCUMSTANCE STABLE | to the appropriate agency |
| close enough to event | time | makes a claim | not overlapping with one |
| reclaimed as necessary | giving appropriate | for the appropriate | the situation |
| in acceptable terms | information | benefit | - not disqualified if |
| supported by evidence required | in respect of | | fits present circumstances |
| adult dependent | | people whose | relative who died | self and dependents |
| self | people covered | situation is reason for | the benefit | best |
| | by payment | IF SUCCESSFUL | needing care |
| dependent child | | IF AWARD IS | | |
| day of unemployment/ 6 day week | receives benefit | up to 312 'linked' days (52 only) | a year (consecutive) |
| fortnight | | | short term 26 weeks |
| 7 day week | period which | period for which | long term |
| | benefit covers | benefit is payable | claimant not entitled |
| in advance | | until circumstances change | one off |
| the middle | paid in | (in payments) | daily |
| in arrears | | with frequency | quarterly |
| girocheque | | | | |
| order book | paid by | | | |
| direct credit | | | | person whose condition is reason for |
| features of the situation | | | changes personal condition |
| ending entering entirely | until | people for whom claim is | no longer covered |
| claimant changes personal attributes | | | entitlement runs out |
| | (the next cycle) | | |
| | | | | | | | |

Figure 11.2 Model of claiming a benefit

The complexity in the system and in the claiming process led to a search for a model which would provide order on this chaos in a way which would make sense to members of the public. Figure 11.3 was the result. Concentric circles create bands for:

- 1. The person whose circumstances give rise to claiming the benefit, e.g. a child.
- 2. The person who actually makes the claim, e.g. the person who is responsible for the care of child.
- 3. The focal event which makes it possible to claim the benefit, e.g. the birth of the child.
- 4. The welfare context, a concept which emerged from this analysis as a useful way to map benefit onto real life experiences; e.g. bringing up children.
- 5. Non-means tested social security benefits available before the Fowler recommendations come into effect.
- 6. Other provisions.

Means-tested benefits, ‘the safety net’, are broad provisions which go across a number of the welfare contexts and so are flung, rather like a hammock, across the bottom with arrows to indicate extensions in both directions.

Systemic grammar networks (SGN) are graphs which provide a way of representing any domain wishes. An SGN is made up of nodes which represent concepts in the domain and are related to each other in one of ways. Forward straight brackets, [, enclose nodes which are mutually exclusive of one another (a disjunction, the ‘exclusive or’ of logic). Curly brackets, {, enclose nodes which occur together (a conjunction, the ‘and’ of logic).

There is a curly arrow (not used on this figure) to indicate the nodes must be ‘gone through’ several times, once for each child of a family (recursion). There is also a square bracket, [, for a conditional relation indicating that if all (and) and of nodes enclosed ‘apply’ then the following one does also.

Work with these networks was hindered by the inability of the software we were using at the time to create these symbols easly. This was especially a problem with the recursive curly arrow and making the curly bracket large enough to enclose the number of nodes required. This difficulty led to the labelling of the enclosing symbol with EOR for the ‘exclusive or’, AND (or ‘and’) for the conjunction and the conditional relations. These logical operators are sometimes (I think incorrectly)

# Legal Applications of KBS

![](img/fd9daa466aa6610f0ebd57e2ccc632c5_250_0.png)

The main references used were the two CPAG handouts and Tolleys.

Benefits included in the diagram are not an exhaustive list, but include a large proportion of them.

BC: PAGESKETCH-1: 18TH DEC '86

# Figure 11.3 Overview of the UK Welfare System
