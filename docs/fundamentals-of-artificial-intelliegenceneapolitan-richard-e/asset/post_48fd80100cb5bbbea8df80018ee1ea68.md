
![](img/67fa924962ee21b3590be9f3b10d9fe7_298_0.png)

Figure 9.7 A tree representing Expression 9.1.

Suppose we have the following mathematical expression (program):

```
$$\frac{x+2}{5-3 \times x}$$ (9.1)
```

Its tree structure representation appears in Figure 9.7.

## 9.3.1 Illustrative Example

A simple way to illustrate genetic programming is to show an application that learns a function $y = f(x)$ from pairs of points $(x_i, y_i)$ known to satisfy the function. For example, suppose we have the pairs of points in Table 9.9.

These points were actually generated from the function

```
$y = x^2/2.$
```

However, we are assuming that we do not know this, and are trying to discover the function. Steps for developing a genetic program for this discovery problem are as follows:

- 1. Decide on the terminal set T. Let the terminal set include the symbol x and the integers between -5 and 5.

- 2. Decide on the function set F. Let the function set be the symbols +, -, x, and /. Note that we could include other functions such as sin, cos, etc. if desired.

- 3. Decide on how many individuals make up a population. Our population size will be 600.

Table 9.9 We Want to Learn a Function that Describes the Relationship between x and y Based on These 10 Points.

| x | y |
|---|---|
| 0 | 0 |
| .1 | .005 |
| .2 | .020 |
| .3 | .045 |
| .4 | .080 |
| .5 | .125 |
| .6 | .180 |
| .7 | .245 |
| .8 | .320 |
| .9 | .405 |

- 4. Decide how to initialize the population. Each initial individual is created by a process called **growing the tree**. First, a symbol is randomly generated from $T \cup F$. If it is a terminal symbol, we stop and our tree consists of a single node containing this symbol. If it is a function symbol, we randomly generate children for this symbol. We continue down the tree, randomly generating symbols and stopping at terminal symbols. For example, the tree in Figure 9.7 would be obtained by the following random generation of symbols: First the symbol / is generated, followed by the values of + and - for its children. The children generated for + are x and 2. We stop at each of these children. The children generated for - are 5 and x. We stop at the 5, and finally generate the children 3 and x for the x.

- 5. Decide on a fitness function. The fitness function will be the square error. That is, the fitness of function $f(x)$ is as follows:

$$\sum_{i=1}^{10} (f(x_i) - y_i)^2,$$

where each $(x_i, y_i)$ is a point in Table 9.9. Functions with smaller errors are more fit.

- 6. Decide on which individuals to select for reproduction. A 4 individual tournament selection process is used. In the **tournament selection process**, $n$ individuals are randomly selected from the population. In this case, $n = 4$. We say that these $n$ individuals enter a tournament in which the $n/2$ most fit of them win and the $n/2$ least fit lose. The $n/2$ winners are allowed to reproduce to produce $n/2$ children. These children replace the $n/2$ losers in the population for the next generation. In this case, the 2 winners reproduce twice to produce 2 children who replace the 2 losers.

![](img/67fa924962ee21b3590be9f3b10d9fe7_300_0.png)

Figure 9.8 Crossover by exchanging subtrees.

A small tournament size results in low selection process, whereas a high tournament size results in high pressure.

- 7. Decide on how to perform crossovers and mutations. Crossover between two individuals will be performed by exchanging randomly selected subtrees. Such a crossover is illustrated in Figure 9.8. Mutations are performed by randomly selecting a node and replacing the subtree at that node by growing a new subtree. Mutations are randomly performed on 5% of the offspring.

- 8. Decide when to terminate. Terminate when the square error of the most fit individual is 0 or when 100 generations have been produced.

Banzhaf et al. [1998] applied the technique just presented to the data in Table 9.9. The following shows the most fit individual in the first 4 generations:

| Generation | Most Fit Individual |
|---|---|
| 1 | \(\frac{x}{3}\) |
| 2 | \(\frac{x}{6 - 3x}\) |
| 3 | \(\frac{x}{x(x - 4) - 1 + \frac{4}{x} - \frac{\frac{9(x+1)}{x}}{6-3x}}\) |
| 4 | \(\frac{x^2}{2}\) |

The most fit individual had expanded to a very large tree by generation 3 but shrunk back down to the correct solution (the function generating the data) by generation 4.

## 9.3.2 Artificial Ant

Consider the problem of developing a robotic ant that navigates along a trail of food. Figure 9.9 shows such a trail called the “Sante Fe trail.” Each black square represents one pellet of food; there are 89 such squares. The ant starts at the square labeled “start” facing right, and its goal is to arrive at the square labeled “89” after visiting all 89 black squares (thereby eating all the food on the trail) in as few time steps as possible. Notice that there are a number of gaps along the trail. The problem with a time limit represents a challenging planning problem.

The ant has one sensor as follows:

- * **food_ahead**: Has value True if there is food in the square the ant is facing; otherwise has value False.

There are three different actions the ant can execute in each time slot:

- * **right**: The ant turns right by 90° (without moving).
- * **left**: The ant turns left by 90° (without moving).
- * **move**: The ant moves forward into the square it is facing. If the square contains food, the ant eats the food, thereby eliminating the food from the square and erasing it from the trail.

Koza [1992] developed the following genetic programming algorithm for this problem.

![](img/67fa924962ee21b3590be9f3b10d9fe7_302_0.png)

Figure 9.9 The Santa Fe trail. Each black square represents a pellet of food.

- 1. Decide on the terminal set T. The terminal set contains the actions the ant can take. That is,

  T = {right, left, move}.

- 2. Decide on the function set F. The function set is as follows:

  (a) if_food_ahead(instruction1, instruction2);
  (b) do2(instruction1, instruction2);
  (c) do3(instruction1, instruction2, instruction3);

The first function executes instruction1 if food_ahead is true; otherwise it executes instruction2. The second function unconditionally executes instruction1 and instruction2. The third function unconditionally executes instruction1, instruction2, and instruction3. For example,

```
do2(right, move)
```

causes the ant to turn right and then move ahead.

- 3. Decide on how many individuals make up a population. The population size is 500.

![](img/67fa924962ee21b3590be9f3b10d9fe7_303_0.png)

**Figure 9.10** The individual in generation 22 with a fitness equal to 89.

- 4. Decide how to initialize the population. Each initial individual is created by growing the tree (See Section 9.3.1).

- 5. Decide on a fitness function. It is assumed that each action (right,left,move) takes one time step, and each individual is allowed 400 time steps. Each individual starts in the upper left-hand square facing east. Fitness is defined to be the number of food pellets consumed in the allotted time. So the maximum fitness is 89.

- 6. Decide on which individuals to select for reproduction.

- 7. Decide on how to perform crossovers and mutations. Crossover between two individuals will be performed by exchanging randomly selected subtrees. Such a crossover is illustrated in Figure 9.8. Mutations are performed by randomly selecting a node and replacing the subtree at that node by growing a new subtree. Mutations are randomly performed on 5% of the offspring.

- 8. Decide when to terminate. Terminate when one individual has a fitness of 89 or some maximum amount of iterations is reached.

In each iteration, each individual in the population (program) is run repeatedly until 400 time steps are performed. The individual's fitness is then equal to 89 in the 22nd generation. That individual appears in Figure 9.10. The average fitness of individuals in generation 0 was 3.5, while the most fit individual in generation 0 had a fitness of 32.

## 9.3.3 Application to Financial Trading

An important decision facing everyone who invests in the stock and other financial markets is whether to buy, sell, or hold on a given day. There have been many efforts to develop automated systems that make this decision for us. Farnsworth et al. [2004] developed such a system using genetic programming. Their system makes an investment decision based on values of market indicators on a given day. We discuss that system next.

### 9.3.3.1 Developing the Trading System

First we show the eight steps using to create the system.

- 1. Decide on the terminal set T. The terminal symbols are the market indicators. The researchers tried and tested various indicators before deciding on the ones to include in the final system. We only present the final ones. They are as follows:

  (a) The S&P500 is a market index based on 500 leading companies in leading industries of the U.S. economy. For a given day, the indicator based on the S&P500 is as follows:

![](img/67fa924962ee21b3590be9f3b10d9fe7_304_0.png)

where $S\&P500_{today}$ is the value of the S&P500 on the current day, $S\&P500_{avg}$ is the average value over the past 200 days, and $S\&P500_{\sigma}$ is the standard deviation over the past 200 days. We denote this indicator simply as $SP500$.

  (b) The k-day Exponential Moving Average (EMA) for a security is a weighted average of the security over the past k days. The Moving Average Convergence/Divergence (MACD) of a security x is as follows:

![](img/67fa924962ee21b3590be9f3b10d9fe7_304_1.png)

The MACD is considered a momentum indicator. When it is positive, traders say upside momentum is increasing; when it is negative, they say downside momentum is increasing. A second indicator used in this system is $MACD(S\&P500)$, which we denote simply as $MACD$.

  (c) The indicator $MACD9$ is the 9-day EMA of the MACD of the S&P500.
