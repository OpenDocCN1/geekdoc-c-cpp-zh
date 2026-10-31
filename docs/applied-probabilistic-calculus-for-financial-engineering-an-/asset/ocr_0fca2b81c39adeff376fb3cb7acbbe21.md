![](bbox=[0.22, 0.11, 0.78, 0.47])

Figure 4.4 Graphical Output for plot (x, y).

# Remark:

For reference, Appendix 1 contains the CRAN documentation of the R function plot(), available for graphic outputting, which may be found by the R code segment:

```
> ?plot
```

CRAN has documentations for many R functions and packages.

Again, returning to the R workspace, and enter

```
> 
> 
> is() # (This is a lower-case "l" followed by "s", viz., the 'list' # command.)
> # (NOT l = "ONE" followed by "s")
> # This command will list all the R objects now in the
> # R workspace:
> # Outputting:
[1] "E" "n" "ls" "x" "y" "z"
```

Again, returning to the R workspace, and enter

```
> rm (x, y) # Removing all x and all y from the R workspace
> x        # Calling for x
```