```
AT END OF connid.
*The code here will be executed if the value of either carrid or
*connid will be different in the next loop pass.
ENDAT.
AT LAST.
*The code here will be executed only in last loop pass.
ENDAT.
ENDLOOP
```

Listing 5.21 Control Break Statements

Control break statements can be maintained in any order in the loop, because they're always triggered on the control break and not by the order in which they are maintained in the code.

The code sample in Listing 5.22 shows an example of some control break statements. The code in this example prints the header and item details of a billing document, highlighting how control break statements can be used to control the report output.

```
*Billing document header structure
TYPES: BEGIN OF TY_VBRK,
         VBELN TYPE VBELN_VF, "Document Number
         FKDAT TYPE FKDAT, "Bill Date
         NETWR TYPE NETWR, "Net Value
         KUNRG TYPE KUNRG, "Payer
       END OF TY_VBRK.

*Billing document item structure
TYPES: BEGIN OF TY_VBRP,
         VBELN TYPE VBELN_VF, "Document Number
         POSNR TYPE POSNR_VF, "Item Number
         ARKTX TYPE ARKTX, "Description
         FKIMG TYPE FKIMG, "Qty
         VRKME TYPE VRKME, "Sales Unit
         NETWR TYPE NETWR_FP, "Net Value
         MATNR TYPE MATNR, "Material Num
         MWSBP TYPE MWSBP, "Tax amt
       END OF TY_VBRP.

DATA: it_vbrp TYPE TABLE OF ty_vbrp,
      it_vbrk TYPE TABLE OF ty_vbrk,
      wa_vbrk TYPE ty_vbrk,
      wa_vbrp TYPE ty_vbrp.

*Selection screen declaration for user selection criteria
SELECT-OPTIONS: s_vbeln FOR wa_vbrp-vbeln.
```