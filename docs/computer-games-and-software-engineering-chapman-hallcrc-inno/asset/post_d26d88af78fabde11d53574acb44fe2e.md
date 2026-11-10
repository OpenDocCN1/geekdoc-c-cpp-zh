
fraction of the game-playing population) and being too easy (and therefore unsuitable for competitive play). For AGAD, we selected questions that are purposely unlikely to be known by even a small fraction of the gamers, yet answers that are discoverable with a few Google searches. The questions also had to be of some intrinsic interest—truly trivial questions, such as what is the 23rd digit in the decimal expansion of pi?—are unsuitable for game play.

AGAD is a fairly simple game to construct. The UI presents a few questions each day, with daily updates to the set. Players work through the questions, doing Google searches in a separate iframe that allows the search engine to be visible alongside the question. Each question has a simple answer that can be recognized by a regular expression. Writing the regexp is slightly tricky, as most questions have multiple variants on an answer (e.g., “three,” “3,” or “the number 3”).

As shown in Figure 9.1, the questions are presented in a frame at the bottom of the page, with typical game mechanics such as unlocking subsequent questions, buttons to let the player skip a question, and ways to compare your score (and time to answer the question) with friends via the Google+ social network.

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_221_0.png)

FIGURE 9.1 (See color insert.) The AGAD game shows a search question (3), then lets you search for the answer with Google (1). You work through the questions (2) scoring points as you unlock and solve additional questions.

As we developed AGAD, it quickly became clear that user testing would have to be an important part of the design cycle. This is true for all games, but as we proceeded, it became clear that we actually had to do more than standard usability testing in the lab.

One large bias was that in the lab setting, people are highly motivated to perform to the best of their ability. As a consequence, we were seeing a divergence between the lab testing and what we anecdotally observed when watching people in the wild. How could we improve the accuracy of our design-driven testing?

To make our understanding of the players more accurate, we needed to understand what they are doing when they started up the game, how they played the game, and what happened over a broad population. This is what led to the idea that the studies should encompass three different approaches. We needed to not just understand the low-level usability issues but also verify that the game was fun to play and would leave people with a positive attitude about Google.

Thus, the goal of our design testing strategy became to observe the players in three different ways in order to create a fully rounded picture of what they are doing in (and how they are enjoying) the game.

## 9.4 THREE VIEWS OF THE USER: MICRO, MESO, AND MACRO

After a bit of iteration, we settled on three different analyses of player behavior. We wanted to understand the play behavior at a second-to-second timescale. As useful as that is for usability issues (e.g., why do players sometimes never click on a particular game option), this level of analysis is too detailed for understanding user reactions to the game and does not provide any information about their affective responses. To provide that kind of information, we ended up doing analyses of game play over the period of minutes to hours. And similarly, that level of analysis (while useful) would not provide the kind of large population data we also wanted to collect and understand—data that would tell us from weeks to months what was happening.

We realized that our three scales of analysis were very similar to Newell's timescales of human behavior (Newell 1994). Newell's analysis framework has four bands: neural (1–10 ms), cognitive (10 ms–10 seconds), rational (minutes to hours), and social (days to months). His division of cognitive behaviors along different timescales was to emphasize that different kinds of effects can be explained by fundamentally different mechanisms. I take a similar approach here.

- 1. *Microscale* measures the behaviors from milliseconds up to minutes of behavior, usually with a small number of people, usually in a lab setting. With these studies, we want to gain insight into the mechanics of the game—where players look, how they perceive the game elements, and what is left unnoticed and unexplored.
- 2. *Mesoscale* measures the behaviors from minutes to hours. This is the realm of field studies, watching people play the game in natural settings (e.g., at home or in the coffee shop). The mesoscale provides insights into why people choose to play and why they end up stopping their play, as well as understanding about what makes the game interesting (or not).
- 3. *Macroscale* measures the behaviors from days to weeks and months. Typically, this involves large numbers of players and is usually an analysis of the logs of many people playing the game.

Logs of user behavior have been a standard practice for some time. Traces of behavior have been gathered in psychology studies since the 1930s (Skinner 1938), and with the advent of web- and computer-based applications, it became common to capture a number of interactions and save them to log files for later analysis. More recently, the rise of web-based computing platforms has made it possible to capture human interactions with web services on a large scale. Log data let us observe how to compare different interfaces for supporting e-mail uptake and sustained use patterns (Dumais et al. 2003; Rodden and Leggett 2010).

Let us look at each of these timescale analysis methods in more detail.

### 9.4.1 Micro Level: How Players Behave over Short Timescales

Although there are many methods to study human behavior over short periods of time, the simplest and most practical method for usability studies is eye tracking (also known as *eye gaze*) studies (Bergstrom et al. 2014).

Eye tracking studies require bringing a subject into the lab to use a special monitor that has an eye tracking system built into the bezel of the monitor (there are many companies that sell such systems, e.g., Tobii, or Senso Motoric Instruments (SMI)). These systems calibrate the player's eye movements on the monitor and output where the eye moves on the screen at time resolutions down to the milliseconds. Essentially, they create *X*, *Y*, and *T* data streams (*X* and *Y* positions of the gaze focus on the display, where *T* is the amount of time the eye dwells on those *X* and *Y* locations), along with any user actions taken (such as a click, typing, or scroll event).

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_225_0.png)

FIGURE 9.3 (See color insert.) The heat map display shows how much time the eye spent at any one spot during the sample time. Here we can see the player spent most of the time reading the question (next to the theatrical mask glyph at the bottom and near the top at the search query).

study participant. Although it seems like a small thing, in fact, questions and behaviors that are natural to ask the participant may never arise in a lab setting (Grimes and Russell 2007). Researchers can learn a good deal about participants and their motivations in this way, but the observed behavior happens in a controlled and artificial setting and may not be representative of behavior that would be observed “in the wild.”

In the lab setting study, a person may invest more time to complete a task in the lab than he or she might otherwise to please the investigator (Dell et al. 2012). In addition, laboratory studies are often expensive in terms of the time required to collect the data and the number of different people and systems that can be studied.

The micro level of study is useful, but does not answer all of the questions one might have about game play in a more ordinary setting.

### 9.4.2 Meso Level: How Humans Behave Minute by Minute

At the meso level of study, research is done to determine how system users perform tasks of interest (play the game) and to collect information that cannot be gathered in any other way (e.g., direct observation of affective responses to a computer game).

The meso-level research approach is primarily to perform field studies of user behavior, that is, to collect data from participants in their natural
