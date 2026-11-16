# Methods within a Camp

We know that choosing between the orthogonal and oblique rotation camps can make a difference in the final results; but how important is the decision about the specific method after you have chosen your camp? Out of the orthogonal methods, varimax rotation is the most commonly used, and it is the default in many programs. One might conclude it is the orthogonal method of choice. Out of the oblique methods, promax rotation is recommended as the most desirable rotation method (Thompson, 2004). Let's test whether the recommended methods produce different results than their alternatives.

The SDQ contains three scales (parent relations, mathematics, and English) that are minimally correlated (r = 0.15, 0.22, 0.26). Since the theoretical factors are correlated, we should use an oblique rotation method. The two common oblique methods reviewed in this chapter are promax rotation and direct oblimin rotation. The syntax to run these two analyses is presented below. We use maximum likelihood extraction since the method seemed appropriate for this data. (See Chapter 2.)

```
proc factor data = sdgdata nfactors = 3 method = ml rotate = PROMAX;
VAR Math: Par: Eng:;
run;
proc factor data = sdgdata nfactors = 3 method = ml rotate = OBLIMIN;
VAR Math: Par: Eng:;
run;
```

Table 4.2 on page 73 and Table 4.1 on page 73 display the factor loadings for each of these rotation methods and Table 4.3 on page 74 displays the inter-factor correlations. Both oblique rotation methods yield similar results. As expected, the initial unrotated factor loadings for each method are identical. These should be identical because they represent the distribution of the unique variance of the factor loadings before the factors are rotated. These initial factor loadings would be very difficult to interpret as the loadings for a variable tend to be of moderate size across all of the factors. The rotated factor loadings, in both the pattern matrix and structure matrix, are nearly identical. These solutions are what we would expect given the theoretical model that the scale was developed with. The final rotated solutions give us a clear, theoretically consistent factor structure with subscale items aligning as expected.

In this example, the type of oblique rotation used did not make a difference. They resulted in the same clear factor structures and only minor differences in loadings. Many others (for example, Gorsuch, 1983; Kim & Mueller, 1978) have drawn similar conclusions. The methods within the orthogonal and oblique camps tend to produce similar results.