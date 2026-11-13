```
K=K+1;
}
return(NUM1);
}
char* SUBSTR(char *STR,int i,int j)
{
int k,m=0;
char STRRES[80];
for(k=i-1;k<=i+j-1;k++)
{
STRRES[m]=STR[k];
m=m+1;
}
STRRES[m]='\\0';
return(STRRES);
}
```

Output:
The number of instances of WORD in short story S are 4

# 3.16 Discuss the changes that must be made in Procedure P3.15 if one wants to count the number of occurrences of an arbitrary word W with length R.

+   There are three basic types of changes.
+   (a) Clearly, 'THE' must be changed to W in Step 1.
+   (b) Since the length of W is r and not 3, appropriate changes must be made in Steps 3 to 6.
+   (c) One must also consider the possibility that W will be followed by some punctuation,
+   e.g.,
+   W,   W;   W.   W?
+   Hence more than the three cases must be treated.

# 3.17 Outline an algorithm which will interchange the kth and lth paragraphs in the short story S.

The algorithm reduces to two procedures:
Procedure A. Find the values of arrays BEG and END where
LINE[BEG[K]]   and   LINE[END[K]]
contain, respectively, the first and last lines of paragraph K of the story S.
Procedure B. Using the values of BEG[K] and END[K] and the values of BEG[L] and
END[L], interchange the block of lines of paragraph K with the block of
lines of paragraph L.