# Chapter 7: Performance Tuning in DS2 125

+   - Site number, operating system, and software release. You can obtain this information from the top of a fresh SAS log, or you can execute this macro to print the information that you need in the SAS log:

```
%macro siteinfo;
%PUT NOTE: Site ID is &SYSITE;
%PUT NOTE- SAS Version is &SYSLONG;
%PUT NOTE- Operating System is &SYSSCP (&SYSSCPL);
%end;

%siteinfo
```

+   - SAS product involved (Base SAS is the product for DS2 questions).
- Succinct, one-line description of the issue for the subject line of your technical support track.
- Detailed problem description, including error or warning messages.
- A clear, concise description of any troubleshooting or research that you've already done.
- Copies of your SAS program, SAS log, and any other pertinent files. If at possible, supply some mock-up input data for your program to add the Technical Support folks in troubleshooting your problem. You can use the data2dataset macro discussed in Section 7.4.2 to provide the data. To include attachments, wait for the first automatic email response to arrive after you post your problem, and then reply to that email with the requisite attachments.

# 7.5 Review of Key Concepts

+   - The SAS system option FULLSTIM can provide significantly more detailed performance information in the SAS log than is usually available.
- The DS2_OPTIONS statement with the TRACE option can provide extra insight into how-database processing is accomplished by DS2 programs running in database.
- For benchmarking, it is necessary to code several approaches to the same problem, run them on realistically sized and located data, and compare performance statistics in order to best tune your DS2 programs.
- There is a lot of help available online for SAS users, including free e-learning courses, how-videos, SAS community forums, and SAS Technical Support
- Proper preparation before contacting SAS Technical Support will make the engagement smoother and result in faster answers to your questions.