
environment that helps developers to achieve a flow state, a technique that has been found to lead to increased engagement and addiction [14]. Although typically viewed as negative behavior, controlled addiction can be beneficial, when the behavior is productive, as in the case of software testing addiction. These methods try to motivate players similar to what is suggested in Reference [15].

### 4.2.3 Software Design

In our experience, students in early computer science classes do not understand or appreciate software design. We believe that this is largely because all the early programming they have done focuses on “getting it working.” Further, typical early CS assignments are a few hundred lines of Java code. Finally, most introductory CS courses at Columbia University (and other universities [16]) typically have only individual assignments and allow no collaboration on the assignments. When programs become larger and when you have to work in large teams, software design becomes a lot more critical.

Our goal was to inculcate good software design principles via a competitive tournament where participation would be contingent based on the students’ code adhering to good design principles.

## 4.3 Gameful Testing Using HALO

As we have found that students do not test as thoroughly as they ought to, we use HALO to make software testing more enjoyable and fun. For example, students are given a number of “quests” that they need to complete. These quests are used to disguise standard software testing techniques such as white and black box testing, unit testing, and boundary value analysis. Upon completing these quests, the students get social rewards in the form of achievements, titles, and experience points. They can see how they are doing compared to other students in the class. Although the students think they are competing just for points and achievements, the primary benefit of such a system is that the students’ code gets tested a lot better than it normally would have. Our current prototype implementation of HALO is a plug-in for Eclipse and a screenshot is shown in Figure 4.1.

### 4.3.1 HALO Plug-In for Eclipse

We used HALO in a class taught at Columbia University: COMS 1007—Object-Oriented Programming and Design with Java. The rest of this section describes some background about the class, how HALO was used, and the results of our case study.

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_107_0.png)

FIGURE 4.1  The HALO Eclipse plug-in: The bottom part shows the dashboard, which keeps track of the achievements, experience points, and leaderboards; the top-right part shows the quest list and progress.

### 4.3.2 COMS 1007—Object-Oriented Programming and Design with Java

COMS 1007—Object-Oriented Programming and Design with Java was the second course in the track for CS majors and minors at Columbia University. The class was also required for majors in several other engineering disciplines, including electrical engineering and industrial engineering, and was used by other students to satisfy their general science or computer science requirement. The first author taught this course in Spring (January–May) 2012.¹ The course goals were as follows: A rigorous treatment of object-oriented concepts using Java as an example language and development of sound programming and design skills, problem-solving and modeling of real-world problems from science, engineering, and economics using the object-oriented paradigm [17]. The prerequisite for the course was familiarity with programming and Java (demonstrated through a successful completion of the CS1 course at Columbia or another university, or passing marks on the AP Computer Science Exam).

In Spring 2012, the class enrollment was 129, which consisted largely of freshmen and sophomores (first- and second-year undergraduates, respectively). The list of topics covered was object-oriented design, design patterns, interfaces, graphics programming, inheritance and abstract classes, networking, and multithreading and synchronization. There were five roughly biweekly assignments, which contained both theory and programming, one midterm exam, and one final exam.

As explained above, HALO uses game elements and motifs from popular games such as *World of Warcraft* [8] to make the whole software engineering process and, in particular, the software testing process more engaging and social. HALO is not a game; it leverages game mechanics and applies them to the software development process. We now describe how we used HALO in our class.

### 4.3.3 A Case Study with HALO

In this class, we used HALO for three assignments. In the first two cases, HALO was not a required part of the assignment; students could optionally use it if they wanted to. For the last case, students could earn extra credit (10 points for the assignment, accounting for 0.8% of the overall course grade) by completing the HALO quests.

The final course assignment allowed students to design their own projects, making it difficult for us to predefine HALO quests, because each project was different. Instead, students were offered extra credit in exchange for creating HALO quests for their projects, thus emphasizing the *learning by example* pedagogy. Out of the 124 students who submitted Assignment 5, 77 students (62.1%) attempted the extra credit, and 71 out of these 77 students (92.21%) got a perfect score for the HALO quests that they had created.

### 4.3.3.1 *An Assignment on Java Networking: Getting and Analyzing Data from the Internet—The CIA World Factbook*

We now describe an assignment that was given to the class and the HALO quests that were created for it. The rest of the assignments and the quests are described in our technical report [18].

The Central Intelligence Agency (CIA) has an excellent collection of detailed information about each country in the world, called the CIA *World Factbook*. For this assignment, students had to write a program in Java to analyze data from the CIA *World Factbook* website, interacting directly with the website. The student programs had to interactively answer questions such as the following:

- 1. List countries in *South America* that are prone to *earthquakes*.
- 2. Find the country with the lowest elevation point in *Europe*.
- 3. List all countries in the *southeastern* hemisphere.
- 4. List all countries in *Asia* with more than *10* political parties.
- 5. Find all countries that have the color *blue* in their flag.
- 6. Find the top *five* countries with the highest electricity consumption per capita (electricity consumption as a percentage of population).
- 7. Find countries that are entirely landlocked by a single country.

For the italicized parts in the above list, the code had to be able to deal with any similar input (e.g., from a user). This should not be hard-coded.

### 4.3.3.2 HALO Quests

We now describe the HALO quests that we used for the above assignment.

- 1. *TARDIS*—To interact with the CIA *World Factbook*, it would be nice to have a TARDIS. No, not like in the show, but a Java program that can transfer and read data from Internet sites. Completing this quest will reward you with 30 experience points (XP). This quest has two tasks:
  - a. *New Earth*—This will probably be your first program that talks to the Internet. Although this is not as complex as creating a new Earth, you should test out the basic functionality to make sure it works. Can your program read one page correctly? Can it read multiple pages? Can it read all of them?
  - b. *The Unicorn and the Wasp*—Just like Agatha Christie, you should be able to sift through all the information and find the important things. Are you able to filter information from the web page to get only the relevant data?
- 2. *EXTERMINATE! EXTERMINATE!*—The CIA Factbook has some unstructured data—not all of it is organized properly. This may not be as annoying (or life-threatening) as Daleks, but your programs should
