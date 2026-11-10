For example, in Listing 16.14, we are assigning the first row of the internal table `IT_MARA` to the `<FS_MARA>` field symbol.

After this assignment, the field symbol will point to the first row of the internal table, and you can change any field in the row directly using the field symbol.

In this example, the `<FS_MARA>-MTART = 'ROH'` statement will change the value of the `MTART` field in the first row of the internal table. Unlike a work area, when using a field symbol you don't need to use the `MODIFY` statement to copy the contents of the work area back to the internal table.

```
```abap
TYPES: BEGIN OF ty_mara.
         matnr TYPE matnr.
         ersda TYPE ersda.
         mtart TYPE mtart.
       END OF ty_mara.
DATA: it_mara TYPE TABLE OF ty_mara.
FIELD-SYMBOLS: <fs_mara> LIKE LINE OF it_mara.
PARAMETERS p_matnr TYPE matnr.
SELECT matnr ersda mtart FROM mara INTO TABLE it_mara WHERE matnr EQ p_
matnr.
READ TABLE it_mara ASSIGNING <fs_mara> INDEX 1.
IF <fs_mara> IS ASSIGNED.
  <fs_mara>-mtart = 'ROH'.
ENDIF.
```
```

**Listing 16.14** Assigning Internal Table Record to Field Symbol

# 16.1.4 Checking if a Field Symbol is Assigned

When a data object is assigned to a field symbol, the `SY-SUBRC` system field is set to 0. If you want to check immediately after the assignment, you can check the `SY-SUBRC` field, as shown in Listing 16.15.

```
```abap
ASSIGN dobj TO <fs>.
IF sy-subrc IS INITIAL.
  <fs> = 123.
ENDIF.
```
```

**Listing 16.15** Checking the SY-SUBRC Field

However, in most situations, you won't need to access the field symbol immediately after the assignment but may need to access it later in the code. In such situations, checking the `SY-SUBRC` system field isn't useful, because `SY-SUBRC` is