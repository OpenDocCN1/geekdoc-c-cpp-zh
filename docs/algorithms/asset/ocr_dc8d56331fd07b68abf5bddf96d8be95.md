# Chapter 4

# Algorithms 25

network, and there is a list $E'$ of pairs of which the new road can be built. Each potential road $e' \in E'$ has an associated length. As a designer for the public works you are asked to determine the road $e' \in E'$ whose addition to the existing network $G$ would result in the maximum decrease in the distance between two cities $s$ and $t$. Give an efficient algorithm for solving this problem.

4.21. Shortest path algorithms can be applied in currency trading. Let $c_1, c_2, \dots, c_n$ be various currencies; for instance, $c_1$ might be dollars, $c_2$ cents and $c_3$ like. For any two currencies $c_i$ and $c_j$, there is an exchange rate $r_{ij}$, this means that you can purchase $r_{ij}$ units of $c_j$ in exchange for one unit of $c_i$. These exchange rates satisfy the condition $r_{ij}r_{ji} < 1$, so if you start with a unit of $c_i$, change it into $c_j$ and then convert back to $c_i$, you end up with less than one unit of $c_i$ (the difference is the cost of the transaction).

+   (A) Give an algorithm for the following problem: Given a set of exchange rates $r_{ij}$ and two currencies $s$ and $t$, find the most advantageous sequence of currency exchanges for converting currency $s$ into currency $t$. Toward this goal, you should represent the currencies and by a graph whose edge lengths are real numbers.

The exchange rates are updated frequently, reflecting the demand and supply of various currencies. Occasionally the exchange rates satisfy the following property: there is a sequence of currencies $c_1, c_2, \dots, c_k$, such that $r_{c_1c_2}r_{c_2c_3} \dots r_{c_kc_1} > 1$. This means that by starting with a unit of $c_1$, and subsequently converting it to currencies $c_2, c_3, \dots, c_k$, and finally back to $c_1$, you would end up with more than one unit of currency $c_1$. Such anomalies last only a fraction of a minute on the currency exchange, but they provide an opportunity for risk-free profits.

+   (B) Give an algorithm for detecting the presence of such an anomaly. Use the graph representation you found above.

4.22. The tramp steamer problem. Suppose you are the owner of a ship that can travel between a group of port cities V. You make money at each port: a visit to city $i$ earns you a profit of $p_i$ dollars. Meanwhile, the transportation cost from port $i$ to port $j$ is $c_{ij} > 0$. You want to find a cyclic route in which the ratio of profit is maximized.

To this end, consider a directed graph $G = (V, E)$ whose nodes are ports, and has edges between each pair of ports. For any cycle $C$ in this graph, the profit-to-cost ratio is

```
$r(C) = \frac{\sum_{(i,j) \in C} p_i}{\sum_{(i,j) \in C} c_{ij}}$
```

Let $r^*$ be the maximum ratio achievable by a simple cycle. One way to determine $r^*$ is by binary search: by first guessing some ratio $r$, and then testing whether it is too large or too small.