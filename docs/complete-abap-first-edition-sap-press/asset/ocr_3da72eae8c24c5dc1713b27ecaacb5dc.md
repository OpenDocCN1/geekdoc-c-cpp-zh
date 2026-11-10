When developing an IDoc, a segment is defined that contains the fields to store the application data. *Segments* are stored in ABAP Data Dictionary as structure types.

For example, say you want to generate an IDoc for a billing document with data such as document number, payer, and net value. To store this data about the billing document in an IDoc, define a segment with fields such as `VBELN`, `KUNRG`, and `NETWR` to store the document number, payer, and net value, respectively. This segment translates to a data record when the IDoc is generated and stored in table `EDID4` with the segment name and corresponding data of the segment fields. The segment name is stored in the `SEGNAM` field, and the data of the segment fields is stored in the `SDATA` field of table `EDID4`.

![](bbox=[0.147, 0.356, 0.859, 0.667])

**Figure 19-32** Table EDID4

+   - `EDIDS`

The status records of the IDoc are stored in this table and linked to the control and data records using the IDoc number. Table `EDIDS` contains different information about the status record, such as the IDoc status, status code, time and date of status record, and so on, as shown in Figure 19.33.