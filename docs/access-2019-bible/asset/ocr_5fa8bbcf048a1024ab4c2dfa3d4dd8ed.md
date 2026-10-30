# FIGURE 21.40

All report page settings must consider the margin widths.

![](bbox=[0.17, 0.21, 0.5, 0.56])

# Exploiting two-pass report processing

In Chapter 20, we mention that Access uses a two-pass approach when formatting and printing reports. We’ll now explore what this capability means to you and how you can exploit both passes in your applications.

The main advantage of two-pass reporting is that your reports can include expressions that rely on information available anywhere in the report. For example, placing a control with the Sum() function in a header or footer means that Access will use the first pass to accumulate the data required by the function, and then use the second pass to process the values in that section before printing them.

Another obvious example is putting an unbound text box in the footer of a report containing the following expression:

```
="Page " & [Page] & " of " & [Pages]
```

The built-in Pages variable (which contains the total number of pages in the report) isn’t determined until Access has completed the first pass through the report. On the second pass, Access has a valid number to use in place of the Pages variable.

The biggest advantage of two-pass reporting is that you’re free to use aggregate functions that depend on the report’s underlying record source. Group headers and footers can include information that can’t be known until the entire record source is processed.