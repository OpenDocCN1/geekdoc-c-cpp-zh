# Chapter 12

# Option pricing with binomial approximations

# Contents

+   12.1 Introduction ........................ 112
+   12.2 Pricing of options in the Black Scholes setting .................... 113
+   12.2.1 European Options .................... 114
+   12.2.2 American Options .................... 114
+   12.2.3 Matlab implementation ............... 116
+   12.3 How good is the binomial approximation? ............ 119
+   12.3.1 Estimating partials. ................ 120
+   12.4 Adjusting for payouts for the underlying ............ 123
+   12.5 Pricing options on stocks paying dividends using a binomial approximation ............ 124
+   12.5.1 Checking for early exercise in the binomial model. ............ 124
+   12.5.2 Proportional dividends. ............. 124
+   12.5.3 Discrete dividends .................. 126
+   12.6 Option on futures ..................... 128
+   12.7 Foreign Currency options .............. 130
+   12.8 References ............................ 131

# 12.1 Introduction

We have shown binomial calculations given an up and down movement in chapter 8. However, binomial option pricing can also be viewed as an *approximation* to a continuous time distribution by judicious choice of the constants u and d. To do so one has to ask: Is it possible to find a parametrization (choice of u and d) of a binomial process