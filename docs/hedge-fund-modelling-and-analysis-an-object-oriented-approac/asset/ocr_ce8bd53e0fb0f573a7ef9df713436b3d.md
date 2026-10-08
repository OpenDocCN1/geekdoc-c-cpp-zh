```
return pp;
}

// ...
// main.cpp
// ...

// Create class instances
Import ctai;
RMetrics rmetrics;

// Declare and call GetData()
V2DD data = ctai.GetData("./data/cta_index.dat");

// Declare and call HistoricVaR() member function
DBL hvar = rmetrics.HistoricVaR(data, 95);

// Output results
cout << "\n Historic VaR = $" << fixed << setprecision(0) << hvar << "\n";
// ...
```

![](bbox=[0.125, 0.466, 0.848, 0.723])

# 7.3.2 Parametric Method

The parametric method does not require all of the data that the historic simulation requires but may use the data to determine parameters of the hedge fund return distribution. If we generally assume the hedge fund returns are consistent with a normal distribution then we only need two parameters to characterise the distribution, namely the mean, $\mu$ and standard deviation, $\sigma$. That is, once we have determined two