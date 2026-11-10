# IDoc Structure

IDocs are stored internally in the database in the following database tables:

+   - **EDIDC**
+   
+     The control record is stored in database table EDIDC with a unique IDoc number (see Figure 19.31). Each IDoc has one record in this table and is uniquely identified by the IDoc number. Other details about the IDoc, such as IDoc status, direction, receiver port, partner details, and so on, are also stored in this table.

![](bbox=[0.138, 0.28, 0.852, 0.629])

Figure 19.31 Table EDIDC

+   - **EDID4**
+   
+     The data records of the IDoc are stored in this table, linking the control record with the document number. There can be one to many records for each IDoc. This table stores the segment information and the application data for the IDoc. The SData field in table EDID4 contains the application data. This field is parsed in the program at runtime to a structure of the type of the IDoc segment.