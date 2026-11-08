
```sas
data drugEvents(keep=subject medstdt drug aestdt aedesc sev);
  * define a hash table to hold the subject counter;
  declare hash subjcnt(ordered:'y'); ❶
    subjcnt.definekey('subject');
    subjcnt.definedata('counter');
    subjcnt.definedone();

  declare hash meds(ordered:'y');
    meds.definekey ('subject', 'counter');
    meds.definedata('subject', 'medstdt','drug','counter');
    meds.definedone ();

  * Load the medication data into the hash object;
  do until(almed);
    set advrpt.commed(keep=subject medstdt drug) end=almed; ❷
    * Check subject counter: initialize if not found,
      otherwise increment;
    if subjcnt.find() then counter=1; ❸
    else counter+1; ❹
    * update the subject counter hash table;
    rc=subjcnt.replace(); ❺
    * Use the counter to add this row to the meds hash table;
    rc=meds.add(); ❻
  end;

  do until(alae);
    .... the remainder of the DATA step is unchanged from the previous example ....
```

The hash table SUBJCNT contains the number of medications that have been read for each patient at any given time. As additional medications are encountered, the COUNTER variable is incremented.

- ❶ A hash table to hold the counter for each patient (SUBJECT) is declared. The key variable is SUBJECT and the only data variable is COUNTER.
- ❷ An observation is read from the medications data set. This loads a value of SUBJECT into the PDV.
- ❸ The COUNTER is initialized to 1 when this value of SUBJECT has not yet been loaded into the SUBJCNT hash table. Remember that a successful FIND will return a 0 value. This means that the expression SUBJCNT.FIND() will be true when the current value of SUBJECT is the first time that subject has been encountered. When SUBJCNT.FIND() successfully returns a value (this is not the first time this SUBJECT has been read from the medications data set), the expression evaluates to false and the COUNTER is incremented ❹. **Either way the SUBJCNT.FIND() has been executed.**
- ❹ When this value of SUBJECT is found in the hash table, the COUNTER is returned and loaded into the PDV. This SUM statement then causes COUNTER to be incremented.
- ❺ The updated COUNTER value is written to the hash table. The REPLACE method causes this value of COUNTER to overwrite a previous value.
- ❻ The medication information along with the updated value of COUNTER is saved.

```sas
data _null_;
  if 0 then set advrpt.demog(keep=clinnum subject lname fname dob); ❶
  * Hash ALL object to hold all the data;
  declare hash all (dataset:'advrpt.demog', ordered:'Y');
    all.definekey ('clinnum','subject');
    all.definedata ('clinnum','subject','lname','fname','dob');
    all.definedone();
  declare hiter hall('all');

  * CLIN object holds one clinic at a time;
  declare hash clin; ❷

  * define the hash for the first clinic; ❸
  clin = _new_ hash(ordered:'Y');
    clin.definekey('clinnum','subject');
    clin.definedata('clinnum','subject','lname','fname','dob');
    clin.definedone();

  * Read the first item from the full list;
  done=hall.first(); ❹
  lastclin = clinnum;

  do until(done);  *loop across all clinics;
    clin.add(); ❺
    done = hall.next(); ❻
    if clinnum ne lastclin then do;
      * This is the first obs for this clinic or the very last obs;
      * write out the data for the previous clinic;
      clin.output(dataset:'clin'||lastclin); ❽
      * Delete the CLIN hash object;
      clin.delete(); ❾
      clin = _new_ hash(ordered:'Y');
        clin.definekey('clinnum','subject');
        clin.definedata('clinnum','subject','lname','fname','dob');
        clin.definedone();
      lastclin=clinnum; ❿
    end;
  end;
  stop;
  run;
```

- ❶ During the compilation phase of the DATA step, the SET statement is used to establish the attributes for the variables on the PDV. These attributes will be used to build the data sets that are written by the OUTPUT method ❽.
- ❷ Declare the CLIN hash object, which will hold the data for one clinic at a time.
- ❸ Instantiate the hash object, CLIN, which was declared earlier ❷. This object will hold the data for each individual clinic. Each clinic will be loaded into the CLIN object one at a time ❺.
- ❹ Using the iterator object for the ALL object, HALL, retrieve the very first item (set of values) from the hash. Save this clinic number in the LASTCLIN variable for comparison with later values. This value is used to detect when we cross clinic boundaries ❼.
- ❺ The current values on the PDV are written to the CLIN object. For the very first item retrieved from the HALL object these values were read by the FIRST method ❹; otherwise, the values were read by the NEXT method ❻ in the previous pass of this DO UNTIL (DONE) loop.

- 1. Unlike the END= option on the SET statement, which is assigned a true value when processing the last observation, the NEXT method returns a 0 until it attempts to read past the last item. This means that DONE is not true on the last observation that will be read out of the HALL object. One more pass of this loop will be required. We take advantage of this behavior to write out the contents of CLIN for the last clinic number.
- 2. When the clinic number that was just retrieved is different from the previous one (or when we are done reading items), we know that it is time to write out the contents of the CLIN object to a data set. The values in the PDV which were just loaded by the NEXT method contain items from a different clinic, but they have yet to be loaded into the CLIN object.
- 3. The OUTPUT method is used to write the contents of the CLIN object, which contains the rows for only one clinic, to the named SAS data set. The data set name contains the value of the clinic number that is stored in the data set, and the name of the data set is determined during the execution of the statement.
- 4. We have written out the contents of the clinic-specific hash object (CLIN) ❸ so we are finished using it. In this example we will delete CLIN and then reestablish it for the next clinic. Since we have already declared CLIN ❷, it can be re-created using the _NEW_ keyword on the assignment statement. Rather than deleting and then reestablishing the CLIN object, we could have cleared it by using the CLEAR method. `rc=clin.clear();` (see the sample programs associated with this section for the full DATA step).
- 5. The current clinic number is saved for comparison ❼ against the next retrieved item ❻. If this is the very last item (DONE=1), this is unnecessary, but costs us little.

## MORE INFORMATION

The example in Section 3.3.6 also creates multiple data subsets using nested hash objects.

## SEE ALSO

Hamilton (2007) discusses this topic in very nice detail, including background and alternate approaches.

### 3.3.6 Hash Tables That Reference Hash Tables

The value of the variable that names a hash table holds information that is unique to that table.

```sas
hashnum = _new_ hash(ordered:'Y');
```

The assignment statement shown to the left instantiates the hash table HASHNUM, and when it is executed a unique value associated with this object is stored in the variable HASHNUM. While this variable exists on the PDV, it is not a variable in the traditional DATA step numeric/character sense—in a real sense the value held by this variable is the whole hash object. This implies that we can instantiate multiple hash tables using the same name as long as the value of the hash table variable changes.

The example in Section 3.3.5 used two independent hash tables to break up one data set into multiple data-dependent data tables—one table for each clinic. That solution loads the data for a specific clinic into a hash table from a master hash table. Once loaded, the data subset is written to a data set and the associated hash table is deleted or cleared. This process requires that each observation has three I/O passes.

- 1. It is read from the incoming data set and loaded into the master hash table.
- 2. The data for a given clinic is read from the master and loaded into a hash table containing data only for that clinic.
- 3. The data are written to the new clinic-specific data set using the OUTPUT method.
