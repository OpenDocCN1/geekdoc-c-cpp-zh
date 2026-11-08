```
```sas
33    proc options option=sasautos;
         run;

      SAS (r) Proprietary Software Release 9.2  TS2M2

      SASAUTOS=      Search list for autocall macros
NOTE: PROCEDURE OPTIONS used (Total process time):
      real time                 0.00 seconds
      cpu time                  0.00 seconds

35    proc opload data=advrpt.current_settings
         (where=(optnam='SASAUTOS'));
36       run;

NOTE: PROCEDURE OPLOAD used (Total process time):
      real time                 0.12 seconds
      cpu time                  0.01 seconds

37    proc options option=sasautos;
         run;

      SAS (r) Proprietary Software Release 9.2  TS2M2

      SASAUTOS=(advmac, sasautos)
                     Search list for autocall macros
NOTE: PROCEDURE OPTIONS used (Total process time):
      real time                 0.00 seconds
      cpu time                  0.00 seconds
```
```

**PROC OPTIONS** is used to view the current setting of the SASAUTOS option.

Here we have recovered the setting of a single option. If the WHERE clause had not been used in the option settings in the data set `ADVRPT.CURRENT_SETTINGS` would have been used.

# Using the DMOPTSAVE and DMOPTLOAD Commands

The DMOPTSAVE and DMOPTLOAD commands are similar to the PROC steps described above. As commands they are designed to be executed from within the DM command line in the Display Manager, but this also means that they can either be assigned a key in the KEYS window (see Section 14.4.7), or that they can be executed from within the DM statement. Since the DM statement is generally the most flexible, the code is shown here.

```
```sas
dm 'dmoptsave advrpt.current_settings';
options sasautos=adv2;
proc options option=sasautos;
   run;
dm "dmoptload advrpt.current_settings
            (where=(optnam='SASAUTOS'))";
   run;
proc options option=sasautos;
   run;
```
```

**The current system option settings are saved using the DMOPTSAVE command.**

**The SASAUTOS option is accidentally changed.**

**The new SASAUTOS option value is ready to be used.** All we do here is demonstrate that it has been changed.

The *original* value for the SASAUTOS option is restored.

# MORE INFORMATION

The DM statement is also discussed in Section 14.4.2.