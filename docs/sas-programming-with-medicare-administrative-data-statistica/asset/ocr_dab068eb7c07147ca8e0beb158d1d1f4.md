# 52 SAS Programming with Medicare Administrative Data

+   * Our instructional plan is to request data from CMS’s data distribution contractor and quickly convert the data we receive into separate files for each claim type that contain all of the information for a claim in one record.

+   * CMS offers a variety of datasets for research purposes which we grouped into three categories: Research Identifiable Files (RIFs), Limited Data Sets (LDS), and Public Use Files (PUFs). Consult with ResDAC to ensure you are requesting the right kind of data for your research.

+   * Our data utilized a file provider by CMS to query the following claims and enrollment data for calendar year 2010: Part B claims, DME claims, inpatient patients, outpatient claims, SNF claims, home health claims, and MBSF enrollment data.

+   * We discussed a high-level overview of the data acquisition process.

+   * The package of data received from CMS’s data distribution contractor contained our requested data (in encrypted files), the SAS code for loading the files into SAS datasets, summary information detailing the data transmission, and a host of documentation and data dictionaries.

+   * We decrypted our data and loaded the files into SAS datasets. Then, we combined the administrative claims, separated into files by claim type, header and line information, and retained access to the finder file (also called our attribution file) for use in subsequent chapters.

> As stated in Chapter 3, all discussions of acquisition of source data are for instructional purposes. The data we use in this book are fake, and subject to the disclaimer presented in Chapter 1. In other words, although we pretend to go through the process of requesting data from CMS, we are simply describing how the process would occur and did not actually produce the data in this book through that process.

> See, for example, ResDAC’s Data for Student Research webpage, available at http://www.resdac.org/data-request-student-research.

> The list of data is not exhaustive, and new sources of data do become available.

> For instructional purposes, as part of our work we will transpose some of the files we create in this chapter to create a file containing one record per line.

> All this said, it is important to note that there are advantages to maintaining separate header and line data sets, and using PROC SQL to join the data sets when. In your work, and consistent with our discussion planning, you should consider the most efficient way to arrange your data and use your SAS code.

> The reader may wish to request a prior or subsequent year of data to study measures like hospital readmissions, or to make comparisons to prior years of performance outcomes (i.e., compare provider’s performance in 2010 to performance in 2009). For our simple example, this will not be necessary.

> See www.resdac.org and www.ccwdata.org, respectively.

> For a funded study, the method section should be included rather than writing a new protocol for the packet sample.

> The institutional files can also include reference code files for things like condition and span codes. We will not use these files, so we will not discuss them.

> Although it is important to be aware that inpatient patients can spill over into more than one claim record, it is not however often, so we will not write code to handle this situation.

> Our code and explanation draws on a helpful SAS Learning Module provided by UCLA’s Institute for Digital Research and Education, available at http://www.ats.ucla.edu/stat/sas/modules/longtowide_data.htm.