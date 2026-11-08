# ### Explicitly by Name

In the DATA step variable names are used explicitly. While this same naming convention will *sometimes* work in the compute block, you need to understand when it will and will not work. The name is used explicitly when the variable or report item:

+   - has a define usage of GROUP, ORDER, COMPUTED, or DISPLAY
+   - is a temporary variable, which is created and used only in a compute block
+   - is the automatic temporary variable named `_BREAK_`
+   - is a report item alias (see below)

# ### Using a Compound Name

Compound variable names are needed when a report item has a define usage of ANALYSIS, which means that it has been used to calculate a statistic (SUM is the default). The compound name is a combination of the variable name and the statistic that it has been used to calculate.

```
```
compute wt;
   wt.mean = wt.mean/2.2;
endcomp;
```
```

The general form is *variablename.statistic*, and in the compute block you might address the mean of the variable WT as shown to the left.

# ### Directly When Using an Alias

Creating an alias of a report item allows you to use that report item in multiple ways. The following COLUMN statement generates a series of aliases for the HT analysis variable. Each of these aliases will be used to calculate a different statistic.

```
```
column region_ht
   ht=htmin  ht=hmax
   ht=htmean ht=htmedian;
```
```

```
```
compute after;
   line @3 'Minimum height is ' htmin 6.1;
endcomp;
```
```

When an alias is used in a compute block, it is named explicitly. Here the HTMIN alias of HT is used in a LINE statement.

# ### Indirectly When Using the Absolute Column Number

The define type of ACROSS creates a series of columns. These columns, and indeed any column in the report, can be referenced by using the column number as an indirect column reference.

This pseudo variable name is always of the form `_Cxx_`, where the xx is the column number as read from left to right on the report. The column count even includes any columns that will ultimately not be printed, e.g., those columns defined with NOPRINT or NOZERO.

When one or more report items have a define usage of ACROSS, it is not possible to address the transposed columns by name. To address these columns it is necessary to use absolute column numbers.

# ### MORE INFORMATION

Absolute column references are used in the example in Section 8.4.3.

# ## 8.4.3 Understanding Compute Block Execution

In the following example a compute block is used to convert the mean weight from pounds to kilograms. Since WT is nested under SEX, which has a define usage of ACROSS, there will be two columns associated with WT. As a consequence, absolute column numbers must be used in the compute block that performs the conversion ❸.