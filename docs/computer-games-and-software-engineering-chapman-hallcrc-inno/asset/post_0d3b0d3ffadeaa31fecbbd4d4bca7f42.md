
- 30. James Paul Gee. *What Video Games Have to Teach Us about Learning and Literacy?* Palgrave Macmillan, New York, 2007.
- 31. Tao Xie, Nikolai Tillmann, and Jonathan de Halleux. Educational software engineering: Where software engineering, education, and gaming meet. In *Proceedings of GAS*, pp. 36–39, San Francisco, CA, 2013.

## Adaptive Serious Games

Barbara Reichart, Damir Ismailović, Dennis Pagano, and Bernd Brügge

## CONTENTS

- 6.1 Introduction — 134
- 6.2 Background — 135
- 6.3 Basis for Exploratory Studies: Development of Four Serious Games — 136
- 6.4 An Exploratory Study: How to Characterize Players in Serious Games? — 138
  - 6.4.1 Study Design — 139
  - 6.4.2 Results — 140
  - 6.4.3 Conclusion — 143
- 6.5 An Exploratory Study: How to Provide Help in Serious Games? — 143
  - 6.5.1 Study Design — 143
  - 6.5.2 Results — 144
  - 6.5.3 Conclusion — 145
- 6.6 Threats to Validity — 146
- 6.7 Towards a Definition of Adaptivity — 146
- 6.8 Outlook — 148
- 6.9 Summary and Conclusion — 148
- References — 149

**Abstract:** Learning is associated with a lot of effort and perseverance. In learning theories, motivation can be observed as a key factor for successful learning. Serious games can increase motivation because they involve use of a variety of elements, such as visual environments, storylines, challenges, and interactions with nonplayer characters. This makes serious games ideal learning environments as the learning experience becomes so intrinsically satisfying and rewarding that external pressures or rewards for learning are of secondary importance. Even though games have such motivational power, several studies have shown that there are no known forms of education as effective as a professional human tutor, because tutors select learning content based on the learners’ skills, thus adapting to the learner every step along the way. This chapter explores the interaction between human tutors and learners in serious-game development with the focus on social development theory. It presents results that show how human tutors observe players in executing learning tasks and interacting with the game environment in serious games. Based on the results of these studies, we provide a definition of adaptivity for serious games.

### 6.1 INTRODUCTION

Serious games can engage the learner in a way most traditional teaching methods cannot. They provide a platform where the two points, motivation and interactive learning, can be perfectly put together.

This chapter describes studies that explore the effects of human tutors in serious games. Observations by developing serious games showed that without help, children require more time to learn how to play the game than adults, although both groups could reach the same time with help [1]. Learning theories such as Vygotsky’s social development theory [2], Piaget’s stages of cognitive development [3], and Erikson’s developmental stages [4] explain this phenomenon based on the social context of learners during the learning process.

The reason why learning progresses faster with human tutors than with other tools is the higher *adaptivity* to the learner. The problem is that serious games of the current state of the art do not adapt to the learner [5–8]. Consequently, a major goal in modern serious-game development and research is to make the game adapt to the learner and provide intelligent actions in order to achieve higher individuality [1,9].

Although one could argue that techniques to realize adaptivity have already been developed for e-learning systems, the *intelligent tutoring systems* (ITSs) usually foster very different activities than those seen in a game. The aim of this chapter is therefore, to explore the ways of adaptivity that are specific to serious games and to build a foundation for software frameworks for adaptivity in serious games.

The contribution of this chapter is twofold. First, we provide two studies that explore the role of human tutors in serious games. Second, based on the

### 6.2 Background

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_155_0.png)

**FIGURE 6.1** (See color insert.) (a,b) Zone of proximal development can be expanded and changes over time.

knowledge over a specific topic is not given by a single score, but instead it also provides information about the specific strengths and weaknesses of a student within the field. This is done by splitting the content into several smaller learning goals. The connection between those different goals is then given in the form of prerequisite relationships. For example, looking at learning how to divide numbers, the division by a digit, can be seen as a prerequisite for learning about division by numbers bigger than 10. This knowledge allows the ITS to select lessons based on the learners’ skills.

### 6.3 BASIS FOR EXPLORATORY STUDIES: DEVELOPMENT OF FOUR SERIOUS GAMES

In order to research the role of tutors on learning and how their competencies could be transferred into serious games, we conducted two studies. In the first study, we wanted to find out which observations tutors used to assess the learners’ skills. The second study then uses the results of this assessment to adapt to the learner.

Both studies required a very high control over the game elements including, but not limited to, the content, the difficulty level, and the game speed. Unfortunately, existing serious games do not give us this level of control. Therefore, we needed to develop our own serious games.

We developed four small serious games with focus on elementary school mathematics. Their goal is to teach skills ranging from writing (Figure 6.2a) and reading numbers (Figure 6.2b), simple addition

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_156_0.png)

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_156_1.png)

**FIGURE 6.2** (a) Writing numbers with the guidance of a flashlight. (b) Practice counting quickly to save bugs. *(Continued)*

The tasks cover a wide range of abilities, from counting and simple addition and subtraction, to classifying geometric figures by form and color (Figure 6.2d). These contents were directly selected from the official curriculum of German elementary schools.

During the development process of the games, experts from different fields were involved. This was necessary, so that important aspects from the technical, psychological, and pedagogical side would not be overlooked.

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_157_0.png)

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_157_1.png)

FIGURE 6.2 (Continued) (c) Central screen for "Emil and Pauline in the cave", where the kids can track their progress and select which game they want to play. (d) Practice geometry and generalization. All shapes that fulfill a specific criterion follow the finger of the kid. The task of the kid is to figure out the commonality (e.g., shape, color, size).

### 6.4 AN EXPLORATORY STUDY: HOW TO CHARACTERIZE PLAYERS IN SERIOUS GAMES?

As we already argued, there are no known forms of education as effective as a professional human tutor [7,8]. The reason is based on the fact that in the current state of the art, no computer system is as good at adapting to users as humans [5,6].

According to the social development theory, tutors observe learners and try to provide help when necessary. Using their observations, tutors can analyze the learner and decide at what point help is necessary. Help is then provided through direct interaction with the student. The ZPD defines the difference of the learning outcome between children learning with a personal tutor and without a tutor [14].

Applying this theory to serious games requires finding out what exactly tutors can observe when watching and learning with the learner using a serious game. Additionally, we need to understand how the observed information is used by the tutors to characterize learners.

When a human tutor observes and consequently provides help to the learner, he or she can identify the learner's skills. In order to transfer this method to serious games, we need to find out how tutors carry out this task in a serious game. Therefore, we focus on answering the following question: What can be observed when a learner plays a serious game and how can this information be used to characterize the individual learner?

**6.4.1 Study Design**

To answer this research question, we applied qualitative research methods by interviewing experts and by observing children while playing.

We developed a serious game in an iterative process with experts (pedagogues, psychologists, professional game developers, serious-game researchers, students, and players). During the development process, we carried out informal, conversational interviews with all participants during each iteration. The constructed game provided us with a real example to the given question and supported experts to reflect on their answers. Additionally, we used this serious game to observe children while playing in order to be able to provide more data for the experts. Finally, we carried out retrospective interviews with experts based on this project. We repeated the process in four serious games. An overview of the steps followed in the study is given in Figure 6.3. We iterated the steps described in the figure for each serious game independently.

The goal of this study is to provide a detailed description of data that can be observed in a concrete serious game for children with one specific topic and a detailed description of how experts characterize the child in the given example.

The difference between the design of this study and the study proposed by Vygotsky in the theory described previously is as follows: In the serious games proposed here, there is no direct interaction with the learner. This is done based on the fact that in the current state of the art of mobile technology, no computer system can observe and react in as much nuance
