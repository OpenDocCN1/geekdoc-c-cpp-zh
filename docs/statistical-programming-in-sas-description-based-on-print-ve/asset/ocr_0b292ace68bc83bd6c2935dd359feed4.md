# Display 10.18 (continued)

```
data _null_;
    set test;
    by brood;
    if first.brood then do;
        i+1;
        ii = left(put(i,2.));
        call symput('mbrood'||ii,trim(left(brood)));
        call symput('mtotal',ii);
    /*
    Alternative with symputx
        call symputx('mbrood'||ii, brood);
        call symputx('mtotal',ii);
    */
    end;
    run;

    %do ibrood = 1 %to &mtotal;
        proc sgplot data=test;
            where brood=&&mbrood&ibrood;
            reg x=conc y=nyoung / degree=2;

            title "Plot: # Young vs. Nitrofen Conc.";
            title2 "[brood &&mbrood&ibrood]";

            %put 'ibrood' = &ibrood;
            %put '&&mbrood&ibrood' = &&mbrood&ibrood;
        run;
    %end;

    proc sgpanel data=test;
        title "SGPANEL alternative display [avoids macros & looping]";
        panelby brood / columns=3;
        reg x=conc y=nyoung / degree=2;

    run;
    %mend;

    ODS RTF bodytitle file="C:\Users\baileraj.IT\Desktop\fig-10-18.rtf";
    %threeregs()
    quit;
    ODS RTF close;
```