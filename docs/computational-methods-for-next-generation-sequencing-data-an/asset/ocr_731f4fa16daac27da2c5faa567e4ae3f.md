# TABLE 7.5 Genotyping Performance for Heterozygous Clogs

| Deletion length | Tool | True Annot. -> # of Calls | Absent Wrong call | Heterozyg. Correct | Homozog. Wrong type |
|---|---|---|---|---||
| 10-29 | BWA/UG | 6,188/10,856 | 8.4/10.8 | 85.5/84.9 | -5/1 |
| | BWA/HC | 10,182/12,464 | 11.6/10.7 | 80.5/80.6 | 10.1/111.3 |
| | GSNAP/UG | 7,747/9,848 | 7.9/7.7 | - | 7.5/7.1 |
| | GSNAP/HC | 10,619/12,506 | 11.6/11.3 | 80.3/80.0 | 10.4/11.2 |
| | MATE-CLEVER | 1,022/333 | 7.0/3.0 | 61.7/86.2 | 37.1/12.9 |
| 30-49 | BWA/UG | 119/971 | 7.6/9.6 | 87.4/86.2 | 9.2/6.5 |
| | BWA/HC | 961/1,456 | 10.9/12.4 | 72.3/87.4 | 11.1/15.0 |
| | GSNAP/UG | 728/1,024 | 22.9/12.3 | 81.2/83.4 | - |
| | GSNAP/HC | 1,122/1,454 | 22.1/11.2 | 69.5/77.8 | 11.1/14.9 |
| | MATE-CLEVER | 877/597 | 10.6/5.9 | 80.8/81.0 | 10.9/5.4 |
| 50-69 | BWA/UG | 0/177 | - | -79.7 | -5/1 |
| | BWA/HC | 262/438 | 32.8/14.4 | 53.4/69.4 | 15.6/18.9 |
| | GSNAP/UG | 43 | 32.6/15.9 | 67.4/77.8 | 0.0/6.3 |
| | GSNAP/HC | 315/410 | 32.1/18.3 | 54.6/66.6 | 15.6/18.5 |
| | MATE-CLEVER | 313/233 | 17.6/6.0 | 75.4/91.4 | 7.3/3.9 |
| 70-99 | BWA/UG | 0/331 | - | -16.1 | -/6.5 |
| | BWA/HC | 148/390 | 38.5/16.3 | 52.0/68.9 | 13.5/20.5 |
| | GSNAP/UG | 0/0 | - | - | -/0 |
| | GSNAP/HC | 182/222 | 39.0/20.7 | 51.1/65.3 | 12.1/18.5 |
| | MATE-CLEVER | 169/163 | 8.3/4.9 | 85.2/92.0 | 8.3/4.3 |
| 100-149 | BWA/UG | 0/0 | - | - | -/0 |
| | BWA/HC | 78/90 | 56.4/15.6 | 25.6/56.7 | 19.2/35.6 |
| | GSNAP/UG | 0/0 | - | - | -/0 |
| | GSNAP/HC | 100/117 | 59.0/17.1 | 31.0/59.8 | 11.0/28.2 |
| | MATE-CLEVER | 92/101 | 14.1/12.9 | 80.4/86.1 | 5.4/2.0 |
| 150-199 | BWA/UG | 0/0 | - | - | -/0 |
| | BWA/HC | 18/29 | 88.9/31.0 | 5.6/51.7 | 11.1/20.7 |
| | GSNAP/UG | 0/0 | - | - | -/0 |
| | GSNAP/HC | 26/20 | 92.3/25.0 | 7.7/50.0 | 3.8/30.0 |
| | MATE-CLEVER | 40/52 | 20.0/9.6 | 75.0/86.5 | 5.0/3.8 |

genotype twilight deletions, which we re-visit here in detail. In addition to those novel strategies, well-maintained SV calls have constantly undergone improvements. They, have grown into methods by which one can make least a good amount of calls in partial areas of the twilight (7, 8, 14, 30). Many of these collects are collectively, combining MATE-CLEVER with a reasonable selection of other tools, we favor PINDEL, and on MiSeq BWA-MEM in particular, should lead to successful twilight deletion calling pipelines. In essence, we consider the discovery of twilight deletions a resolved issue, at least when operating on carefully prepared sequencing libraries with reasonably standard deviations.

Here, we sketch the novel, successful strategies and evaluate a large rate of tools, some of which have helped considerably shedding light on the