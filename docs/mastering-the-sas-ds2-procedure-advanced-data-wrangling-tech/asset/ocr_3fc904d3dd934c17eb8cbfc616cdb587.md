# Mastering the SAS DS2 Procedure: Advanced Data Wrangling Techniques

Figure 1.3: Parallel Processing with Threads: SAS Compute Platform versus In-Database

# DS2 threads parallel processing
on the SAS compute platform

# DS2 threads parallel
processing in-database

![](bbox=[0.101, 0.142, 0.836, 0.513])

As you can see in Figure 1.3, using DS2 thread and data programs with the SAS In-Database Code Accelerator allows the DS2 code to compile and execute on the massively parallel DBMS hardware. If the process reads from a DBMS table and also writes to a DBMS table, then only the code goes into the DBMS, and only the SAS log comes out. Processing takes place in the DBMS. This concept of "taking the code to the data instead of the traditional "bringing the data to the code" greatly reduces the amount of data movement for processing, extends the computational capabilities of the DBMS to include SAS functions and processing logic, and takes full advantage of the massively parallel processing (MPP) capabilities of the DBMS. If you are a SAS programmer or a data scientist in an environment that includes SAS, you will find that DS2 quickly becomes a go-tool for data manipulation.

# 1.1.1 What to Expect from This Book

Data wrangling, as use the term, is more than cleaning up data to prepare it for analysis. A data wrangler acquires data from diverse sources, and then organizes, combines it in unique ways to facilitate analysis and obtain new insights. This book teaches you to strangle data using DS2, highlighting the similarities and differences between DS2 data programs and traditional DATA step processing as well as using DS2’sparallel-processing power to boost your data-wrangling speed.