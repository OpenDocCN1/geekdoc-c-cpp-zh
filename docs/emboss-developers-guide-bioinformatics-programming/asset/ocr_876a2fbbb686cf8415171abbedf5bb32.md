```
AjPSeqset alignfile = NULL;
AjPFile prior = NULL;
AjPFile null = NULL;
AjPFile pam = NULL;
float pamwgt = 0.0;
AjPStr n = NULL;
AjPStr *strategy = NULL;
ajint pbswitch = 0;
float archpri = 0.0;
AjBool binary = ajFalse;
AjBool fast = ajFalse;
float gapmax = 0.0;
AjBool hand = ajFalse;
float idlevel = 0.0;
AjBool noeff = ajFalse;
float swentry = 0.0;
float swexit = 0.0;
AjBool verbosity = ajFalse;
AjPStr *weighting = NULL;
AjPFile hmmfile = NULL;
AjPFile o = NULL;
AjPFile cfile = NULL;

/* Housekeeping variables */
AjPStr cmd = NULL;
AjPStr rnd1 = NULL;
AjPStr rnd2 = NULL;
AjPStr tmp = NULL;
AjPStr fmt = NULL;
char option;
AjBool fmtok = ajFalse;
AjPStr hmmfilename = NULL;
```

# 10.6.2.3 Processing the ACD file

The code below shows the function calls for processing the ACD file. embInitP processes the ACD file and prompts the user for any required values that are not specified on the command line. The prefix ajAcdGet family of functions are used to retrieve values from the ACD data definitions and store them in the variables defined earlier:

```
/* ACD file processing */
embInitP("ehmmbuild",argc,argv,"HMMERNEW");

alignfile = ajAcdGetSeqset("alignfile");
prior = ajAcdGetInfile("prior");
null = ajAcdGetInfile("null");
pam = ajAcdGetInfile("pam");
pamwgt = ajAcdGetFloat("pamwgt");
n = ajAcdGetString("n");
strategy = ajAcdGetList("strategy");
pbswitch = ajAcdGetInt("pbswitch");
archpri = ajAcdGetFloat("archpri");
binary = ajAcdGetBoolean("binary");
fast = ajAcdGetBoolean("fast");
```