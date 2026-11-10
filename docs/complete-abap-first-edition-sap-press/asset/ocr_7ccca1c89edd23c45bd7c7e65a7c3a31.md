```
```abap
S_ZMAKTID-mtnr = w_makt-mtnr.
S_ZMAKTID-spras = w_makt-spras.
S_ZMAKTID-matnr = w_makt-matnr.
IDOC_DATA = SEGNAME = C_ZMAKTID.
IDOC_DATA = SDATA = S_ZMAKTID.
APPEND IDOC_DATA.
CLEAR IDOC_DATA.
ENDLOOP.

*Send Idoc
CALL FUNCTION 'MASTER_IDOC_DISTRIBUTE'
  EXPORTING
    MASTER_IDOC_CONTROL              = control_record_out
  TABLES
    COMMUNICATION_IDOC_CONTROL       = T_COMM_IDOC
    MASTER_IDOC_DATA                 = IDOC_DATA
  EXCEPTIONS
    ERROR_IN_IDOC_CONTROL            = 1
    ERROR_WRITING_IDOC_STATUS        = 2
    ERROR_IN_IDOC_DATA               = 3
    SENDING_LOGICAL_SYSTEM_UNKNOWN   = 4
    OTHERS                           = 5.
IF SY-SUBRC <> 0.
*Update IDoc status
ENDIF.
```
```

**Listing 19.3** Outbound Program

In Listing 19.3, we selected the data from the application table and filled the IDoc data structure. This data is then sent to the MASTER_IDOC_DISTRIBUTE function module along with the control record to generate the IDoc.

In this section, we discussed the steps for creating and generating IDocs to be used with EDI and ALE technologies. In the next section, we'll look at a tool used to migrate data from legacy systems.

# 19.4  Legacy System Migration Workbench

Legacy System Migration Workbench (LSMW) is a tool provided by SAP to quickly migrate data from legacy systems. This tool targets functional consultants and end users and doesn't require any ABAP knowledge. The tool provides different options to migrate data, such as the direct input method, batch input method, BAPIs, or IDocs.