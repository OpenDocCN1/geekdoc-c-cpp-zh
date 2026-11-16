
(Constantin 95). Von Altrock, Constantin. Fuzzy Logic and Neuro Fuzzy Applications Explained. Prentice-Hall, 1995.

(Cornelius 98). Fuzzy Logic and Expert Systems Applications ed. by Cornelius T. Leondes, Academic Press, 1998.

(Kerre 00). Da Ruan and Etienne E. Kerre. Fuzzy If-Then Rules in Computational Intelligence, Kluwer Academic Publishers, 2000.

(Da Ruan 97). Intelligent Hybrid Systems: Fuzzy Logic, Neural Networks, and Genetic Algorithms, Kluwer Academic Publishers, 1997.

(Gardenfors 04). Peter Gardenfors, Belief Revision, Cambridge Tracts in Theoretical Computer Science, 2004.

(Dempster 67). A. P. Dempster, "Upper and Lower Probabilities Induced by Multivalued Mappings," Annals of Math. Stat., 38, pp. 325-329, 1967.

(Giarratano 91). Joseph Giarratano, et al., "Fuzzy Logic Control for Camera Tracking System," Fifth Annual Workshop on Space Operations Applications and Research (SOAR '91), pp. 94-99, 1991.

(Harris 00). John Harris, An Introduction to Fuzzy Logic Applications, Kluwer Academic Publishers, 2000.

(Ibrahim 03). Ahmed M. Ibrahim, Fuzzy Logic for Embedded Systems Applications, book with CDROM with lots of references, pub. by Newnes, 2003.

(Kosko 96). Bart Kosko, Fuzzy Engineering, Prentice Hall, 1996.

(Liu 04). RuYin Liu. Fuzzy Neural Network Theory and Application (Machine Perception and Artificial Intelligence), World Scientific Publishing Company, 2004.

(Mendel 00). Uncertain Rule-Based Fuzzy Logic Systems: Introduction and New Directions, Prentice-Hall, 2000.

(Nguyen 99). Hung T. Nguyen and Elbert A. Walker, A First Course in Fuzzy Logic, CRC Press, 1999.

(Roger 96). Jyh-Shing Roger Jang, Chuen-Tsai Sun, Eiji Mizutani, Neuro-Fuzzy and Soft Computing: A Computational Approach to Learning and Machine Intelligence, Prentice-Hall, 1996.

(Ross 04). Timothy J. Ross, Fuzzy Logic with Engineering Applications, John Wiley & Sons, 2004.

(Siller 04). William Siler and James J. Buckley, Fuzzy Expert Systems: Theory and Applications, Wiley-Interscience, 2004.

## CHAPTER 6

### Design of Expert Systems

### 6.1 INTRODUCTION

In the previous chapters, we have discussed the general concepts and theory of expert systems and other intelligent decision making-systems. A number of papers have attempted to summarize the properties of intelligent systems. There are many pros and cons for each type (Begley 03). This chapter presents general guidelines for building practical expert systems designed for real-world applications, not research prototypes. A software engineering methodology is described so that an expert system can be a quality product developed in a cost-effective and timely manner.

Many books, papers, and software tools have been devoted to the design of expert systems, covering all aspects in great detail. So this one chapter will not make you an instant expert. (You'll have to read the chapter first). However by understanding the principles that explain why expert systems are designed the way they are, you'll be better able to take advantage of sophisticated tools and methodologies. In fact the design of expert systems is part of a more general field called Knowledge Management (KM) which deals with all the knowledge assets available to an organization (Becera-Fernandez 03).

KM is connected to the Information Management (IM) which is connected to the Information Processing (IP) which is connected to the Information Systems (IS) which is connected to the Information Technology (IT). (On second thought, if you can say KM, IM, IP, IT, three times in a row without mispronouncing, you are an Instant Expert!) KM is a major problem considering all the different types of resources for many different types of audiences such as office, web, FAQs, Help Desk (human and automated), email, fax, phone, product, program, developer, manager, end-user, and publicity.

Large companies have their own very detailed methods, documents, books, and software they developed to create, manage, maintain, and sell knowledge assets because it is such a profitable field (Conway 02). This is especially true when intelligent tools are created that can greatly reduce human expenses because that's even cheaper than global outsourcing.

If you think how much time a typical person spends using computers, it's a tautology that we need computers to manage all the documents created by computers. Expert systems are widely used in business because they are so essential to the dramatically increasing amount of information and knowledge available on the web (Malhotra 01). As usual, links to software and other online resources for this chapter are listed in Appendix G.

### 6.2 SELECTING THE APPROPRIATE PROBLEM

There are many ways and resources by which you can build a knowledge-based or expert system. There are even more ways you can waste your time and money (for example, donating to the Starving Authors and Copyeditors Fund, a for-profit organization). However, the Fourth Law of Wisdom states that before you set out on a journey, you should know your destination.

Before you build an expert system, you should select an appropriate problem, as discussed in Section 1.6. Like any software project, there are a number of general considerations that should be made before a large commitment of people, resources, and time to a proposed expert system. These general considerations are typical of project management concerns in conventional programs, but must be customized for the special requirements of expert systems. A very high-level view of project development is shown in Figure 6.1. The three general stages of Activity, Product Configuration, and Resource Management have some more specific considerations, shown below. These more specific considerations will be discussed as questions and answers to serve as guidelines for expert systems projects.

### Selecting the Appropriate Paradigm

### Why are we building an expert system?

This is probably the most important question to be asked of any project. The most desirable answer is that the president of the company wants it built. If that's not the case, see if the general advantages of expert systems as described in Chapter 1, Section 2 apply. Most of all, remember only management can authorize the system and technical personnel needed. If you decide to build it on your own time to show the company you were right, and then realize what a great product it is, and decide to quit and form your own company, there is the small matter of that Intellectual Property Agreement you signed. Most IPAs state that whatever you come up with, whether related or not to your job duties, 24x7x52, belongs to the company. In particular, the answer to this question must eventually be given to the owners or stockholders funding development. Before starting, there should be a clear identification of the problem, expert, and users.

Note that the singular term expert is used, not plural experts. Just as the best way to guarantee trouble is to have multiple spouses at once, more than one expert will also guarantee trouble. Even the President only sees one doctor at a time, so it's not a matter of cost. Trying to model the expertise of multiple experts in one system is a bad idea. However, modeling the expertise of multiple experts in multiple systems using a blackboard architecture to reach at least a majority opinion is good. This does bring up what the fuzzy term good means. If nine out of ten doctors say the patient will die, the patient will inevitably choose the doctor that offers a treatment for life (unless the patient is really cheap and the treatment costs money). Trying to decide how to rank multiple expert opinions is a daunting task, usually more formidable than building a single expert system for a single expert. So we'll stick with the single-system-single-expert approach in this chapter and leave the multiple-experts-multiple-systems as a class project.

Figure 6.1 Project Management Tasks

![](img/2c460d4de56b7ffaad3834eee20beaa0_372_0.png)

### Payoff

What is the payoff?
This question is related to the first question. However, this question is more pragmatic by asking for a specific return on investment of people, resources, time, and money. The payoff may be in money, increased efficiency, or any of the other advantages of expert systems described in Chapter 1. It is also important to remember that if no one uses the system, there will be no payoff. Because expert systems is different from conventional programming it is more difficult to answer this question.

### Tools

What tools are available to build the system?
There are many expert systems tools available today with advantages and disadvantages as discussed in Appendix G. However, this should be taken only as a guide since software tools develop so rapidly. Generally, you can count on an enhancement every couple years in each tool and a major revision every five
