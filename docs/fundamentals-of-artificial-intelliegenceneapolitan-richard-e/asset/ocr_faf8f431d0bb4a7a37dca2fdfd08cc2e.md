+   (d) Let Diff be the difference of the number of advancing and declining securities. That McClellan Oscillator (MCCL) is as follows:

MCCL = 19-day EMA(Diff) - 39-day EMA(Diff).

Traders consider the market overbought when MCCL > 100 and oversold when MCCL < -100.

We denote this indicator simply as MCCL.

+   (e) The indicators SP500lag, MACDlag, MACD9lag, and MCCLlag are the values of those indicators on the previous day.

+   (f) Other terminal symbols include real constants in the interval [-1, 1].

All indicator values were normalized to the interval [-1, 1].

+   2. Decide on the function set F. Function symbols include +, -, and x, and the following control structures:

+   (a) if x > 0 then y else z. This structure is represented in the tree with the symbol IF having the children x, y, and z.

+   (b) if x > w then y else z. This structure is represented in the tree with the symbol IFGT having the children x, w, y, and z.

+   3. Decide on how many individuals make up a population. Various population sizes were tried. Sizes below 500 were ineffectual, whereas ones around 2500 had good results.

+   4. Decide how to initialize the population. Each initial individual was created by growing the tree as discussed in Section 9.3.1. The maximum number of levels allowed was 4 and the maximum number of total nodes allowed was 24. This restriction was also enforced in future populations. The purpose of these limitations was to avoid overfitting, which occurs when the tree matches the training data very closely but has limited predictive value for unseen data.

+   5. Decide on a fitness function. Data was obtained on the S&P closing prices from April 4, 1983, to June 18, 2004. A given tree analyzes the first 4750 days of this data. The tree starts with $1 on the first day. If the tree returns a value greater than 0 on a given day, a buy signal is generated, otherwise a sell signal is generated. All the current money is always invested or withdrawn when there is a buy or a sell. There are no partial investments. If the tree was in the market on the previous day and a buy signal is generated, no action is taken. Similarly, if the tree was out of the market on the previous day and a sell signal is generated, no action is taken. When the 4750 days of trading are complete, the initial dollar is subtracted so that the final value represents profit. To further avoid overfitting, a fitness penalty proportional to the total number of transactions was imposed.