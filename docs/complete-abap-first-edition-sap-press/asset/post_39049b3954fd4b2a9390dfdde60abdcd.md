
![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_808_0.png)

**Figure 19.4** Third Screen of Transaction MM01

To create another material, you repeat the same steps with a different set of data. If you want to create only a few materials, it’s easy to create materials manually via this transaction. But what if you want to create hundreds or thousands of materials? We can automate this process by creating a batch input program. We’ll walk through the steps for doing so in the next subsection.

## Creating a Batch Input Program

A batch input program requires you to capture the screen and field information in an internal table with a special structure known as BDCDATA (BDC here indicates *batch data communication*).

The BDCDATA structure is shown in Figure 19.5.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_808_1.png)

**Figure 19.5** BDCDATA Structure

The BDCDATA structure consists of five components, as detailed in Table 19.2.

| Field Name | Meaning |
| --- | --- |
| PROGRAM | Program name of the screen to which the data is transferred |
| DYNPRO | Screen number of the program (specified in the PROGRAM field above) |
| DYNBEGIN | Flag to indicate new screen |
| FNAM | Field name of the screen |
| FVAL | Value to be transferred to the field |

Table 19.2 BDCDATA Structure Components

The basic concept behind developing a batch input program is that you capture the program name and screen field names of the transaction and map the values that should be passed to the screen fields using table BDCDATA. For example, if you look at the initial screen of Transaction MM01 and use the [F1] help on the MATERIAL field to look at the technical information, you can find the technical details of the field as shown in Figure 19.6.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_809_0.png)

Figure 19.6 Technical Information about Screen Field

Notice that the program name is SAPLMGMM, the screen number is 0060, and the screen field name is RMG1-MATNR. Using this information, we can map the BDCDATA structure, as shown in Listing 19.1.

```abap
PROGRAM ZDEMO_BATCH_INPUT.
Data: it_bdcdata TYPE STANDARD TABLE OF bdcdata,
      wa_bdcdata TYPE bdcdata.
START-OF-SELECTION.
  perform bdc_dynpro      USING 'SAPLMGMM' '0060'.
  perform bdc_field       USING 'RMG1-MATNR' '567A5HG'.
  PERFORM bdc_field       USING 'RMG1-MBRSH' 'P'.
  PERFORM bdc_field       USING 'RMG1-MTART' 'ROH'.
  PERFORM bdc_dynpro      USING 'SAPLMGMM' '0070'.
  ........
FORM bdc_dynpro USING program dynpro.
  CLEAR wa_bdcdata.
  wa_bdcdata-program = program.
  wa_bdcdata-dynpro = dynpro.
  wa_bdcdata-dynbegin = 'X'.
  APPEND wa_bdcdata TO it_bdcdata.
ENDFORM.
FORM bdc_field USING fnam fval.
  CLEAR wa_bdcdata.
  wa_bdcdata-fnam = fnam.
  wa_bdcdata-fval = fval.
  APPEND wa_bdcdata TO it_bdcdata.
ENDFORM.
```

**Listing 19.1** Filling BDCDATA Structure

In Listing 19.1, we defined an internal table it_bdcdata with the line type as BDCDATA. We defined two subroutines, BDC_DYNPRO and BDC_FIELD. In the BDC_DYNPRO subroutine, we're filling the program name and screen number. In the BDC_FIELD subroutine, we're filling the field name and field value. The PERFORM statements for both these subroutines are passing two actual parameters.

For example, the PERFORM BDC_DYNPRO statement is passing the program name and screen number as literals, and the PERFORM BDC_FIELD statement is passing the field name and field value. In our example, we're passing the literals for the field value, but the literal will be replaced with the field value uploaded from the sequential file. We're flagging dynbegin as X in the BDC_DYNPRO subroutine, because this subroutine is called only when new screen information needs to be passed.

Once the internal table is filled with all the required screen and field information, we can pass the data by using either the CALL TRANSACTION method or the SESSION method. We'll look at these methods in the next two subsections.

### CALL TRANSACTION

In the CALL TRANSACTION method, BDCDATA is passed to the transaction using the CALL TRANSACTION USING statement. The internal table that contains BDCDATA is passed with the statement. The transaction can be executed in foreground mode, background mode, or foreground on error mode.

When a transaction is executed in *foreground mode*, the transaction runs in the foreground, displaying all the screens. Running a transaction in foreground mode is useful when doing a test run, because it helps verify that the fields are mapped correctly with the right data.

When a transaction is executed in *background mode*, the transaction completely runs in the background and no screens are displayed. Any messages raised by the transaction during the execution will be transferred to the batch input program at the end.

Running a transaction in background mode is the preferred method for production runs. If *foreground on error* mode is used, the transaction runs in the background unless any error messages are raised by the transaction. If an error message is raised, the transaction screen that has caused the error is displayed to the user.

Data can be updated synchronously or asynchronously. With synchronous updates, the system waits for the previous transaction to commit, while with asynchronous updates, the system will start processing the next transaction without waiting for the previous transaction to commit.

For example, if you're updating a sales order header and item data, synchronous updates can ensure that the sales order item data is updated only after the header data is committed to the database. If you use asynchronous updates, the sales order item data may commit to the database without waiting for the header data to commit first. For this reason, an asynchronous update is faster than a synchronous update.

The CALL TRANSACTION method doesn't support an automated error log or resuming on error. Error handling should be performed in the program. You can call one transaction at a time, and the data is processed synchronously.

### SESSION

In the SESSION method, we generate a session with all the data. The session is then processed separately. The session can be processed manually or at regular intervals by scheduling the program RSDCSUB as a background job. This method automatically creates an error log in case of any errors.

The error transactions can be processed, after correcting the errors, by resuming the session. The BDC program opens the session (using function module BDC_OPEN_GROUP), writes the data to the session (using function module BDC_INSERT), and closes the session (using function module BDC_CLOSE_GROUP). The previous session should be closed before opening a new session.

The SESSION method can be used to transfer data to multiple transactions and perform a synchronous database update. For example, you can use the SESSION method to post the header and item data of a document and have the system update the item data after updating the header data.

Transactions should always be updated in background mode; foreground mode should be used only for testing the screen sequence.

Both the CALL TRANSACTION method and the SESSION method require you to pass the screen and field information of the transaction using table BDCDATA. However, capturing all the screen and field information manually is a tedious job. To make this easy and generate a batch input program, SAP provides a tool called Transaction Recorder (Transaction SHDB).

In the next subsection, we'll discuss the steps for generating a batch input program with Transaction SHDB.

### Creating a Batch Input Program Using the Transaction Recorder

Using Transaction Recorder, we can simulate the sequence of steps performed by the transaction to capture all the required information for table BDCDATA. Transaction Recorder also supports generating the batch input program using this information.

The following steps walk through generating a batch input program via Transaction Recorder:

1. On the initial screen of Transaction SHDB (Transaction Recorder: Recording Overview), as shown in Figure 19.7, click the New Recording button.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_813_0.png)

**Figure 19.7** Transaction Recorder Initial Screen

2. In the Create Recording dialog box, as shown in Figure 19.8, provide a name for the recording and enter the transaction code for which the recording should be performed. You can also set the Update Mode to update the data. There are three update modes available, as listed in Table 19.3.

| Update Mode | Meaning |
| --- | --- |
| Local | The update task is carried out by the dialog work process that is processing the transaction. |
| Asynchronous | The update is performed by the update work process asynchronously. |
| Synchronous | The update is performed by the update work process synchronously. |

**Table 19.3** Update Mode Options

Also provide the following settings in the Create Recording box (Figure 19.8):

- Select the Default Size checkbox to avoid screen resolution issues and use a default size for recording.
- The Cont. After Commit checkbox sets a flag to continue processing when a commit work is performed while using the CALL TRANSACTION method.
