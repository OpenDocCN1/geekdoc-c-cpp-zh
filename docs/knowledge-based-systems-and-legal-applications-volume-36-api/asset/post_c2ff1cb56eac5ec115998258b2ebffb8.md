
# The Claimant Advice Systems

none to generate phrases. Each of these mechanisms had a corresponding declarative representation; a ‘public tree’ to describe the content of all utterances made by the user and the system. Both of these declarative representations had to relate to the referents mentioned in the knowledge base. The text generator that generates possible phrases is also used to generate complete system utterances.

## 9.4.4. Evaluation

At the time of writing, a number of lone parents are using the Advice System under laboratory conditions to evaluate the usability of the system as a whole. They are given the opportunity to explore what benefits might be available to them in their own situations. They are encouraged to comment verbally on what they are doing while they use the system and their interactions with it are logged for later analysis. Their comments and an interview held immediately after the trial are tape-recorded. In addition, a larger number of students are being given a ‘scenario’ containing a brief story about a hypothetical family and are being asked to use the system to find out what benefits the family is eligible for. Further details can be found [Gilbert 1990] and in [Gilbert and Jiroka 1990].

The detailed results of these trials are not yet available, a preliminary analysis of the data suggest that on the whole design meets objectives. The system's answers were considered to be clear and direct, and users appreciated their ability to ask as many questions as they liked. One user said the best thing about the system was that ‘you keep going around without getting fed up... you can go through different areas and different angles on the same thing’. The negative side of was that the sessions were often quite long, frequently lasting an hour or more.

In general, users tended to seek out case level rather than domain or theory level answers. In this way users were able to capitalize on the major capability of the system over information leaflets: that giving personalised information. This attitude was captured by one user who said the system was ‘better than ploughing through leaflets. It lets you to the heart of what you want to find out’. The trend was particularly evident for the lone parents, who had been given the freedom to explore the system for any kinds of answers they wanted. Out of a total of twenty-nine questions asked, twenty-one were for the case level answers, seven were for domain level answers, and one was for a theory level answer. These users asked primarily for quite specific answers with questions like ‘Can I get housing benefit?’ or ‘How much income can support I get?

## Legal Applications of KBS

Most domain level answers were definitions of terms which users found useful in the process of answering system questions relating to their primary case level question. Theory answer types were generally not requested except in cases where the system gave negative advice. Users reported trusting the system's answers and only if it meant they could not get a benefit they had expected to.

The fact that users trusted the advice given did not mean that they were always satisfied with it. In fact a single system answer gave enough information of the desired kind of question. Users often had troubling phrasing exactly the right kind of question on the same or a similar topic. This led to a highly interactive dialogue in which users explored an issue from a number of different angles. In the post-session interview, users confessed to being surprised at this, having expected to ask a follow-up question and expected a much more system dialogue in which they would answer a long string of questions before giving a single monologue on the benefits they could get. Several users spontaneously commented on the 'human qualities' of the talk, reacted against the suggestion that it was 'like a conversation'. One user reflected a general feeling that the interaction was more formal or business-like than a conversation, by saying that 'It was more like a question and answer interview'. Another commented that 'It's better than a conversation because you can tell it to shut up and butt in'.

## 5.9. OTHER EXPERIMENTAL DEVELOPMENTS

### 5.9.1. Tools for qualitative analysis

As part of the potential user study, we tape-recorded two interviews with each of fifty families. These interviews were transcribed and common themes picked out from the transcripts. We had not gone far with the analysis before it became obvious that the technology we were using for the Forms Helper and the Advice System also had potential for assisting with the tedious and time-consuming task of sifting through hundreds of pages of transcript. Thus was born the 'qualitative analysis tool' or QAT, a specification and prototype for a program to help with the analysis of any large body of textual materials. A description of user requirements and a requirement specification was produced and was persuaded that some resources should be assigned to building a prototype. This prototype, constructed over the period April to December 1986, was the project's first attempt to build a system with a significantly complex user interface. It was not a success, mainly because the difficulties of building such systems were not at that properly appreciated and the facilities which could be provided were very limited. However, the failure of the prototype was of considerable significance for the project as a whole: from its ashes was born the project's screen management tools and, because the the project realised that the QAT would have potential not only for analysing interview transcripts but also for analysing documents such as legislation and regulations, QAT metamorphosed into KANT (Chapter 11).

### 9.5.2. Word incorporation parser

There are points in the dialogues between the user and both the Advice System and the Forms Helper where the user is asked for a date or a sum of money. We decided that we should allow users to input dates and amounts of money in any reasonable format, rather than forcing them to abide by some predefined style. This meant that these systems had to incorporate a parser capable of taking user inputs in many different formats and converting them into a standard one. Our first attempt used a chart parser, but this was found to be much too slow, taking three to five seconds to parse a single input. A second parser was built, based on a technique known as 'word incorporation-poration' ... This took between half and one second to parse a date, an acceptable response time. The parser used a grammar and dictionary which was developed to recognize inputs such as the following: 25th dec '86, 25/12, the 25th of December 1967, thirty pounds, 35.00, three hundred and sixty five, 365, three hundred and 65, and don't know.

# CHAPTER 10

# MANAGING A LARGE COLLABORATIVE PROJECT

Charlie Portman

The Alvey-DHSS Large Demonstrator was a large project in several senses. It consumed over 35 person-years (115 different people were associated with the project during its lifetime). It consequently spent a lot of money each quarter. It lasted five years and took a significant slice out of the lives of its members. It was set up to tackle a large problem with several facets and ended up writing large pieces of software and constructing quite large knowledge bases. Lastly, the project was large in a physical sense; it was spread from Lancaster to Guildford and from Liverpool to Cambridge across nine sites.

## 10.1. ORGANIZATION

The project was preceded by a study which did the work needed to write the formal proposal — a document of 256 closely printed pages. The proposal outlined the project's structure and method of working so when the project started the organizational framework had already been defined. This framework was proposed in the absence of real experience of such a large, cross-culture collaborative project but seems, in hindsight, to have been well-chosen apart from the design control function which was probably inappropriate in the first few years of the project since it seemed to suggest that commonality would exist from the outset. This turned out to be an unreasonable view in light of the scope of exploration needing to be done in the early years.

The project was initially organized with a top-level steering team,
