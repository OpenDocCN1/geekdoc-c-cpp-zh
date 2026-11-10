In the EDI process, an ABAP program selects the application data from the database and generates an IDoc. This IDoc is then pushed to the OS level, to a specific directory from which the subsystem will pick up the IDoc for processing. The subsystem will first perform a syntax check to ensure the IDoc is in the correct format and all mandatory fields are filled.

The IDoc consists of a control record, multiple data records, and multiple status records:

+   - **Control record**: The *control record* consists of the general information about the IDoc, such as the type of document (called the message type), the business partner details, and so on. You'll learn more about the control record when we discuss IDoc development in the upcoming subsections.
+   - **Data records**: *Data records* consist of the actual data of the document.
+   - **Status records**: *Status records* are updated with the status of the IDoc at each processing step.

The subsystem converts the IDoc to EDI format. It uses the control record of the IDoc to identify the partner details and the message type being exchanged. Based on the message type, the required syntax checks are performed to ensure data consistency. The subsystem takes care of stripping the control record before transmitting the document to the business partner.

Once the IDoc is converted to an EDI document, the subsystem establishes a connection with the business partner's system (either through direct connection to the partner's network or through VAN) and transmits the document. Once the acknowledgment is received from the business partner that the document has been received successfully, the subsystem updates the IDoc with the status message. The IDoc is updated with the status message at each step of the process to help identify any issues.

In the inbound process, the EDI transmission is received by the subsystem and takes care of converting the EDI document to an IDoc. SAP provides program `STARTRFC` to start any RFC-enabled function module from the operating system level. The subsystem uses program `STARTRFC` to call the `EDI_DATA_INCOMING` function module to trigger the inbound processing. The control record of the IDoc is used to identify the partner profile, using which the ABAP posting program is