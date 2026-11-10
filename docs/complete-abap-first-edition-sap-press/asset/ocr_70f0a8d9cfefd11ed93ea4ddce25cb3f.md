For the example, we'll use the driver program to fetch the data from the billing document header and item tables VBRK and VBRP, respectively. In this driver pro-gram, we'll call a form to initiate form processing.

The code in Listing 18.1 shows the selection logic in the driver program.

```
REPORT zdemo_sapscript_driver.
*Document header data
TYPES : BEGIN OF ty_vbrk,
          vbeln TYPE vbeln_vf,
          fkdat TYPE fkdat,
          kunrg TYPE kunrg,
          netwr TYPE netwr,
        END OF ty_vbrk.
*Document item data
TYPES : BEGIN OF ty_vbrp,
          vbeln TYPE vbeln_vf,
          posnr TYPE posnr,
          arktx TYPE arktx,
          netwr TYPE netwr,
        END OF ty_vbrp.

*Customer data
TYPES : BEGIN OF ty_knal,
          kunnr TYPE kunnr,
          land1 TYPE land1_gp,
          name1 TYPE name1_gp,
          name2 TYPE name2_gp,
          ort01 TYPE ort01_gp,
        END OF ty_knal.


DATA : wa_vbrk TYPE ty_vbrk,
       wa_knal TYPE ty_knal,
       it_vbrp TYPE STANDARD TABLE OF ty_vbrp,
       wa_vbrp TYPE ty_vbrp.

PARAMETERS p_vbeln TYPE vbeln_vf.

START-OF-SELECTION.
  PERFORM fetch_data.
  PERFORM print_form.
*&---------------------------------------------------------------------*
*&      Form  FETCH_DATA
*&---------------------------------------------------------------------*
FORM fetch_data .
  SELECT SINGLE vbeln fkdat kunrg netwr FROM vbrk INTO wa_
  vbrk WHERE vbeln EQ p_vbeln.
    IF sy-subrc IS INITIAL.
```