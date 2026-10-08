
This assigns the address of variable var a; by preceding the name of the variable with the address-of-operator (&), we are no longer assigning the content of the variable itself to a, but its address. A variable that stores the address of another variable is called a pointer. Pointers are said to 'point to' the variable address they store. An interesting property of pointers is that they can be used to access the variable they point to. This is done by preceding the pointer name with the dereference operator (*). The operator itself can be read as 'value pointed to'. Unfortunately, a full discussion of pointers is beyond the scope of this book so we have only briefly introduced them for completeness.

The results for the IR show that the rankings have changed somewhat now that we have introduced a reference market benchmark. CTA1 is the highest ranked and MN2 still the lowest ranked, CTA3 is in second place with GM1 in third. In other words, some funds are starting to look better than before in the presence of a benchmark and we are starting to drop the rankings.

## 5.5.2 The Treynor Ratio

The Treynor ratio (TR) introduced by Treynor (1962) is again of the same form as the generalised risk-adjusted return given by (5.3). However, this time risk is defined as the beta of the fund relative to a benchmark, such that:

$$TR = \frac{\alpha_p}{\beta_p} \frac{R_p - R_F}{\beta_p}$$ (5.14)

The beta of the portfolio $\beta_p$ can be calculated in two ways. The first method has already been discussed in Chapter 4. Box 5.2 shows a detailed explanation of an alternative method of estimating beta.

> BOX 5.2: ESTIMATING BETA AND ITS RELATIONSHIP TO CORRELATION

Beta is a very common measure for estimating the extent to which the hedge fund excess returns are influenced by that of the benchmark or market excess returns. The beta of the portfolio is the gradient (m) of the OLS regression line where the market excess returns are plotted on the x-axis and the hedge fund excess returns on the y-axis (see Chapter 4). The fund’s beta can be visualised as a measure of its relative directional exposure to the benchmark i.e. a kind of relative elasticity as shown in Figure 5.12.

![](img/2d1ac831a270b8b08f8b8ec2205913dc_208_0.png)

### FIGURE 5.12 Relative directional exposure to a benchmark

When the hedge fund's beta is greater than 1.0, it has a tendency to exhibit greater moves in its returns (both positive and negative) than those of the benchmark. When the fund's beta is equal to 1.0, the fund is market held long (if the market gains 1%, the fund gains 1% and for all intents purposes the fund is exactly matched to the market i.e it is the market). When the fund's beta is between zero and 1.0, the fund's returns are less than those of the market (this is the region of beta usually occupied by long-short funds). If the fund's beta is zero, it has no impact on the returns of the fund. If the fund's beta is between zero and -1.0, the fund is in a less volatile fashion. If the fund's beta is -1.0, the fund is the benchmark held short and as the fund models the benchmark exactly but in the opposite way (if the benchmark market gains 1%, the fund loses 1% and vice versa).

Depending on your objectives, you may have different groups of betas to analyse. For example, if you are analysing a group of market neutral managers versus a market benchmark you may well have a statistical distribution of betas around zero. However, if you are a fund of managers analysing the betas of various hedge funds within a diversified fund funds portfolio, you will have a group of betas distributed around one. Either way, the beta is the sensitivity of the fund or asset relative to some systematic factor such as the market or collective index as seen in Merton (1990) in the following:

$$\beta_i = \frac{\sigma_{iM}}{\sigma_M^2}$$ (5.15)

$$\alpha_i = \beta_i(R_M - R_F)$$ (5.16)

Beta is however directly proportional to leverage which opens up a new set of problems for risk-adjusted return analysis when beta using any equation with beta in it will be leverage dependent – a case which is usually undesirable if the manager is to be measured for his skill and not. The beta, however, can be re-scaled to create an unleveraged cash equivalent correlation coefficient:

$$\rho_i = \frac{\sigma_M}{\sigma_p} \beta_i$$

So, in the world of hedge funds we see the emergence of the correlation coefficient as representing the sensitivity of a fund to a certain factor which has been risk-adjusted. The correlation value if multiplied by 100 will then show the percentage of the dependent variable accounted for by the source of returns or premium for the factor in question e.g. the systematic returns associated with the market portfolio if the CAPM is used. The correlation squared or r-squared when multiplied by 100 measures the proportion of variance captured in the dependent variable by the factor returns.

Source 5.6 shows the TR member declaration and definition.

### SOURCE 5.6: THE TR MEMBER DECLARATION AND DEFINITION

```cpp
// ...
// PMetrics.h
// ...

void TR(vector<double>& v, double r);
void GetSlope(vector<double>& v);
protected:
    Utils utils;
    LinReg linreg;
};
```

```cpp
// ...
// PMetrics.cpp
// ...

vector<double> TR(vector<double>& v, double r) {
    int n = v.size();
    vector<double> tr;
    for (int j = 0; j < n - 1; j++) {
        double tmp = 0;
        for (int i = 0; i < n; i++) {
            tmp = (mean[i] - r) / slope[i];
        }
        tr.push_back(tmp);
    }
    return tr;
}

vector<double> GetSlope(vector<double>& v) {
    vector<double> tmpv;
    for (int j = 0; j < v.size(); j++) {
        tmpv.resize(3);
        for (int i = 0; i < v.size(); i++) {
            if (j == 0) {
                // ...
            } else {
                // ...
            }
        }
    }
    // ...
}
```

```cpp
// main.cpp
// ...
int main() {
    // ...
    vector<double> tr = TR(data, 0.03);
    cout << "\n Treynor Ratio (Rf = 0.03):\n";
    Sort(tr, s);
    // ...
}
```

![](img/2d1ac831a270b8b08f8b8ec2205913dc_212_0.png)
