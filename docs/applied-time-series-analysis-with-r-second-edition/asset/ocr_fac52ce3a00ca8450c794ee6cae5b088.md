Using R: One way to obtain the data Y_t = (1 − B)(1 − B^{12}) (called here airlog13) is to use two calls to the function artrans.wge. Specifically, you could use

```
airlog12 = artrans.wge(airlog,phi.
    tr = c(0,0,0,0,0,0,0,0,0,0,0,1))
```

and then issue the command

```
airlog13 = artrans.wge(airlog12,phi.tr = 1).
```

# EXAMPLE 8.10: MODELING THE PENNSYLVANIA MONTHLY TEMPERATURE DATA

In Figure 8.10a, we show the average monthly temperatures (°F) for the state of Pennsylvania from January 1990 to December 2004 (patemp in tswge). These data were previously plotted in Figure 1.1b. In Figure 8.10b, we show the sample autocorrelations.

Since these data are monthly and (as expected) show a distinct seasonal pattern, we consider a model of the form

(1 − B^{12})φ(B)(X_t − μ) = θ(B)a_t.

As with the other potential seasonal data sets, we examine factor tables associated with high-order AR fits to the data (with p > 12). Table 8.6 shows a factor table associated with an AR(16) fit to these data. The features of this table are similar to factor tables for other values of p.