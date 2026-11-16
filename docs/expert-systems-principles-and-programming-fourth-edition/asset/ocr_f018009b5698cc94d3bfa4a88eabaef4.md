We can now use induction to infer the winning strategy for the 15 + 3N Game, where N is any natural number 1, 2, 3, ... by thinking of the game as analogous to a tic-tac-toe board, which is analogous to a magic square of values:

{1+N, 2+N, 3+N, 4+N, 5+N, 6+N, 7+N, 8+N, 9+N}

Using the analogy of the order 3 square for games of three moves, by induction we can infer that magic squares of higher order can be used for games involving more than three moves. For example, the magic square of order 4:

| 16 | 3 | 2 | 13 |
|---|---|---|---|
| 5 | 10 | 11 | 8 |
| 9 | 6 | 7 | 12 |
| 4 | 15 | 14 | 1 |

allows you to pick the winning strategy of the four-move, 34 game, by thinking of it in terms of tic-tac-toe. In contrast to the one standard order 3 square, there are 880 standard squares of order 4, which allows considerably more games.

Reasoning by analogy is an important part of commonsense reasoning, which is very difficult for computers (and children). Other applications of analogy have been being learning.

# Generate-and-Test

Another method of inference is the classic AI strategy of generate-and-test, sometimes called generation and test, which involves the generation of a likely solution and then testing it to see if the proposed solution meets all the requirements. If the solution is satisfactory, then quit, else generate a new solution, test again, and so forth. This method was used in the first expert system, DENDRAL, conceived in 1965, to aid in identifying organic molecular structures. Data from an unknown sample are supplied by a mass spectrometer and input to DENDRAL, which generates all the potential molecular structures that could produce the unknown spectrum. DENDRAL then tests the most likely candidate molecules by simulating their mass spectrograms and comparing the results to the original unknown. Another program that uses generate-and-test is the Artificial Mathematician program to infer new mathematical concepts.

In order to reduce the enormous number of potential solutions, generate-and-test is normally used with a planning program to limit the likely potential solutions for generation. This variation is called plan-generate-test and is used for efficiency in many systems. For example, the medical diagnosis expert system MYCIN also has the capability of planning a therapeutic drug treatment after a patient's disease has been diagnosed. A plan is essentially finding chains of rules or inferences that connect a problem with a solution, or goal, with the evidence to support it. Planning is most efficiently done by simultaneously searching forward from the facts and backward from the goal.

The MYCIN planner first creates a prioritized list of therapeutic drugs to which the patient is sensitive. In order to reduce undesirable drug interactions,