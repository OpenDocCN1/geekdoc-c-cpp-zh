# Chapter 7 Likelihood Models for Overdispersed Multinomial Responses 241

Kappa coefficient (κ), which compares the degree of observed agreement to the agreement one would expect purely out of chance, is defined as

```
$$\kappa = \frac{\pi_0 - \pi_c}{1 - \pi_c}$ (7.39)$
```

If the raters are in complete agreement, κ = 1. If observed agreement is greater than or equal to chance agreement, then κ ≥ 0. If observed agreement is less than chance agreement, then κ < 0. A negative Kappa is unusual in practice. The minimum value of Kappa depends on the marginal proportions.

To illustrate the use of the Kappa coefficient, consider the data in Table 7.7 where Agresti and Winner (1997) evaluated the agreement and disagreement between the well-known movie critics Gene Sikel and Robert Ebert from April 1995 through September 1996; over 160 movies were reviewed by both.

# Table 7.7: Sikel's and Ebert's Opinions on 160 Movies

| Sikel's Rating | Ebert's Rating | | |
| | Con | Mixed | Pro |
| Con | 24 | 8 | 13 |
| Mixed | 8 | 13 | 11 |
| Pro | 10 | 9 | 64 |

The coefficient of agreement Kappa can be calculated using the FREQ procedure. The programming statements are shown in Program 7.6.

# Program 7.6: Computation of Kappa Coefficient on Sikel's and Ebert's Movie Ratings

```
/*
Sikel and Ebert Ratings on 160 Movies
Agresti and Winner (1997)
*/
data movie_ratings;
  input x1-x3;
  n;
  Ebert = 1; w=x1; output;
  Ebert = 2; w=x2; output;
  Ebert = 3; w=x3; output;
  keep Sikel Ebert w;
datalines:
  24 13
  8 13 11
  10 9 64

proc format;
  value abc 1 = 'Con'
  2 = 'Mixed';
```

More