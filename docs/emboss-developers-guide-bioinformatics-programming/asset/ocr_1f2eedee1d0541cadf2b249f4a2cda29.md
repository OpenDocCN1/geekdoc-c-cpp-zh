| | Command line parameters | |
|---|---|---|
| DI directory | Output subdirectory | Mandatory where output sub-directories are used |
| DF FileName | Name of file in output sub-directory | Optional |
| DL directive | Directive for results directory on test completion | Optional |
| ER ErrorCode | Error return code | Optional |
| FI FileName | Name of output file in results directory | Mandatory for all files created in the main results directory |
| FC [<=] NumberLines | Test number of lines in the preceding FI file | Mandatory for all files other than stdout and stderr if an FZ record is not defined, otherwise optional |
| FP count / regexp / | Test for pattern in the preceding FI file | Mandatory for all files other than stdout and stderr |
| FZ [<=] FileSize | Test size of the preceding FI file | Mandatory for all files other than stdout and stderr if an FC record is not defined, otherwise optional. |
| IC text | Annotation on the input | Optional |
| IN UserInput | Value to use in response to an EMBOSS prompt | Mandatory for each application option that will be prompted for by the application |
| OC text | Annotation on the output | Optional |
| PP command | Pre-processor command | Optional |
| QQ command | Post-processor command | Optional |
| RQ RequiredApps | Required external programs | Mandatory for applications that require other applications to run, e.g. application wrappers |
| TI seconds | Time limit for test | Optional |
| UC text | Annotation on the usage examples | Optional |
| ## | Comment | Optional |

# 7.2.1.1 ID ApplicationName-Tag

The identifier has the general form ApplicationName-Tag where ApplicationName is the name of the application being tested and Tag indicate what sort of test is being performed.

When a test is run, a directory is created under /emboss/test/ to hold the output of the test run. This includes all the application output files and files with any output written by the application to the UNIX file streams stdout and stderr. The identifier defines the name