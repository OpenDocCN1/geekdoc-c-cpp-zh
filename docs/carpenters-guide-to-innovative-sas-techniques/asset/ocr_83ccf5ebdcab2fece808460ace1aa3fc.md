```
```sas
data _null_;
  if 0 then set advprt.demog(keep=clinnum subject lname fname dob); ❶
  * Hash ALL object to hold all the data;
  declare hash all (dataset:'advprt.demog', ordered:'Y');
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
  stop;
  run;
```
```

❶ During the compilation phase of the DATA step, the SET statement is used to establish the attributes for the variables on the PDV. These attributes will be used to build the data sets that are written by the OUTPUT method ❽.

❷ Declare the CLIN hash object, which will hold the data for one clinic at a time.

❸ Instantiate the hash object, CLIN, which was declared earlier ❷. This object will hold the data for each individual clinic. Each clinic will be loaded into the CLIN object one at a time ❺.

❹ Using the iterator object for the ALL object, HALL, retrieve the very first item (set of values) from the hash. Save this clinic number in the LASTCLIN variable for comparison with later values. This value is used to detect when we cross clinic boundaries ❼.

❺ The current values on the PDV are written to the CLIN object. For the very first item retrieved from the HALL object these values were read by the FIRST method ❹; otherwise, the values were read by the NEXT method ❻ in the previous pass of this DO UNTIL (DONE) loop.