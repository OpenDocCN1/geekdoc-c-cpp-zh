# # 8

# # Software Engineering with SPARK

In the preceding chapters we have concentrated on the details of the SPARK language. In this chapter, we look at a broader picture of how SPARK might be used in the context of a software engineering process. The SPARK 2014 Toolset User's Guide (SPARK Team, 2014b) lists three common usage scenarios:

+   1. Conversion of existing software developed in SPARK 2005 to SPARK 2014
+   2. Analysis and/or conversion of legacy Ada software
+   3. Development of new SPARK 2014 code from scratch

We start by examining each of these scenarios in more detail, discussing the interplay between proof and testing, and then presenting a case study to illustrate some issues arising when developing new SPARK 2014 code from scratch.

# ## 8.1 Conversion of SPARK 2005

Converting a working SPARK 2005 program to SPARK 2014 makes sense when that program is still undergoing active maintenance for enhanced functionality. The larger language and the enhanced set of analysis tools provided by SPARK 2014 offer a potential savings in development time when adding functionality to an existing SPARK 2005 program.

As SPARK 2014 is a superset of SPARK 2005, the conversion is straight forward. Section 7.2 of the SPARK 2014 Toolset User's Guide (SPARK Team, 2014b) provides a short introduction to this conversion. Appendix A of the SPARK 2014 Reference Manual (SPARK Team, 2014a) has information and a wealth of examples for converting SPARK 2005 constructs to SPARK 2014. Explanations and examples are provided for converting subprograms, type (ADT) packages, variable (ASM) packages, external subsystems, proofs, and