# Inbound Program

In an *inbound program*, the function module should use the standard interface using the EDIDC and EDIDD structures. The IDoc control record will be filled in the EDIDC structure, which can be used to validate if the inbound program is called for the correct message type. The EDIDD structure is an internal table that contains the data records. The SDATA field of the EDIDD structure contains the unformatted row, which can be parsed to a structure of the correct segment type. This row is then updated in the database.

The easy way to define an interface is to copy the interface from an existing inbound function module. Listing 19.2 shows the inbound function code in its bare minimum form. This inbound function module is configured in Transaction WE42.

```
FUNCTION ZDEMO_IDOC_INPUT.
*"---------------------------------------------------------------------
*"*Local Interface:
*"  TABLES
*"      IDOC_CONTROL STRUCTURE  EDIDC
*"      IDOC_DATA STRUCTURE  EDIDD
*"      IDOC_STATUS STRUCTURE  BDIDOCSTAT
*"---------------------------------------------------------------------
    DATA : wa_makt TYPE zmakt.
           st_seg TYPE zseg1.
           it_makt TYPE STANDARD TABLE OF zmakt.

    LOOP AT IDOC_DATA WHERE DOCNUM EQ IDOC_CONTROL-DOCNUM.
      st_seg = IDOC_DATA-SDATA.
      MOVE-CORRESPONDING st_seg TO wa_makt.
      APPEND wa_makt to it_makt.
    ENDLOOP.
    MODIFY zmakt FROM TABLE it_makt.
    IF sy-subrc IS INITIAL.
      IDOC_STATUS-DOCNUM = IDOC_CONTROL-DOCNUM.
      IDOC_STATUS-STATUS = '53'.
      IDOC_STATUS-MSGTY = 'I'.
      IDOC_STATUS-MSGID = 'YM'.
      IDOC_STATUS-MSGNO = '004'.
      APPEND IDOC_STATUS.
    ELSE.
      IDOC_STATUS-DOCNUM = IDOC_CONTROL-DOCNUM.
      IDOC_STATUS-STATUS = '51'.
      IDOC_STATUS-MSGTY = 'E'.
      IDOC_STATUS-MSGID = 'YM'.
```