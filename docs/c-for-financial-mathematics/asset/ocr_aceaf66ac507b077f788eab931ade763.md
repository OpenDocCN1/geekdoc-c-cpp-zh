![](bbox=[0.15, 0.1, 0.86, 0.61])

**FIGURE 18.6:** UML summary of changes to FMLib

NeutralPricePaths that create `MarketSimulation` objects according to the configuration of the model.

Internally the `MultiStockModel` stores most of its data using matrices. For example, the current stock prices are stored as $n \times 1$ matrix—i.e., a column vector. Each of these stock prices corresponds to the price of some stock in the market. The mapping between the names of the stocks and the index of the stock in this column vector is stored in two different ways. Firstly they are stored in an `unordered_map` called `stockToIndex` which maps the name of a stock to the index. Secondly the names are stored in index order in a `vector` called `stockNames`. Together these data structures allow one to quickly map between stock names and indices and vice versa. To help with this mapping,