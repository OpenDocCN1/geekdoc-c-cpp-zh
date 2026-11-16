```
end;
else do;
  edit \alignedLoadings;
  append from sub_aligned_ldgs;
  close \alignedLoadings;
  edit \summary;
  append from sub_rev_summary;
  close \summary;
end;
end;
run;
%MEND;
```

In order to run the syntax, we just need to load the macro into SAS memory by running the syntax above. Then we run a line that calls the macro and enters the appropriate arguments into it. The macro call that is used for the engineering factor loadings is provided below. The first argument in the parentheses specifies the data set containing the factor loadings from our original run with the full sample (orig_loadings). The second specifies the data set containing the factor loadings for each of the resamples (boot_loadings). The third identifies the name of the data set that will be output from the macro that will contain the aligned loadings that can then be entered into PROC UNIVARIATE (aligned_loadings). Finally, the fourth identifies the name of a data set that will contain a summary of the alignment procedure. This argument also contains the final ordering, any reflection that was done, and the sum of squared differences for the order that best matched the original factor solution (rev_summary). This macro will perform this step for any EFA factor loadings, regardless of the number of factors or items.

```
\alignFactors(orig_loadings, boot_loadings, aligned_loadings, rev_summary);
```

# Application

# What Does Bootstrapping Look Like?

Now that we are familiar with the syntax, let us review an example of the use and application of bootstrap resampling. Remember that EFA is a complex procedure with lots of effects. It can have many communalities, eigenvalues, and factor loadings. So although it does not take a terribly long time with modern computers (it took our computer about 2 minutes to run 2000 bootstrap analyses and save them to a data file), the process that takes the longest is examining all the different parameters one wants to examine.

The analyses in Chapter 3 indicated that the engineering data had two small, clear factors. The sample was relatively small, however, so we could wonder whether it is likely that the two-factor model will replicate. With such a small sample, we would be hesitant to split it and