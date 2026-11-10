
Digitized by the Internet Archive in 2022 with funding from Kahle/Austin Foundation

## Computer Games and Software Engineering

## Computer Games and Software Engineering

Edited by

Kendra M. L. Cooper  
University of Texas  
Dallas, USA

Walt Scacchi  
University of California, Irvine  
Irvine, USA

## Contents

- Contributors, vii
- **CHAPTER 1** · Introducing Computer Games and Software Engineering — 1  
  *Kendra M. L. Cooper and Walt Scacchi*

**SECTION I** **The Potential for Games in Software Engineering Education**

- **CHAPTER 2** · Use of Game Development in Computer Science and Software Engineering Education — 31  
  *Alf Inge Wang and Bian Wu*
- **CHAPTER 3** · Model-Driven Engineering of Serious Educational Games: Integrating Learning Objectives for Subject-Specific Topics and Transferable Skills — 59  
  *Kendra M. L. Cooper and Shaun Longstreet*
- **CHAPTER 4** · A Gameful Approach to Teaching Software Design and Software Testing — 91  
  *Swapneel Sheth, Jonathan Bell, and Gail Kaiser*
- **CHAPTER 5** · Educational Software Engineering: Where Software Engineering, Education, and Gaming Meet — 113  
  *Tao Xie, Nikolai Tillmann, Jonathan de Halleux, and Judith Bishop*
- **CHAPTER 6** ■ Adaptive Serious Games — 133  
  *Barbara Reichart, Damir Ismailović, Dennis Pagano, and Bernd Brügge*

**SECTION II** **Conducting Fundamental Software Engineering Research with Computer Games**

- **CHAPTER 7** ■ RESTful Client–Server Architecture: A Scalable Architecture for Massively Multiuser Online Environments — 153  
  *Thomas Debeauvais, Arthur Valadares, and Cristina V. Lopes*
- **CHAPTER 8** ■ Software Engineering Challenges of Multiplayer Outdoor Smart Phone Games — 183  
  *Robert J. Hall*
- **CHAPTER 9** ■ Understanding User Behavior at Three Scales: The A Google A Day Story — 199  
  *Daniel M. Russell*
- **CHAPTER 10** ■ Modular Reuse of AI Behaviors for Digital Games — 215  
  *Christopher Dragert, Jörg Kienzle, and Clark Verbrugge*
- **CHAPTER 11** ■ Repurposing Game Play Mechanics as a Technique for Designing Game-Based Virtual Worlds — 241  
  *Walt Scacchi*
- **CHAPTER 12** ■ Emerging Research Challenges in Computer Games and Software Engineering — 261  
  *Walt Scacchi and Kendra M.L. Cooper*
- Index, 285

## Contributors

- **Jonathan Bell**  
  Department of Computer Science  
  Columbia University  
  New York, New York
- **Christopher Dragert**  
  School of Computer Science  
  McGill University  
  Montréal, Québec, Canada
- **Judith Bishop**  
  Microsoft Research  
  Redmond, Washington
- **Robert J. Hall**  
  AT&T Labs Research  
  Florham Park, New Jersey
- **Bernd Brügge**  
  Computer Science Department  
  Technical University of Munich  
  Munich, Germany
- **Damir Ismailović**  
  Computer Science Department  
  Technical University of Munich  
  Munich, Germany
- **Kendra M.L. Cooper**  
  Department of Computer Science  
  University of Texas, Dallas  
  Richardson, Texas
- **Gail Kaiser**  
  Department of Computer Science  
  Columbia University  
  New York, New York
- **Jonathan de Halleux**  
  Microsoft Research  
  Redmond, Washington
- **Jörg Kienzle**  
  School of Computer Science  
  McGill University  
  Montréal, Québec, Canada
- **Thomas Debeauvais**  
  Department of Informatics  
  University of California, Irvine  
  Irvine, California

## Introducing Computer Games and Software Engineering

Kendra M.L. Cooper and Walt Scacchi

### CONTENTS

- 1.1 Emerging Field of Computer Games and Software Engineering — 1
- 1.2 Brief History of Computer Game Software Development — 3
- 1.3 Topics in Computer Games and Software Engineering — 6
  - 1.3.1 Computer Games and SEE — 6
  - 1.3.2 Game Software Requirements Engineering — 8
  - 1.3.3 Game Software Architecture Design — 8
  - 1.3.4 Game Software Playtesting and User Experience — 9
  - 1.3.5 Game Software Reuse — 10
  - 1.3.6 Game Services and Scalability Infrastructure — 11
- 1.4 Emergence of a Community of Interest in CGSE — 12
- 1.5 Introducing the Chapters and Research Contributions — 14
- 1.6 Summary — 24
- Acknowledgments — 25
- References — 25

### 1.1 Emerging Field of Computer Games and Software Engineering

Computer games (CGs) are rich, complex, and often large-scale software applications. CGs are a significant, interesting, and often compelling software application domain for innovative research in software engineering (SE) techniques and technologies. CGs are progressively changing the everyday world in many positive ways (Reeves and Read 2009). Game developers, whether focusing on entertainment-market opportunities or game-based applications in nonentertainment domains such as education, health care, defense, or scientific research (serious games or games with a purpose), thus share a common community of interest in how to best engineer game software.

There are many different and distinct types of games, game engines, and game platforms, much like there are many different and distinct types of software applications, information systems, and computing systems used for business. Understanding how games as a software system are developed to operate on a particular game platform requires identifying what types of games (i.e., game genre) are available in the market. Popular game genres include action or first-person shooters, adventure, role-playing game (RPG), fighting, racing, simulations, sports, strategy and real-time strategy, music and rhythm, parlor (board and card games), puzzles, educational or training, and massively multiplayer online games (MMOGs). This suggests that knowledge about one type of game (e.g., RPGs such as *Dungeons and Dragons*) does not subsume, contain, or provide the game play experience, player control interface, game play scenarios, or player actions found in other types of games. Therefore, being highly skilled in the art of one type of game software development (e.g., building a turn-taking RPG) does not imply an equivalent level of skill in developing another type of game software (e.g., a continuous play twitch or action game). This is analogous to saying that if a software developer is skilled in payroll and accounting software application systems, this does not imply that such a developer is also competent or skilled in the development of enterprise database management or e-commerce product sales over the web systems. The differences can be profound, and the developers’ skills and expertise narrowly specialized.

Conversely, similar games, such as card or board games, raise the obvious possibility for a single game engine to be developed and shared or reused to support multiple game kinds of a single type. Game engines provide a runtime environment and reusable components for common game-related tasks, which leaves the developers free to focus on the unique aspects of their game. For example, the games checkers and chess are played on an 8 × 8 checkerboard; though the shape and appearance of the game play pieces differ and the rules of game play differ, the kinds of player actions involved in playing either chess or checkers are the same (picking a piece and moving it to a square allowed by the rules of the game). Therefore, being skilled in the art of developing a game of checkers can suggest the ability or competent skill in developing a similar game like chess, especially if both games can use the same game engine. However, this is feasible only when the game engine is designed to allow for distinct sets of game rules and distinct appearance of game pieces—that is, the game engine must be designed for reuse or extension. This design goal is not always an obvious engineering choice, and it is one that increases the initial cost of game engine development (Bishop et al. 1998; Gregory 2009). Subsequently, developing software for different kinds of games of the same type, or using the same game engine, requires a higher level of technical skill and competence in software development than designing an individual game of a given type.

Understanding how game software operates on a game platform requires an understanding of the game device (e.g., Nintendo GameBoy, Microsoft Xbox One, Apple iPhone) and the internal software run-time environment that enables its intended operation and data communication capabilities. A game platform constrains the game design in terms of its architectural structure, how it functions, how the game player controls the game device through its interfaces (keyboard, buttons, stylus, etc.) and video/audio displays, and how they affect game data transmission and reception in a multiplayer game network.

### 1.2 Brief History of Computer Game Software Development

Game software researchers and developers have been exploring computer game software engineering (CGSE) from a number of perspectives for many years. Many are rooted in the history of CG development, much of which is beyond what we address here, as are topics arising from many important and foundational studies of games as new media and as cultural practice. However, it may be reasonable to anticipate new game studies that focus on topics such as how best to develop CGs for play across global cultures or through multisite, global SE practices.

The history of techniques for CG software development goes back many decades, far enough to coincide with the emergence of SE as a field of research and practices in the late 1960s. As CG software development was new and unfamiliar, people benefitted from publications of open source game software, often written in programming languages such as Fortran (Spencer 1968). Before that, interest in computer-based playing against human opponents in popular parlor games such as chess,
