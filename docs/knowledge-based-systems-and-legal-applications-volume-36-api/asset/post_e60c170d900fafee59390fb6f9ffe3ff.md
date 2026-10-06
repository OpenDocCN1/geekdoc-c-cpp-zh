
for example it is important to distinguish between capital owned by dependents and that owned by the claimant or the claimant's partner, and some kinds of income need to be treated as if they were capital.

These limitations encouraged us to concentrate our work for the second prototype on the requirements for supporting the handling of a case.

## 7.7. LOCAL OFFICE DEMONSTRATOR 2 (LOD2)

LOD2 was to concentrate on the assessment of new claims while recording sufficient data about the assessment to enable facilities for reviewing assessments and preparing appeal submissions to be added later. Assessment would start with pre-input case data, and end with rejection of the claim or a 'payment panel' giving the amount, means, and start date of payment.

The assessment task was seen as consisting:

- 1. Checking that the claim has been properly made.
- 2. Identifying the type of case, and its associated problems.
- 3. Identifying the 'topics' that will need attention during the detailed assessment.
- 4. Choosing a sensible order in which to handle the topics.
- 5. Handling the topics.
- 6. Combining and summarizing the findings and completing the case assessment.

Decisions were seen as involving the selection of appropriate rules by ascribing some feature of the case to a specific legal category, as in LOD1, but also:

- 1. The (relatively) straightforward application of 'clear rules' (i.e. rules whose conditions do not require interpretation).
- 2. The (human) interpretation of legal conditions.
- 3. A sequence of procedures or decisions, depending on the results of earlier decisions.

The interaction was to involve guidance from the system, decision by the user, and the processing of straightforward results by decisions of the system. The user would identify the type of case and the problems associated it. The system contained its own 'classification rules' which would be applied to the data. The system would ask for clarification if its classification rules gave different conclusions from those given by the user. The user would be guided by the system through the detailed conflict in assessing the given case — the system would contain 'planning' rules allowing it to recommend an order for handling the necessary topics. Relevant textual or case-related guidance was to be

## Legal Applications of KBS

easily accessible when a condition requiring interpretation was being dealt the user had to be free to change his or her mind at any time about earlier inputs. The system was to help the user to keep track of the whole assessment process — the user is responsible for the outcome of the assessment, so must understand all aspects of it, including those performed by the system. If the user encountered problems in handling some part of a case, he or she was able to mark it for the attention of a reviewer, handle it whatever seemed best, and carry on with the rest of the assessment. Different styles of interaction were required to support the following types of:

- 1. Starting up the system, selecting a case to work on, possibly going to another case, and closing down the system after working on a case or series of cases.
- 2. Handling a case, including validating the case data, identifying problems associated with the case, finding and ordering relevant assessment topics, selecting each topic for handling, reviewing the overall result and closing the case.
- 3. Arriving at a decision based on the answers to sequences of questions, possibly presented in groups on forms, where the answers at a given stage in the interaction help to determine what questions will be asked next, and where the ordering is also based on the user's need to see some coherence in the interaction (we referred to this style as a ‘structured dialogue’).
- 4. Classifying items (as in LOD1) where the selection of a 'real world' class for an item leads to a request (by a form or a series of questions) for the detailed data needed to determine the treatment of such an item.
- 5. Retrieving case-related information as guidance on the interpretation of a condition.
- 6. Retrieving textual styles of interaction for all of these subtasks except (3) (‘structured dialogue’).

An icon representing the system expanded into a login box. After successful login, the user was presented with a menu of his or her case. Selecting a case led into the case handling screen, containing a window holding case data, a window for results of assessments, windows for guidance and ‘system help’, and a working area. Icons at the side of the screen gave access to on-line legislation, guidance and procedures.

The user could browse through the case data using buttons beside the case data window to access sections corresponding to the sections of the claim form. On request, he or she could proceed to a classification stage, where a form allowed potential problem areas to be marked. Guidance was available for each potential problem area on the form, and justifications could be added to chosen items. When satisfied with his or her entries, the user could compare notes with the system; any differences in opinion about potential problem areas needed to be resolved or justified by the user before handling of the assessment could proceed further.

The system then used the classification to derive a list of topics needing to be handled, and to present them in a menu in the preferred sequence.

This menu of new topics was presented in the working area; when the user selected a topic it would take over the working area of the screen, and when the user suspended or completed the handling of the topic he or she would be returned to the new topic, with the topic that had just been worked on moved to a 'suspended' or 'completed' menu as appropriate. Completion of all necessary topics gave access to a final assessment display, with fields for the main conclusions in the case. The user was permitted to override the values in the final assessment, so long as a justification was given. Authorization of the final assessment would lead to the 'payment panel' containing the amount, date and means of benefit payment. The topic fully implemented in LOD2 was capital, as implemented in LOD1. To allow demonstration of the retrieval of case-related guidance, some conditions in the classification form led to a case retrieval facility modified on that of the mobility allowance application.

While the implementation of LOD2 appeared to make advances on LOD1 in terms of embedding specific support within an overall handling of a case, LOD2 was a disappointment to those involved in its specification and implementation. The interaction supported by LOD2 appeared unnatural and forced, in a number of ways:

- 1. Users were being required to go through a fixed preliminary stage of classification, whereas in practice their classifications would tend to emerge as they progressed through the case.
- 2. The general heading of 'classification' actually covered a range of separate issues, including:
    (a) the identification of ways of quickly resolving a case;
    (b) highlighting of potential 'problems' which require specific attention;
    (c) declaration of features of the case which have 'pervasive' implications (e.g. claimant involved in a trade dispute, or student).
    LOD2, however did not distinguish between these.
- 3. The number, and level of precision, of the classifications appeared 'arbitrary'.
- 4. The style of support raised concerns about its effect on users with different levels of skill and the requirement for fast paths through the interaction.
- 5. The system required prior input of claim data; this raised questions about the status of data input by clerical staff, and made it likely that large amounts of data would be input unnecessarily.

Overall, we had the feeling that something was deeply wrong with the system, but had not yet got to the root of the problem. We were, by then, well until the final year of the project — if anything radical was to be done, it would have to be done quickly.

## 7.8. LOCAL OFFICE DEMONSTRATOR 3 (LOD3)

While LOD2 was being developed, its designers had been faced with a long list of demanding requirements. It was not clear whether some of these requirements could be met at all, how well others could be met, or whether some of the requirements conflicted with others. A literal reading of the requirements had led to a view of the system as having many parts, and strongly modal behaviour. This, coupled with the daunting nature of the list overall, had led to a rather piecemeal approach to the design and construction of LOD2.

While LOD2 was never completed, and what there was of it had arrived, it fulfilled the intention of a 'prototype' in giving a concrete basis for discussion between 'requirement owners' and designers. It gave a clear indication that we were on the wrong track, and would have to reconsider our earlier intention to use LOD2 as a 'shell' within which we could scale up the domain knowledge and detailed user interface to produce LOD3. Some time was spent re-evaluating and prioritizing requirements. The following list was produced in early October 1988:

- 1. Needed throughout the system:
    (a) data input by user, validated by system;
    (b) access to explanations in terms of the legislation used;
    (c) ability to work on a claim with incomplete information;
    (d) system prompts for information should make clear why the information is needed;
    (e) on-line browseable manuals and legislation;
    (f) on-line help with use of system (e.g. input formats);
    (g) support for the styles of subtask as described for LOD2;
    (h) support for appeals submissions (in terms of ability to review the working of a completed case, retrieving explanations in terms of the legislation used, possibly with the additional ability to select and assemble standard pieces of text together with parts of the explanation and case data within a standard textual
