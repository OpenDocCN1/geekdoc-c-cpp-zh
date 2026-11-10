```
wa_sflight-connid = '0007'.
wa_sflight-fldate = '20140104'.
INSERT wa_sflight INTO it_sflight INDEX 1
```

**Listing 5.15** Adding Records Using INSERT Statement

The syntax to use the INSERT statement is the same for all table types. However, index operations can’t be performed on hash keys.

# System Fields

System fields are always available in ABAP programs and they are filled by the runtime system based on the context. You query the system fields in the program to identify the status. For example, you can query the system field `subrc` to learn whether an INSERT operation was successful or whether a SELECT statement could find a matching record in the database.

System fields are available as variables in the program. However, they should be treated like constants and should never be manipulated. All system fields are available in the ABAP Data Dictionary structure `SYST` and can be accessed in the program using the pre-defined structure `SY`. For example, to access the system field `subrc` in an ABAP program, use the structure reference `sy` followed by the field name separated by a hyphen, as in `sy-subrc`.

To refer your program data types and data objects to system fields, use the `SYST` structure reference. For example, `DATA lv_index TYPE syst-index`.

Often, you’ll perform an INITIAL check on system fields to see if a statement was successful, as shown in Listing 5.16.

```
READ TABLE it_sflight INTO wa_sflight WITH KEY carrid = 'AA'.
IF sy-subrc IS INITIAL.
******
ELSE.
******
ENDIF.
```

**Listing 5.16** System Fields

This example checks if the READ statement could successfully find a matching record and accordingly build the program logic. In this case, `sy-subrc` will have its initial value if the READ statement was successful; otherwise, it will have a value other than its initial value.

Each keyword updates different system fields with different values based on the context. The keyword documentation helps you understand the system field values set by different keywords. To open the keyword documentation, simply press F1 in the ABAP Editor.