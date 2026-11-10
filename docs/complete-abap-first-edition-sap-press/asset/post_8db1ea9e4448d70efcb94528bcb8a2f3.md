
![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_264_0.png)

**Figure 7-5** START-OF-SELECTION Acts as Default Event

In general, you put all the data selection logic of your ABAP program within the START-OF-SELECTION event. Here, the program starts selecting values from tables. In a typical report program, you initialize the program data under the INITIALIZATION event, validate the selection screen inputs under the selection screen events, and, if everything looks fine, proceed with the data selection (based on the selection criteria) under the START-OF-SELECTION event.

## GET table

The GET table event is used when the executable program uses a logical database for data selection. A logical database is a special ABAP program that retrieves data from the database and makes it available to the application program. In other words, when you use a logical database in your program, you do not need to code the SQL statements to retrieve the data from the database.

The logical database itself contains the Open SQL statements that retrieve the data from the database and pass the data line by line to the interface work area of your application program.

A logical database consists of a program with selection screen and authorization checks. When a logical database is used for the report program, the program can automatically inherit the selection screen and authorization checks.

Interface work areas are defined using the `TABLES` or `NODES` keywords, and they work similarly to the work areas defined using the `DATA` keyword, with just one basic difference. These interface work areas are created in the shared data area between the programs. In other words, when you define a work area using the `DATA` keyword, it is defined in the memory space of the program. Interface work areas are defined in the shared memory space of the session, which all the programs running in the same session can have access to. For this reason, using `TABLES` is not recommended, as it can produce side effects.

In older versions of the SAP ERP system, the only way to use a logical database was to link it to an executable program and use `GET` events to retrieve the data. However, since release SAP R/3 4.5A, it's been possible to call a logical database in any program using the `LDB_PROCESS` function module. This module allows you to call many logical databases in your program, nested in any order. In this respect, the use of interface work areas is practically obsolete, available only for backward compatibility with earlier releases.

The `GET` event is triggered when the logical database has read a line from the table mentioned in the event keyword and made it available to the program in the work area declared using the `TABLES` `<table>` or `NODES` `<table>` statement (as seen in Listing 7.12).

```abap
    NODES: SPFLI.
    GET SPFLI.
      SKIP.
      WRITE: / 'From:', SPFLI-CITYFROM,
             'To  :', SPFLI-CITYTO.
```

**Listing 7.12** Code Showing GET Event

### GET `<table>` LATE

Once all of the data records for a node of the logical database have been read, the ABAP runtime environment triggers the `GET <table> LATE` event. By maintaining this event in the program, you can process the steps that should be executed at the end of the block. For example, if you want to print an itemized summary of sales orders, you can do so in this event block.

Listing 7.13 shows the implementation of this event block.

```abap
NODES: SPFLI, SFLIGHT, SBOOK.
DATA WEIGHT TYPE I VALUE 0.
GET SPFLI.
SKIP.
WRITE: / 'Carrid:', SPFLI-CARRID,
       'Connid:', SPFLI-CONNID,
       / 'From:', SPFLI-CITYFROM,
       'To:', SPFLI-CITYTO.
ULINE.
GET SFLIGHT.
SKIP.
WRITE: / 'Date:', SFLIGHT-FLDATE.
GET SBOOK.
WEIGHT = WEIGHT + SBOOK-LUGGWEIGHT.
GET SFLIGHT LATE.
WRITE: / 'Total luggage weight =', WEIGHT.
ULINE.
CLEAR WEIGHT.
```

**Listing 7.13** Code Showing GET `<table>` LATE Event

In Listing 7.13, we're printing the date-wise summary of the total luggage weight for each airline code (CARRID) and flight connection number (CONNID). We retrieve the flight details using the GET SPFLI event. The GET SFLIGHT event loops through all the flights for a given date (the user can restrict the range on the logical database selection screen).

The GET SBOOK event retrieves the luggage weight for each booking from table SBOOK for the respective flight. Within this event, we're aggregating the total weight for the given date.

Finally, the GET SFLIGHT LATE event is called at the end once all the records for the flights in a given date are processed. In this event, we're printing the total luggage weight for the given date for the respective CARRID and CONNID. For this example, we're using the logical database selection F1S, which you can check using Transaction SLDB.

## END-OF-SELECTION

The END-OF-SELECTION event is used to mark the end of selection. If your report isn't using a logical database, then this event is used after a START-OF-SELECTION event to mark the end of selection and to continue with further processing of the selected data, such as printing the selected data in the output. However, if your report is linked to a logical database, this event is called after the logical database has completely transferred all the records to the application program.

For example, in Listing 7.13, if all the data from the logical database selection is updated in an internal table that you then want to process further, you can use the END-OF-SELECTION event to mark the end of data selection and implement the logic to further process the selected data. The END-OF-SELECTION event is called by the runtime environment after processing all the GET events.

Using this event becomes mandatory to separate the selection logic from the output logic when using a logical database. Otherwise, its purpose is purely for documentation and for making the code legible. We recommend using this event to mark the separation from selection logic to output logic even if no logical database is used in the program.

Listing 7.14 shows an example using the END-OF-SELECTION event.

```abap
NODES: SPFLI, SFLIGHT, SBOOK.
DATA: gr_table TYPE REF TO cl_salv_hierseq_table.
DATA: it_spfli TYPE TABLE OF spfli.
DATA: it_sflight TYPE TABLE OF sflight.
DATA: it_binding TYPE salv_t_hierseq_binding.
DATA: wa_binding LIKE LINE OF it_binding.

GET SPFLI.
APPEND spfli TO it_spfli.
GET SFLIGHT.
APPEND sflight TO it_sflight.

END-OF-SELECTION.
wa_binding-master = 'CARRID'.
wa_binding-slave = 'CARRID'.
APPEND wa_binding TO it_binding.

wa_binding-master = 'CONNID'.
wa_binding-slave = 'CONNID'.
APPEND wa_binding TO it_binding.

cl_salv_hierseq_table=>factory(
  EXPORTING
    t_binding_level1_level2 = it_binding
  IMPORTING
    r_hierseq = gr_table
  CHANGING
    t_table_level1 = it_spfli
    t_table_level2 = it_sflight ).
gr_table->display( ).
```

**Listing 7.14** END-OF-SELECTION Event

In **Listing 7.14**, we're filling the internal tables `IT_SPFLI` and `IT_SFLIGHT` within the `GET SPFLI` and `GET SFLIGHT` events, respectively. We're then displaying this data as a hierarchical sequential display using the ALV object model within the `END-OF-SELECTION` event.

The ALV object model makes it easy to generate the ALV output. We’ll discuss the ALV object model further in **Chapter 15**.

### 7.3.3 Selection Screen Events

*Selection screens* are special screens that allow the user to input the selection criteria for a program. These are typically used in report programs (executable programs), but can also be used in module pool programs or function groups.

Selection screen events typically help to prepare the selection screen and evaluate user actions on the screen. For example, we can use selection screen events to assign default values to the input fields at runtime, dynamically disable or enable certain fields, or validate user input and show appropriate messages to the user.

Selection screen events are triggered when a selection screen is defined for the program and is processed by the ABAP runtime environment. If there is no selection screen defined for the program, none of the selection screen events are triggered.

Selection screens are categorized as special screens that can be defined using ABAP statements (`PARAMETERS` or `SELECT-OPTIONS`) and are generated by the ABAP compiler automatically, rather than defined manually using the Screen Painter (like general screens).

Because selection screens are generated automatically, programmers don't have access to the screen flow logic in which they can define dialog modules to modify the screen or react to user actions. The ABAP runtime environment fully controls the screen processing, generating a number of selection screen events through which programmers can maintain the event blocks in the program to react to these events.
