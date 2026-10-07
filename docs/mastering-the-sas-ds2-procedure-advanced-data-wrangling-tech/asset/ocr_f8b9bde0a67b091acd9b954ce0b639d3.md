SAS Log:

```
ERROR: Compilation error.
ERROR: Parse encountered SET when expecting end of input.
ERROR: Line n: Parse failed; >>> set crs.one_day;
```

Enclosing the executable statements in a method resolves the issue:

```
proc ds2;
data _null_;
  method run()
    set crs.one_day;
    put _all_;
  end;
enddata;
run;
quit;
```

SAS Log:

```
NOTE: Execution succeeded. 6 rows affected.
```

# 3.2.2.2 DS2 Programs Do Not Overwrite Data by Default

If you submit this program, it runs normally. If you submit the exact same program a second time, it results in a syntax error:

```
proc ds2;
data test1 test2;
  method run()
    set crs.one_day;
  end;
enddata;
run;

proc ds2;
data test1 test2;
  method run()
    set crs.one_day;
  end;
enddata;
run;
```

SAS Log:

```
683 proc ds2;
684 data test1 test2;
685 method run();
686 set crs.one_day;
687 end;
688 enddata;
689 run;
690 NOTE: Execution succeeded. 12 rows affected.
691 quit;
692 NOTE: PROCEDURE DS2 used (Total process time):
```