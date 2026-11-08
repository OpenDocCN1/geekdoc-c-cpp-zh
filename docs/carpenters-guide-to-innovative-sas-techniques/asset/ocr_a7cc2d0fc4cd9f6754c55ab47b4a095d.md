+   - 12.7 Building Formats from Data Sets 390
+   - 12.8 Using the PVALUE Format 392
+   - 12.9 Format Libraries 393
+     - 12.9.1 Saving Formats Permanently 393
+     - 12.9.2 Searching for Formats 394
+     - 12.9.3 Concatenating Format Catalogs and Libraries 394

The use of formats is essential to the process of analysis and reporting of data. The user must be well grounded not only in the basic application of formats, but the deeper, less commonly known aspects as well. The power of formats can be taken advantage of in a wide variety of situations. It is incumbent on the user that these capabilities are fully understood.

# MORE INFORMATION

Section 3.5.1 discusses the difference between formats and informats and their uses in the conversion of character to numeric values.

# SEE ALSO

Carpenter (2003a) introduces a number of topics on the use of user-written formats. Ron Cody (2008a) provides a number of examples of user-written formats which demonstrate a number of the options and techniques described in this chapter. Bilenas (2005) is a book that is devoted to the topic of SAS formats.

# 12.1 Using Preloaded Formats to Modify Report Contents

Generally when a level of a classification variable is not included in the data, that level will not appear in any reports or analyses based on that data. Preloaded formats provide a mechanism to not only force the inclusion of those absent classification levels, they can also be used to filter or remove unwanted levels.

Preloaded formats can be used with the REPORT, TABULATE, MEANS and SUMMARY procedures. Preloaded formats are invoked through the use of options, and the available options and their usage varies for each procedure. For each procedure it is the interaction of these options that determines the resulting table. For the examples in this section study the results of the various combinations of the options, then experiment using other combinations.

For each of these procedures the two primary options used are PRELOADFMT and EXCLUSIVE:

+   - **PRELOADFMT** — Loads the format levels prior to execution. This option will always be present when using preloaded formats.
+   - **EXCLUSIVE** — Only data levels that are included in the format definition are to appear in table.