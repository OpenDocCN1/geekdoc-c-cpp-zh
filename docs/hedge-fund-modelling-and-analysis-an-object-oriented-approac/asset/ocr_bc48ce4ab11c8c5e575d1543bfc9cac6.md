```
tmp += pow((v[i] - mean / std, 4);
}

tmp *= (double)n* (n+1) / ((n-1) * (n-2) * (n-3));
tmp = 3 * pow((double)(n-1), 2) / ((n-2) * (n-3));
tmp /= (double)f; // Cast frequency (f) to portfolio
skskurt = tmp;

return xskurt;
}
//
```

Figure 7.5 shows a histogram indicating the monthly MVaR figure which is clearly higher when compared to the parametric VaR95 of $1 556 215 for the CTA Index.

# 7.5 EXPECTED SHORTFALL

Apart from the assumption that the P&L distribution is normal, VaR also fails to satisfy one of the concepts of a coherent risk measure. Artzner et al. (1999) have stated that a desirable measure of risk should satisfy four properties or axioms of risk, namely:

+   1. Must be monotonic i.e. if asset X ≥ 0, VaR(X) ≤ 0 i.e. positive returns should not increase risk.
2. Must be sub-additive i.e. for assets X1 and X2, VaR(X1 + X2) ≤ VaR(X1) + VaR(X2) i.e the risk of a portfolio of two assets should not be larger than the risk of the sum of the individual assets. If this were the case, adding assets to a portfolio to reduce risk through diversification would not be possible.
3. Must possess positive homogeneity so for any positive number, a, VaR(aX) = aVaR(X) i.e increasing the size of the portfolio by a times should increase the risk by a multiple of a assuming all assets in the portfolio remain the same in terms of weighting.
4. Must be translational invariant that for any real number, a, VaR(X+a) ≤ VaR(X)- a i.e. adding amount of cash (or risk-free asset) to the portfolio should result in a reduction of the risk by any amount a.

Unfortunately, VaR only satisfies three of the axioms of risk i. it fails to satisfy the sub-additive rule. For this reason, an alternative (and often complementary) measure of VaR was developed known as expected shortfall (ES)¹ which is discussed in