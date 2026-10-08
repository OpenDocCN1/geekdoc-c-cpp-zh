out the computation of the amount of stock required to hedge into its own function, we highlight the essential feature of the delta hedging strategy compared to other stock hedging strategies. In addition this will make it easy to enhance the code to find out what happens if the trader decides to pursue another investment strategy.

Next follows a loop where we simulate trading at each intermediate time point.

```
for (int i = 0; i < nSteps-1; i++) {
    double balanceWithInterest = bankBalance *
        exp(simulationModel->riskFreeRate*dt);
    double S = pricePath[i];
    double date = dt*(i + 1);
    double newStockQuantity =
        selectStockQuantity(date, S);
    double costs =
        (newStockQuantity - stockQuantity)*S;
    bankBalance = balanceWithInterest - costs;
    stockQuantity = newStockQuantity;
}
```

This code corresponds to Equation (14.2).

Finally we need to consider what happens at maturity. This is addressed by the following code which completes the definition of `runSimulation`.

```
double balanceWithInterest = bankBalance *
    exp(simulationModel->riskFreeRate*dt);
double S = pricePath[nSteps - 1];
double stockValue = stockQuantity*S;
double payout = toHedge->payoff(S);
return balanceWithInterest + stockValue - payout;
}
```

This code corresponds to Equation (14.3).

# ### 14.2.3 Implementing the other methods of HedgingSimulator

The remaining details of the implementation of our HedgingSimulator class are extremely straightforward.

The `runSimulations` simply calls `runSimulation` multiple times and stores the results in a vector:

```
std::vector<double>
    HedgingSimulator::runSimulations(
        int nSimulations) const {
    std::vector<double> ret(nSimulations);
    for (int i = 0; i < nSimulations; i++) {
```