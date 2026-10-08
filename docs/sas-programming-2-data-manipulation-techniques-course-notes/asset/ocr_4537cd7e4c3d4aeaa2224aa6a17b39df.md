# FIND Function

```
data find;
Text='AUSTRALIA, DENMARK, 'US';
Pos1=find(Text,'US');
Pos2=find(Text,'US');
Pos3=find(Text,'us');
Pos4=find(Text,'us','I');
Pos5=find(Text,'us','I',10);
```

run;

| Pos1 | Pos2 | Pos3 | Pos4 | Pos5 |
| N 8 | N 8 | N 8 | N 8 | N 8 |
| 2 | 20 | 0 | 2 | 21 |

# Data Cleanup: Step 1

Use the SUBSTR and FIND functions to change incorrect product IDs for mittens.

```
SUBSTR(string,start,<length>)=value;
data correct;
set orion.clean_up;
if find(Product,'Mittens','I')>0 then do;
substr(Product_ID,9,1)='5';
end;
proc print data=correct noobs;
```