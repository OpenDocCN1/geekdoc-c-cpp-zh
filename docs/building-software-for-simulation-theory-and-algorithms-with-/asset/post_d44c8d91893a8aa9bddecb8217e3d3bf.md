
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

```
1 method δ(x^b)
2 Sell a cup of coffee
3 If v ≥ 100 then v ← v − 100
4 If cancel is pressed, clear it and return any change
5 if cancel = true then
6     cancel ← false
7     C ← getCoins(v)
8     n ← n − number of nickels in C
9     d ← d − number of dimes in C
10    q ← q − number of quarters in C
11    v ← 0
12 end
13 Add the coins inserted by the customer
14 n_c ← number of nickels in x^b, n ← n + n_c
15 d_c ← number of dimes in x^b, d ← d + d_c
16 q_c ← number of quarters in x^b, q ← q + q_c
17 v ← v + 5n_c + 10d_c + 25q_c
18 Check the cancel button
19 cancel ← cancel is in x^b
20 end method
```

### Algorithm 3.3 State transition function for the coffee-vending machine.

```
1 method getCoins(cents) returns C
2 Initialize the bag of coins
3 C ← ∅
4 Copy the inventory of the machine
5 q_c ← q, d_c ← d, n_c ← n
6 Pick quarters first
7 while q_c > 0 and cents ≥ 25 do
8     q_c ← q_c − 1, cents ← cents − 25
9     C ← C ∪ {quarter}
10 end
11 Pick dimes next
12 while d_c > 0 and cents ≥ 10 do
13    d_c ← d_c − 1, cents ← cents − 10
14    C ← C ∪ {dime}
15 end
16 Pick nickels last
17 while n_c > 0 and cents ≥ 5 do
18    n_c ← n_c − 1, cents ← cents − 5
19    C ← C ∪ {nickel}
20 end
21 return C
22 end method
```

### Algorithm 3.4 Definition of the *getCoins* method.

```
1  method λ() returns y^b
2    Initialize the output bag
3    y^b ← ∅
4    How much money has the customer put into the machine?
5    cash ← v
6    Sell a cup of coffee
7    if cash ≥ 100 then
8      y^b ← {coffee}
9      cash ← cash − 100
10   end
11   Expel any change that remains after the sale
12   if cancel = true then y^b ← y^b ∪ getCoins(cash)
13   If the bag is still empty, then the output is nothing
14   if y^b = ∅ then y^b ← {nothing}
15   return y^b
16 end method
```

**Algorithm 3.5** Output function for the coffee-vending machine.

### 3.1.4 Systems with Bags for Input and Output

Bags are so useful as the basic type of input and output to a model that we will include them in the definition of a system. The set of bags with elements in $X$ is denoted $X^b$. Similarly, the set of bags with elements in $Y$ is denoted $Y^b$. For example, if $Y = {nickel, dime, quarter}$, then ${nickel} ∈ Y^b$, ${nickel, nickel} ∈ Y^b$, and so is ${dime, nickel}$. The state transition function computes the next state of the model from its current state $s$ and a bag $x^b$ of inputs in $X$; it has the form

δ : S × X^b → S    (3.13)

The output function maps the current state $s$ to a bag $y^b$ of outputs in $Y$; its form is

λ : S → Y^b    (3.14)

These new forms do not change the definition of the total state transition function or the simulation algorithm for atomic models. Their significance is chiefly in how network models are defined and simulated, a topic that is addressed in Section 3.2.

### 3.1.5 A Simulator for Atomic Models

The simulation engine for atomic models has four classes: *Atomic*, *Simulator*, *EventListener*, and *Bag*. The *Bag* is a generic class for unordered collections of objects. It is used to supply input to and obtain output from the *Atomic* model. The *Bag* is a partial implementation of a multiple associative container as defined in the

## TABLE 3.2 Two Simulations of the Vending Machine

| s | Experiment 1 (x1) | Experiment 1 (y) | Experiment 2 (x2) | Experiment 2 (y) |
|---|---|---|---|---|
| 0 | {quarter, quarter, quarter, quarter, dime, nickel, dime}<br>q = 14, d = n = 10<br>v = 0<br>cancel = false | (nothing) | {quarter, quarter, quarter, quarter, dime, nickel, dime}<br>q = 14, d = n = 10<br>v = 0<br>cancel = false | (nothing) |
| 1 | {dime, dime, nickel}<br>q = 14, d = n = 11<br>v = 105<br>cancel = false | (coffee) | {dime, dime, nickel}<br>q = 17, d = 13, n = 10<br>v = 105<br>cancel = false | (coffee) |
| 2 | {quarter, quarter, quarter, quarter, dime, nickel, dime}<br>q = 14, d = n = 11<br>v = 115<br>cancel = false | (nothing) | {quarter, quarter, quarter, quarter, dime, nickel, dime}<br>q = 17, d = 13, n = 10<br>v = 105<br>cancel = true | (cancel) |
| 3 | {dime, dime, nickel}<br>q = 14, d = n = 11<br>v = 115<br>cancel = true | (dime, nickel) | {dime, dime, nickel}<br>q = 17, d = 13, n = 10<br>v = 5<br>cancel = true | (nickel) |
| 4 | {quarter, quarter, quarter, quarter, dime, nickel, dime}<br>q = 14, d = n = 10<br>v = 0<br>cancel = false | (nothing) | {quarter, quarter, quarter, quarter, dime, nickel, dime}<br>q = 17, d = 13, n = 9<br>v = 0<br>cancel = false | (nothing) |

C++ Standard Template Library (STL) (see, e.g., Ref. 60). It has methods to insert and remove objects, iterate through the contained objects, and determine the number of objects in the container.

The *EventListener* can be registered with the *Simulator*, which will notify the listener when the model produces output and changes its state. The *EventListener* has two abstract methods: *stateChange* and *outputEvent*. The *stateChange* method is called by the *Simulator* when the model changes its state. The *outputEvent* method is called when the model produces an output.

The *Simulator* has four methods: *addEventListener*, *getTime*, *computeNextState*, and *computeOutput*. The *addEventListener* method puts an *EventListener* into the list of listeners that are notified of changes to the model. The *getTime* method returns the simulation time at which the state was last computed. The *computeNextState* method does four things: (1) computes the model’s output function if this has not already been done, (2) computes the model’s next state, (3) notifies listeners of these actions, and (4) tells the model to clean up objects created by its output function. The *computeOutput* method invokes the model’s output function and informs registered *EventListeners* of the consequent output values; it does not change the state of the model.

Atomic models are derived from the abstract *Atomic* class, which defines the interface needed by the simulation algorithm. This class has two abstract methods: *delta* and *output_func*¹. The method *delta* implements the state transition function, and *output_func* implements the output function. The member variables of the derived class are the state variables of the model, and these are initialized by its constructor.

The *computeOutput* method is effective just once at each simulation time. Subsequent calls at the same simulation time have no effect. This design decision has two practical motivations: (1) it simplifies the management of output objects by cleaning them up just once at the end of the *computeNextState* method, and (2) the model’s *output_func* method is called just once at each simulation time; in practice, modelers often collect statistics, drive output devices, and perform other tasks in the *output_func* or in response to output that must be done just once at each simulation time.

The type of object in the model’s input–output set is specified with a template parameter. The decision to use a template class for building atomic models is strongly motivated by use of the C++ programming language. C++ is a strongly typed language and it lacks a built-in base class. Consequently, the simulation engine must know at compile time what types of objects will be produced and consumed by the model. A generic base class for atomic models, with a template for specifying the type of input and output, solves this problem and gives the programmer explicit control over how

¹Why not *lambda*? The symbol (or word) *delta* is commonly used to represent change. This usage is introduced in first- and second-year calculus and physics courses. Use of the symbol (or word) *lambda* for output is relatively uncommon. The method name *output_func* seemed, therefore, less likely to confuse the programmer.
