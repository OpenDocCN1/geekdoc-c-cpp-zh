# # 150 PROC SQL: Beyond the Basics Using SAS, Second Edition

variable is not one of these three values, then a program warning message is displayed in the SAS log. Invoking the macro with %VIEW(Products) produces the following results.



```
```sas
%MACRO VIEW(NAME);
%IF %UPCASE(&NAME) ^= %STR(PRODUCTS) AND
%UPCASE(&NAME) ^= %STR(MANUFACTURERS) AND
%UPCASE(&NAME) ^= %STR(INVENTORY) %THEN %DO;
%PUT A valid view name was not supplied and no output will be generated!;
%END;
%ELSE %DO;
PROC SQL;
TITLE "Listing of &NAME View";
%IF %UPCASE(&NAME)=%STR(PRODUCTS) %THEN %DO;
SELECT PRODNAME,
PRODCOST
FROM &NAME._view
ORDER BY PRODCOST;
%END;
%ELSE %IF %UPCASE(&NAME)=%STR(MANUFACTURERS) %THEN %DO;
SELECT MANUNAME,
MANUCITY,
MANUSTAT
FROM &NAME._view
ORDER BY MANUCITY;
%END;
%ELSE %IF %UPCASE(&NAME)=%STR(INVENTORY) %THEN %DO;
SELECT PRODNUM,
INVENQTY,
INVENCOST
FROM &NAME._view
ORDER BY INVENCOST;
%END;
QUIT;
%END;
%END;
%MEND VIEW;
```
```

In the previous example, if a name is supplied to the macro variable &NAME that is not valid, then the user-defined program warning message would be displayed in the SAS log. Suppose we invoked the VIEW macro by entering %VIEW(Customers). The results are displayed in the SAS log.



```
```sas
%VIEW(Customers);
```
```