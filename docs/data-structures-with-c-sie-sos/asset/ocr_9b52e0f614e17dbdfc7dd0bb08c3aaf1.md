```
}
STRES[m]='\0';
return(STRES);
}
```

Output:
The number of paragraphs in short story S are 2

# 3.15 Write a procedure which counts the number NUM of times the word “the” appears in the short story S. (We do not count “the” in “mother,” and we assume no sentence ends with the word “the.”

Note that the word “the” can appear as THE□ at the beginning of a line, as □THE at the end of a line, or as □THE□ elsewhere in a line. Hence we must check these three cases for each line. The procedure follows.

+   Procedure P3.15: COUNT(LINE, N, NUM)
+   1. Set WORD := "THE' and NUM := 0.
+   2. [Prepare for the three cases.]
+      Set BEG := WORD//'□', END := '□'//WORD and
+      MID := '□' //WORD// '□'.
+   3. Repeat Steps 4 through 6 for K = 1 to N:
+   4. [First case.] If SUBSTRING(LINE[K], 1, 4) = BEG, then:
+      Set NUM := NUM + 1.
+   5. [Second case.] If SUBSTRING(LINE[K], 77, 4) = END, then:
+      Set NUM := NUM + 1.
+   6. [General case.] Repeat for J = 2 to 76.
+      If SUBSTRING(LINE[K], J, 5) = MID, then:
+      Set NUM := NUM + 1.
+      [End of If structure.]
+      [End of Step 6 loop.]
+      [End of Step 3 loop.]
+   7. Return.

# Program 3.9

```
/* C implementation of Procedure 3.15 */
#include <stdio.h>
#include <conio.h>
#include <string.h>

char S[10][80]={(“This is the story of a boy”),
(“who lived in Delhi”),
(“
His name was Rohan”),
(“THE Dummy Text: Checking THE use of THE string THE”),
```