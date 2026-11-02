The model accepts any combination of inputs from the set

$$X = \{nickel, dime, quarter, cancel, wait\}$$

and produces combinations of output from the set

$$Y = \{nickel, dime, quarter, coffee, nothing\}$$

Inputs to the model are bags of values from $X$ and outputs are bags of values from $Y$. A bag (sometimes called a *multiset*) is an unordered collection. For example, the bag {nickel, nickel, dime} contains two nickels and a dime, a total value of 25 cents. The empty bag, like the empty set, is denoted by ∅. The union of two bags is the same as the union of two sets except that duplicates are permitted. For example, {nickel, nickel, dime} ∪ {dime} = {nickel, nickel, dime, dime}. The empty bag is an identity for the union operator: for any bag $X$, $X \cup \varnothing = X$.

The order in which items are listed does not matter. For example, {nickel, dime, nickel} is equal to {nickel, nickel, dime}. Consequently, the machine must produce an identical result if, when in any particular state $s$, it is provided with either of these values. It is necessary, for example, that

$$\delta(s, \{nickel, nickel, dime\}) = \delta(s, \{nickel, dime, nickel\})$$

The inventory of coins, the value of the coins inserted by the current customer, and the status of the CANCEL button constitute the state of the model. The variables $n$, $d$, and $q$ are the number of nickels, dimes, and quarters in the inventory. The variable $v$ is the total value of the coins put into the machine by the current customer. The variable $cancel$ is true if the CANCEL button is depressed and false otherwise.

The state transition function for this machine is defined by Algorithm 3.3, which is written in the form of a method for an object whose member variables are the machine's state variables. The method's single argument is a bag $x^b$ of inputs in $X$. The method *getCoins*, which is implemented by Algorithm 3.4, returns a bag of coins selected from the machine's inventory and with a total value equal to its argument. The state transition function begins by deducting, if possible, a dollar from the value of the unspent coins previously inserted by the customer. Any new coins are then added to the customer's total value and the inventory of the machine. The status of the CANCEL button is established last.

Algorithm 3.5 defines the model's output function, and it is in the same form. This method returns a bag $y^b$ of elements in the output set $Y$. If there is at least \$1 in the machine then it produces a cup of coffee. If the CANCEL button has been pressed, then the machine returns the customer's change. If a cup of coffee was also sold, then only the unspent coins are returned.

Table 3.2 shows two experiments with this model. Once again, we see the semi-group property in action. That the state transition function is in fact a function can be verified by checking that a change in the order of the items in the input bags does not change the outcome of the simulation.