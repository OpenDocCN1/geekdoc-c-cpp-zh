fixed interest rate $r$ if and only if

```
$$\underline{\eta}_{(i)} = r - \frac{1}{2} A_{(i,i)} .$$
```

In addition we see that the vector $\underline{\eta}$ can be computed from the individual drifts of each stock.

# 18.12 Using the Standard Template Library in FMLib

We wish to enhance FMLib so that it is possible to price a portfolio which contains options on more than one stock. In addition we would like to be able to price options such as a Margrabe option where the contract involves the interaction of two stocks (see Exercise 18.12.2).

The key changes we need to make to FMLib are summarised in Figure 18.6. Let us also explain them in words.

The **ContinuousTimeOption** interface is changed so that its payoff function now takes a **MarketSimulation** object as a parameter. The previous version of this function took a matrix of stock price paths as a parameter.

The **MarketSimulation** class is a simple class that stores a map between the name of a stock and a matrix of stock price paths. It stores all our simulations of the stock market. In order to compute the payoff of an option on multiple stocks, one queries the **MarketSimulation** for the price paths for each of the stocks involved in the option contract. One can now compute the payoff of the option according to the option contract.

In addition to changing the payoff function, the **ContinuousTimeOption** now has a method **getStocks** which can be used to query which stocks the option depends upon. To ensure that this method does not return duplicates, its return type is **set<string>**.

Most options involve only a single stock, so our base class **ContinuousTimeOptionBase** has been enhanced so that it stores the name of a single stock. It implements **getStocks** by returning this name. **ContinuousTimeOptionBase** also implements the payoff function that takes a **MarketSimulation** as a parameter by extracting the matrix of stock price paths for this single stock and then calling an abstract function, which is also called **payoff** but which takes a single **Matrix** as parameter. Since all our existing subclasses of **ContinuousTimeOptionBase** already implement this second version of the payoff function, they will now automatically implement the modified **ContinuousTimeOption** interface.

To generate the **MarketSimulation** objects we use a class called **MultiStockModel**. This class represents the mathematical model for multiple stocks described above. It has functions **generatePricePaths** and **generateRisk-