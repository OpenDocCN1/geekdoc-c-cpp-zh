**Table 1.1: Solutions to Example 5, showing the existence of 8 solutions**

| $x_1$ | $x_2$ | $x_3$ | $x_4$ | $x_5$ | $P$ | Frequency |
|---:|---:|---:|---:|---:|---:|---:|
| 0.98842 | 2.67366 | -1.88446 | -0.67341 | 0.21106 | 11.67664 | 21 |
| 1.03962 | 2.49153 | 1.78457 | -0.59958 | 0.15835 | 10.47324 | 97 |
| 1.37627 | -2.21617 | 1.77606 | -0.59704 | 0.23721 | 9.56909 | 2 |
| 2.22372 | -0.15747 | 1.98930 | -0.48910 | 0.25739 | 8.92702 | 6 |
| 1.56816 | -1.80074 | -1.75513 | -0.53053 | 0.20752 | 8.78227 | 41 |
| 2.04323 | -0.95605 | -1.90573 | -0.49408 | 0.24057 | 8.72063 | 10 |
| -1.41865 | -0.16020 | 1.01262 | -0.31252 | 0.34621 | 3.06362 | 3 |
| -1.40504 | -0.24481 | -1.00205 | -0.30976 | 0.34134 | 3.03818 | 20 |

# ## Example 6

Another problem for which computational difficulties have been recently reported by Shacham *et al.* [29] is the calculation of the dew point temperature for a 20% isobutanol and 80% water mixture. This is based on the problem in Henley and Rosen [8]. The problem consists of 16 algebraic equations that can be arranged into a structure of 13 simple equations and 3 difficult equations:

$$x_4 = 1 - x_1$$ \tag{1.136}

$$x_5 = 1 - x_2$$ \tag{1.137}

$$\log_{10}x_6 = 7.62231 - \frac{1417.90}{191.15 + x_3}$$ \tag{1.138}

$$\log_{10}x_7 = 8.10765 - \frac{1750.29}{235.00 + x_3}$$ \tag{1.139}

$$\log_{10}x_8 = \frac{1.7x_4^2}{(1.7x_1/0.7 + x_4)^2}$$ \tag{1.140}

$$\log_{10}x_9 = \frac{0.7x_1^2}{(x_1 + 0.7x_4/1.7)^2}$$ \tag{1.141}

$$\log_{10}x_{10} = \frac{1.7x_5^2}{(1.7x_2/0.7 + x_5)^2}$$ \tag{1.142}

$$\log_{10}x_{11} = \frac{0.7x_2^2}{(x_2 + 0.7x_5/1.7)^2}$$ \tag{1.143}

$$x_{12} = x_6x_8/760$$ \tag{1.144}

$$x_{13} = x_7x_9/760$$ \tag{1.145}