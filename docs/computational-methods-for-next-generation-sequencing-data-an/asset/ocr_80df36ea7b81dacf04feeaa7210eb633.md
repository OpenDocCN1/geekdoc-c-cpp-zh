# DISCOVERING AND GENOTYPING TWILIGHT ZONE DELETIONS

TABLE 7.3 Results for SV Prediction Tools on 30x HiSeq/MeSeq Data for Deletions from 70 to 199 bp

| Deletion length | Tool | Precision (strict) | Precision (released) | Recall (homol.) | Recall (het.) |
|---|---|---|---|---|--|
| 70–99 | BreakDancer | 5.8/19 | 85.2/25.8 | 59.6/12.3 | 50.7/0.6 |
| | CLEVER | 38.0/23.4 | 88.8/79.1 | 81.3/77.9 | 60.2/16.9 |
| | VariationHunter | 15.7/12.0 | 83.1/67.4 | 83.0/77.0 | 79.1/11.5 |
| | PINDEL | 56.1/72.1 | 64.6/80.9 | 38.3/65.5 | 48.6/14.7 |
| | SOCRATES | 49.1/55.8 | 54.7/60.5 | 7.2/8.5 | 10.9/8.9 |
| | DELLY | 66.- | 66.- | 0.4/2.1 | 0.0 |
| | MATE-COWER | 80.9/89.6 | 90.1/94.6 | 57.4/63.4 | 41.5/42.1 |
| | Bowtie | - | - | 0.9/3.0 | 0.0/9.0 |
| | MEM | -81.4 | -86.4 | - | 2.6/22.3 |
| | GSNAP | - | - | 13.2/72.3 | - |
| | Tammy | 87.5/34.9 | 100.0/67.4 | 20.0/54.0 | 12.3/2.0 |
| 100–149 | BreakDancer | 3.1/0.2 | 78.2/21.8 | 48.7/19.3 | 48.6/0.4 |
| | CLEVER | 31.4/21.6 | 83.6/70.8 | 69.0/64.0 | - |
| | VariationHunter | 5.2/5.5 | 65.3/60.3 | 76.6/72.6 | 66.9/8.0 |
| | PINDEL | 61.1/77.6 | 65.5/85.3 | 20.9/34.1 | 11.2/18.4 |
| | SOCRATES | 36.0/41.9 | 44.0/48.4 | 5.6/5.6 | 5.6/4.8 |
| | DELLY | 40.7/50.0 | 69.5/80.4 | 6.1/6.1 | 8.0/5.2 |
| | MATE-COWER | 75.5/77.9 | 85.4/87.5 | 44.2/47.7 | 30.3/32.3 |
| | Bowtie | - | - | 0.0/1.8 | 0.0/8.0 |
| | BWA MEM | -100.0 | -100.0 | 1.5/2.7 | 2.8/0.0 |
| | GSNAP | - | - | 8.6/5.1 | 5.6/0.0 |
| | Tammy | - | - | 6.2/20.8 | 5.6/0.0 |
| 150–199 | BreakDancer | 1.9/0.3 | 41.5/18.3 | 40.7/19.8 | 30.9/0.7 |
| | CLEVER | 32.0/16.3 | 86.4/67.0 | 61.5/63.7 | 36.2/13.8 |
| | VariationHunter | 4.3/3.8 | 35.8/31.4 | 70.3/67.0 | 63.8/8.6 |
| | PINDEL | 55.4/69.0 | 58.5/81.0 | 20.9/34.1 | 2.0/2.6 |
| | SOCRATES | 20.0/31.0 | 22.9/34.5 | 6.6/7.7 | 7.2/9.9 |
| | DELLY | 25.0/56.4 | 45.0/74.4 | 9.9/12.1 | - |
| | MATE-COWER | 74.7/83.5 | 86.1/91.3 | 37.4/46.2 | 19.7/30.9 |
| | Bowtie | - | - | 0.0/0.0 | 0.0/0.0 |
| | BWA MEM | - | - | 0.0/0.0 | 0.0/0.0 |
| | GSNAP | - | - | 0.0/0.0 | 0.0/0.0 |
| | Tammy | - | - | 0.0/0.0 | 0.0/0.0 |

size-based approaches in terms of accuracy of breakpoint annotation, as indicated by the much improved precision rates. It is also obvious that in the lower part of the twilight zone (see Table 7.2), split-read alignment approaches have certain advantages, where we note that alignment-based approaches PINDEL excels in terms of precision, while GSNAP excels in recall of HiSeq data. BWA-MEM has clear advantages. Approaches from the classes that have high recall in the lower are CLEVER and MATE-COWER, certainly because they are the only approaches tailored toward discovery of twilight zone deletions.