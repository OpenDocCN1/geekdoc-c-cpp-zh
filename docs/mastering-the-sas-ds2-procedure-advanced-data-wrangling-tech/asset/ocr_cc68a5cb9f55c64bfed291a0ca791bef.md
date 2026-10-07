+   * arrays
* iterative processing (DO loops)
* macro processing:
  * assigning values to macro variables
  * resolving macro variables in SAS code
  * timing of macro process execution versus execution of other SAS code
* SQL joins

# # Scope of This Book

This book covers the following topics:

+   * the types of processes for which the language was designed and the conditions indicating when DS2 would be a good choice for improving process performance
* programming statements and functions shared between traditional DATA steps and DS2 programs
* DATA step functionality that is not available in DS2
* new DS2 functionality that is not available in the traditional DATA step
* manipulating ANSI data types at full precision in DS2
* converting traditional Base SAS steps to DS2 data programs
* creating reusable code modules in DS2 and packaging them for easy reuse
* using DS2 packages to create object-oriented programs
* creating DS2 thread programs for parallel processing of data records
* executing DS2 thread programs distributed on MPP DBMS platforms

# # About the Examples

# ## Software Used to Develop the Book's Content

SAS 9.4M3

The majority of the programs in this book use only Base SAS and were developed with SAS University Edition.

+   * The programs that read and write to DBMS also required these solutions:
  * SAS/ACCESS Interface to Teradata.
  * SAS In-Database Code Accelerator for Teradata.

All DBMS data was stored in Teradata Express 15.0.