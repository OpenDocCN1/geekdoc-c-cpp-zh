
Grady, Robert B. *Practical Software Metrics for Project Management and Process Improvement*. Englewood Cliffs, NJ: Prentice Hall PTR, 1992. Grady describes lessons learned from establishing a software-measurement program at Hewlett-Packard and tells you how to establish a software-measurement program in your organization.

Conte, S. D., H. E. Dunsmore, and V. Y. Shen. *Software Engineering Metrics and Models*. Menlo Park, CA: Benjamin/Cummings, 1986. This book catalogs current knowledge of software measurement circa 1986, including commonly used measurements, experimental techniques, and criteria for evaluating experimental results.

Basili, Victor R., et al. 2002. “Lessons learned from 25 years of process improvement: The Rise and Fall of the NASA Software Engineering Laboratory,” *Proceedings of the 24th International Conference on Software Engineering*. Orlando, FL, 2002. This paper catalogs lessons learned by one of the world’s most sophisticated software-development organizations. The lessons focus on measurement topics.

NASA Software Engineering Laboratory. *Software Measurement Guidebook*, June 1995, NASA-GB-001-94. This guidebook of about 100 pages is probably the best source of practical information on how to set up and run a measurement program. It can be downloaded from NASA’s website.

Gilb, Tom. *Competitive Engineering*. Boston, MA: Addison-Wesley, 2004. This book presents a measurement-focused approach to defining requirements, evaluating designs, measuring quality, and, in general, managing projects. It can be downloaded from Gilb’s website.

## 28.5 Treating Programmers as People

![](img/649c8eee28c38ca1e062691e45dc9883_716_0.png)

The abstractness of the programming activity calls for an offsetting naturalness in the office environment and rich contacts among coworkers. Highly technical companies offer parklike corporate campuses, organic organizational structures, comfortable offices, and other “high-touch” environmental features to balance the intense, sometimes arid intellectuality of the work itself. The most successful technical companies combine elements of high-tech and high-touch (Naisbitt 1982). This section describes ways in which programmers are more than organic reflections of their silicon alter egos.

## How Do Programmers Spend Their Time?

Programmers spend their time programming, but they also spend time in meetings, on training, on reading their mail, and on just thinking. A 1964 study at Bell Laboratories found that programmers spent their time this way as described in Table 28-3.

### Table 28-3 One View of How Programmers Spend Their Time

| Activity | Source Code | Business | Personal | Meetings | Training | Mail/Misc. Documents | Technical Manuals | Operating Procedures, Misc. | Program Test | Totals |
|---|---|---|---|---|---|---|---|---|---|---|
| Talk or listen | 4% | 17% | 7% | 3% |  |  |  | 1% |  | 32% |
| Talk with manager |  | 1% |  |  |  |  |  |  |  | 1% |
| Telephone |  | 2% | 1% |  |  |  |  |  |  | 3% |
| Read | 14% |  |  |  |  | 2% | 2% |  |  | 18% |
| Write/record | 13% |  |  |  |  | 1% |  |  |  | 14% |
| Away or out |  | 4% | 1% | 4% | 6% |  |  |  |  | 15% |
| Walking | 2% | 2% | 1% |  |  | 1% |  |  |  | 6% |
| Miscellaneous | 2% | 3% | 3% |  |  | 1% |  | 1% | 1% | 11% |
| Totals | 35% | 29% | 13% | 7% | 6% | 5% | 2% | 2% | 1% | 100% |
| Source: "Research Studies of Programmers and Programming" (Bairdain 1964, reported in Boehm 1981). |

This data is based on a time-and-motion study of 70 programmers. The data is old, and the proportions of time spent in the different activities would vary among programmers, but the results are nonetheless thought-provoking. About 30 percent of a programmer's time is spent in nontechnical activities that don't directly help the project: walking, personal business, and so on. Programmers in this study spent six percent of their time walking; that's about 2.5 hours a week, about 125 hours a year. That might not seem like much until you realize that programmers spend as much time each year walking as they spend in training, three times as much time as they spend reading technical manuals, and six times as much as they spend talking with their managers. I personally have not seen much change in this pattern today.

## Variation in Performance and Quality

![](img/649c8eee28c38ca1e062691e45dc9883_717_0.png)

Talent and effort among individual programmers vary tremendously, as they do in all fields. One study found that in a variety of professions—writing, football, invention, police work, and aircraft piloting—the top 20 percent of the people produced about 50 percent of the output (Augustine 1979). The results of the study are based on an analysis of productivity data, such as touchdowns, patents, solved cases, and so on. Since some people make no tangible contribution whatsoever and weren't considered in the study (quarterbacks who make no touchdowns, inventors who own no patents, detectives who don't close cases, and so on), the data probably understates the actual variation in productivity.

## Individual Variation

![](img/649c8eee28c38ca1e062691e45dc9883_718_0.png)

The original study that showed huge variations in individual programming productivity was conducted in the late 1960s by Sackman, Erikson, and Grant (1968). They studied professional programmers with an average of 7 years’ experience and found that the ratio of initial coding time between the best and worst programmers was about 20 to 1, the ratio of debugging times over 25 to 1, of program size 5 to 1, and of program execution speed about 10 to 1. They found no relationship between a programmer’s amount of experience and code quality or productivity.

![](img/649c8eee28c38ca1e062691e45dc9883_718_1.png)

Although specific ratios such as 25 to 1 aren’t particularly meaningful, more general statements such as “There are order-of-magnitude differences among programmers” are meaningful and have been confirmed by many other studies of professional programmers (Curtis 1981, Mills 1983, DeMarco and Lister 1985, Curtis et al. 1986, Card 1987, Boehm and Papaccio 1988, Valett and McGarry 1989, Boehm et al. 2000).

## Team Variation

Programming teams also exhibit sizable differences in software quality and productivity. Good programmers tend to cluster, as do bad programmers, an observation that has been confirmed by a study of 166 professional programmers from 18 organizations (Demarco and Lister 1999).

![](img/649c8eee28c38ca1e062691e45dc9883_718_2.png)

In one study of seven identical projects, the efforts expended varied by a factor of 3.4 to 1 and program sizes by a factor of 3 to 1 (Boehm, Gray, and Seewaldt 1984). In spite of the productivity range, the programmers in this study were not a diverse group. They were all professional programmers with several years of experience who were enrolled in a computer-science graduate program. It’s reasonable to assume that a study of a less homogeneous group would turn up even greater differences.

An earlier study of programming teams observed a 5-to-1 difference in program size and a 2.6-to-1 variation in the time required for a team to complete the same project (Weinberg and Schulman 1974).

![](img/649c8eee28c38ca1e062691e45dc9883_718_3.png)

After reviewing more than 20 years of data in constructing the Cocomo II estimation model, Barry Boehm and other researchers concluded that developing a program with a team in the 15th percentile of programmers ranked by ability typically requires about 3.5 times as many work-months as developing a program with a team in the 90th percentile (Boehm et al. 2000). Boehm and other researchers have found that 80 percent of the contribution comes from 20 percent of the contributors (Boehm 1987b).

The implication for recruiting and hiring is clear. If you have to pay more to get a top-10-percent programmer rather than a bottom-10-percent programmer, jump at the chance. You’ll get an immediate payoff in the quality and productivity of the programmer you hire, and you’ll get a residual effect in the quality and productivity of the other programmers your organization is able to retain because good programmers tend to cluster.

## Religious Issues

Managers of programming projects aren’t always aware that certain programming issues are matters of religion. If you’re a manager and you try to require compliance with certain programming practices, you’re inviting your programmers’ ire. Here’s a list of religious issues:

- Programming language
- Indentation style
- Placing of braces
- Choice of IDE
- Commenting style
- Efficiency vs. readability tradeoffs
- Choice of methodology—for example, Scrum vs. Extreme Programming vs. evolutionary delivery
- Programming utilities
- Naming conventions
- Use of gotos
- Use of global variables
- Measurements, especially productivity measures such as lines of code per day

The common denominator among these topics is that a programmer’s position on each is a reflection of personal style. If you think you need to control a programmer in any of these religious areas, consider these points:

*Be aware that you’re dealing with a sensitive area* Sound out the programmer on each emotional topic before jumping in with both feet.

*Use “suggestions” or “guidelines” with respect to the area* Avoid setting rigid “rules” or “standards.”

*Finesse the issues you can by sidestepping explicit mandates* To finesse indentation style or brace placement, require source code to be run through a pretty-printer for matter before it’s declared finished. Let the pretty printer do the formatting. To finesse commenting style, require that all code be reviewed and that unclear code be modified until it’s clear.
