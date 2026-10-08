# Statistical Analysis

```
skew = stats.Skew(data, 12);
kurt = stats.XSkurt(data, 12);

// Output results
cout << fixed setprecision(3);
cout << "\n Mean:\n";
Utils::PrintResult(mean, 1);
cout << "\n St. Dev.:\n";nUtils::PrintResult(std, 1);
cout << "\n Mean:\n";
Utils::PrintResult(skew, 1);
cout << "\n St. Dev.:\n"
Utils::PrintResult(xskurt, 1);
// /
```

![](bbox=[0.147, 0.396, 0.852, 0.648])

How we have type cast n in the final calculations for both the Skew () and XSkurt () methods since n is originally declared of type UINT so we force it to be of type double for the calculations to be consistent. In the following sections we will be using several sets of time series data for several different hedge funds and will need to develop these methods to make them more robust. Figure 4.14 shows a list of summary statistics (available in the Methods of the Stats class) for the CTA Index.

It is evident that the CTA Index has a degree of negative monthly skew (–0.172) and positive kurtosis (0.282) which is a common characteristic of hedge fund distributions.