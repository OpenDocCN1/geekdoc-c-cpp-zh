+   ⑥ The data set LABTRAN will be transposed back to the original set of rows and columns.

+   ⑦ By default rows in the new data set (SPARSED) will be identified with the variable _NAME_.
+   This variable is renamed to VISIT.

+   ⑧ The incoming data set (LABTRAN) has one observation per SUBJECT_NAME_
+   combination.

+   ⑨ The ID statement identifies the variable (_NAME_) that contains the names of the new
+   columns.

+   ⑩ Each of the variables starting with VISIT is included in the transpose (see Section 2.6.1 for
+   more on variable list abbreviations).

Prior to the first transpose, inspection of the data for SUBJECT=210 shows that this subject has
missed both visits 3 and 9.

```
2.5.2 Creating a Sparse Table
Using a Double Transpose
Prior to First Transpose

  Obs    SUBJECT    VISIT          LABDT    potassium    sodium    chloride

   95      210        1         02/19/2007      5.0        14.0       103
   96      210        2         02/28/2007      4.0        14.2       103
   97      210        4         03/14/2007      3.9        14.1       101
   98      210        5         03/09/2007      4.7        14.4       105
   99      210        6         03/16/2007      4.7        14.5       104
  100      210        7         03/26/2007      4.7        14.3       103
  101      210        8         03/28/2007      4.4        14.1       102
  102      210       10         07/10/2007      4.3        14.2       106
  103      210       11         04/06/2007      4.1        14.2       104
  104      210       12         04/17/2007      4.0        13.9       103
  105      210       13         04/19/2007      4.4        14.2       104
  106      210       14         04/26/2007      4.1        14.1        99
  107      210       15         05/22/2007      3.8        13.8        99
  108      210       16         06/27/2007      5.2        14.3       109
```

After the first PROC TRANSPOSE ❷ the data (WORK.LABTRAN) looks like the following (for
SUBJECT=210). There is now a VISIT9 column for this subject, even though this subject did not
have a VISIT9 in the data; however, there is still no column for visit 3. This is because no subject
in the entire data set had a VISIT3.