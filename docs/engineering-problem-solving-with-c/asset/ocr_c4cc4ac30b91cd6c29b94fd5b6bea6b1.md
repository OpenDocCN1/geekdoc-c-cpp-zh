# 10.9 Problem Solving Applied: Iterated Prisoner's Dilemma

The iterated prisoner's dilemma (IPD) is a popular game from game theory. The traditional form of the prisoner's dilemma game has two players. Each player must choose between one of two possible moves: defect or cooperate. The combination of your move and your opponent's move determines some form of payoff, usually represented as a score.

The name “prisoner’s dilemma” is derived from the following situation: Two prisoners are serving time for a minor offense. However, both are suspected of having committed a far more serious crime. The police approach each prisoner, privately, with the same deal. Each is given the choice between

+   1. implicating the other prisoner (i.e., defect, relative to the other prisoner) and thereby getting paroled
+   2. not implicating the other prisoner (i.e., cooperate, relative to the other prisoner) and thereby continuing to serve time for the minor offense.

In this example, each suspect has only one move and one payoff. If both cooperate, each continues to serve their remaining time in prison. If both defect, each gets paroled; however, each is then convicted of the more serious crime and must serve a new, longer jail sentence. If one defects and the other cooperates, the defector goes free, and the cooperator spends a lot of time behind bars. What would you do in this situation? What do you hope your fellow prisoner does? How will you behave towards your fellow prisoner in the future if he or she implicates you in the crime? This situation is the basis for interesting research in many areas, including political science, biology, and economics.

In the implementation of the IPD game, you will have repeated interactions with your opponent, rather than just one, thus the name *iterated* prisoner’s dilemma. Your first move in the game, cooperate or defect, will be decided with no knowledge of how your opponent will move. However, on all subsequent moves you can decide whether to cooperate or defect based on your opponent’s last move. This is when strategy becomes interesting.

You will be competing with your opponent, and you will also be competing with other players who will be playing against you and your opponents. The goal of the game is to accumulate the maximum number of points in a given number of moves. The payoff table for the prisoner’s dilemma is as follows:

# IPD Payoff Table

| | cooperate | defect |
| :--- | :--- | :--- |
| cooperate | 3,3 | 0,5 |
| defect | 5,0 | 1,1 |

If you look at the table carefully, you will notice that the highest payoff occurs when your opponent cooperates and you defect. However, if both players cooperate, each player will receive a higher payoff than if both had defected.

If the game consisted of only one move, then you could argue that it is rational to defect on the first move to give yourself the best chance of winning the game, since you will not encounter your opponent again. However, since you will encounter your opponent multiple