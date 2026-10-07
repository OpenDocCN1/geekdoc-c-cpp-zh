(continued)

# TABLE 8.3 ODS HTML Output Using JOURNAL Style

ODS HTML Example Using Journal Style

The MEANS Procedure

| Variable | Label | N | Mean | Std Dev | Minimum | Maximum |
| --- | --- | --- | --- | --- | --- | --- |
| AGE | Age on Jan 1, 2000 | 50 | 10.46 | 2.43 | 4.00 | 15.00 |
| TIME1 | Baseline | 50 | 21.27 | 1.72 | 17.00 | 24.00 |
| TIME2 | 6 Months | 50 | 27.44 | 2.66 | 21.30 | 32.30 |
| TIME3 | 12 Months | 50 | 30.49 | 3.03 | 22.70 | 35.90 |
| TIME4 | 24 Months | 50 | 30.84 | 3.53 | 21.20 | 36.10 |

# TABLE 8.4 Output in PDF Format with the Statistical Style

ODS PDF Example

The MEANS Procedure

| Variable | Label | N | Mean | Std Dev | Minimum | Maximum |
| --- | --- | --- | --- | --- | --- | --- |
| AGE | Age on Jan 1, 2000 | 50 | 10.46 | 2.43 | 4.00 | 15.00 |
| TIME1 | Baseline | 50 | 21.27 | 1.72 | 17.00 | 24.00 |
| TIME2 | 6 Months | 50 | 27.44 | 2.66 | 21.30 | 32.30 |
| TIME3 | 12 Months | 50 | 30.49 | 3.03 | 22.70 | 35.90 |
| TIME4 | 24 Months | 50 | 30.84 | 3.53 | 21.20 | 36.10 |

Change the ODS HTML CLOSE statement to

ODS PDF CLOSE;

(See ODS.SAS.) The results will appear in the Results Viewer. Depending on your particular setup, the Adobe Reader program may start up and display the ODS.PDF file. The results are given in Table 8.4. This output is created in the STATISTICAL style format as specified in the ODS statement FILE=. Similar results can be observed by outputting information in other ODS formats.

# 8.3 USING ODS TO SELECT SPECIFIC OUTPUT TABLES FOR SAS PROCEDURES

SAS procedures often output a lot of information you don't want or need. In ODS output, each part of the output is contained in a table. Using ODS options, you can customize