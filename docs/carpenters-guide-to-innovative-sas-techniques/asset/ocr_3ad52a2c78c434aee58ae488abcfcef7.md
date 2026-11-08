2.5.2 Creating a Sparse Table
Using a Double Transpose
First Transpose

| Obs | SUBJECT | _NAME_ | Visit1 | Visit2 | Visit3 | Visit4 | Visit5 | Visit6 | Visit7 | Visit8 |
|---:|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|
| 31 | 210 | sodium | 14 | 14.2 | 14.1 | 14.4 | 14.5 | 14.3 | 14.1 | |
| 32 | 210 | potassium | 5 | 4.0 | 3.9 | 4.7 | 4.7 | 4.7 | 4.4 | |
| 33 | 210 | chloride | 103 | 103.0 | 101.0 | 105.0 | 104.0 | 103.0 | 102.0 | |

| Obs | Visit9 | Visit10 | Visit11 | Visit12 | Visit13 | Visit14 | Visit15 | Visit16 |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 31 | . | 14.2 | 14.2 | 13.9 | 14.2 | 14.1 | 13.8 | 14.3 |
| 32 | . | 4.3 | 4.1 | 4.0 | 4.4 | 4.1 | 3.8 | 5.2 |
| 33 | . | 106.0 | 104.0 | 103.0 | 104.0 | 99.0 | 99.0 | 104.0 |

The second PROC TRANSPOSE ➋ uses this data as input and since all visits are included on the VAR statement ➌, each visit becomes a row in the new table.

2.5.2 Creating a Sparse Table
Using a Double Transpose
Second Transpose

| Obs | SUBJECT | Visit | sodium | potassium | chloride |
|---:|---:|---|---:|---:|---:|
| 151 | 210 | Visit1 | 14.0 | 5.0 | 103 |
| 152 | 210 | Visit2 | 14.2 | 4.0 | 103 |
| 153 | 210 | Visit4 | 14.1 | 3.9 | 101 |
| 154 | 210 | Visit5 | 14.4 | 4.7 | 105 |
| 155 | 210 | Visit6 | 14.5 | 4.7 | 104 |
| 156 | 210 | Visit7 | 14.3 | 4.7 | 103 |
| 157 | 210 | Visit8 | 14.1 | 4.4 | 102 |
| 158 | 210 | Visit9 | . | . | . |
| 159 | 210 | Visit10 | 14.2 | 4.3 | 106 |
| 160 | 210 | Visit11 | 14.2 | 4.1 | 104 |
| 161 | 210 | Visit12 | 13.9 | 4.0 | 103 |
| 162 | 210 | Visit13 | 14.2 | 4.4 | 104 |
| 163 | 210 | Visit14 | 14.1 | 4.1 | 99 |
| 164 | 210 | Visit15 | 13.8 | 3.8 | 99 |
| 165 | 210 | Visit16 | 14.3 | 5.2 | 104 |

This subject now has a data row for VISIT9 (with missing values) even though VISIT9 was not in the original data for this subject. This implies that at least one subject had a VISIT9. Since VISIT3 still does not appear, we can infer that no subject in our study had a VISIT3. This technique requires that the row that is to be spared (visits 3 and 9) appear in the data set somewhere at least once.

Remember when using PROC TRANSPOSE that it is *very* important that some combination of the BY and ID variables identify down to the row level (see Section 2.4.1).

# **MORE INFORMATION**

The TRANSPOSE procedure and some of its pitfalls (gotecha's) can be found in Section 2.4.1.