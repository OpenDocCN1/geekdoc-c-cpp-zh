# # Chapter 19: Introducing the Output Delivery System

+   - **19.1 Introduction........................................................................................... 325**
- **19.2 Sending SAS Output to an HTML File............................................................... 325**
- **19.3 Creating a Table of Contents...................................................................... 327**
- **19.4 Selecting a Different HTML Style................................................................ 328**
- **19.5 Choosing Other ODS Destinations.................................................................. 329**
- **19.6 Selecting or Excluding Portions of SAS Output............................................... 329**
- **19.7 Sending Output to a SAS Data Set............................................................... 333**
- **19.8 Problems...................................................................................................... 335**

# ## 19.1 Introduction

The Output Delivery System (abbreviated ODS) allows you to send SAS output to a variety of destinations, such as HTML, PDF, RTF, and SAS data sets.

Not only can you send your SAS output to all of these formats, you can, if you are brave enough, customize the output's fonts, colors, size, and layout. Finally, you can now capture virtually every piece of SAS output to a SAS data set for further processing.

# ## 19.2 Sending SAS Output to an HTML File

Beginning in SAS 9.3 the default ODS Destination for SAS output is HTML. If you don't need your output in a file, you don't need to submit any ODS statements unless you want to capture procedure output to a SAS data set.

As an example, suppose you want to send the output of PROC PRINT and PROC MEANS to an HTML file. It takes only two SAS statement to do this, as shown next: