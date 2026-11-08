# CONTENTS

The CONTAINS operator works much like the INDEX function to determine if a text string can be found within another string. The word CONTAINS can be replaced with its mnemonic, the question mark (?).

```
title2 'CONTAINS';
proc print data=advrpt.demog;
    var lname fname edu;
    where lname contains 'son';
/*  where lname ? 'son';*/
/*  where index(lname,'son');*/
    run;
```

+   3. All last names that contain the letters ‘son’ will be printed. Like all string comparisons the search is case sensitive.
+   4. The question mark could be used to replace the CONTAINS operator.
+   5. The INDEX function could also be used.

CONTAINS is negated by preceding the operator with a NOT or other negation mnemonic.

# IS MISSING

The IS MISSING operator can be used to check for missing values. One advantage is that it can be used to check for either a numeric or a character missing value. Either the IS MISSING or the IS NULL operator can be used.

```
title2 'IS MISSING';
proc print data=advrpt.demog;
    var lname fname edu symp;
    where edu is missing or symp is missing;
/*  where edu is null or symp is null;*/
/*  where edu = . or symp = ' ';*/
    run;
```

+   6. The syntax is the same for numeric variables (EDU) and character variables (SYMP).
+   7. IS NULL can be used instead of IS MISSING.
+   8. When checking for missing values using the ‘traditional’ approach the programmer must be aware of the variable’s type.

Negation is formed using NOT (or other negation operator). The NOT may appear either before the IS or between the IS and MISSING.

```
where edu is not missing or symp not is missing;
```

# LIKE

The LIKE operator allows for simple pattern matching. When appropriate, more complex pattern matching can be accomplished using regular expressions in the RX() family of functions. This operator uses the percent sign (%) and the underscore (_) as wildcards. The % will stand for any number of characters and the _ is a place holder for exactly one character.

The following table shows some examples using the LIKE operator and alternate equivalent expressions.

| Using the LIKE Operator | Without the LIKE Operator | What It Does |
|---|---|---|
| `lname like 'S%'` | `lname = 'S'`<br>`substr(lname,1,1) = 'S'` | Find all last names beginning with a capital S. |
| `lname like '%ly%'` | `index(lname,'ly') > 0`<br>`lname contains 'ly'` | Find all last names containing an 'ly'. |
| `lname like 'Ch__'` | `substr(lname,1,2) = 'Ch' and`<br>`length(lname)<5` | Any two, three, or four letter last names starting with Ch. |