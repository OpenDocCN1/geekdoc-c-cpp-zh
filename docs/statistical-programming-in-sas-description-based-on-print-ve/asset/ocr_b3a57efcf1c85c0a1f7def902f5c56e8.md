The SAS log output contains the following results:

```
MPRINT(TRAP_AREA_Z):  data trapper;
MPRINT(TRAP_AREA_Z):  file "C:\Users\baileraj.IT\Desktop\est3.out" MOD;
MPRINT(TRAP_AREA_Z):  retain trapsum 0;
MPRINT(TRAP_AREA_Z):  array x_value(5) x1-x5;
MPRINT(TRAP_AREA_Z):  array f_value(5) y1-y5;
MPRINT(TRAP_AREA_Z):  low = 0;
MPRINT(TRAP_AREA_Z):  high = 1.96;
MPRINT(TRAP_AREA_Z):  incr = (high-low)/( 5 -1);
MPRINT(TRAP_AREA_Z):  pi = arcos(-1);
MPRINT(TRAP_AREA_Z):  do i= 1 to 5;
MPRINT(TRAP_AREA_Z):  x_value[i] = low + incr*(i-1);
MPRINT(TRAP_AREA_Z):  f_value[i] = (1/sqrt(2*pi))*exp(-x_value[i]*x_value[i]/2);
MPRINT(TRAP_AREA_Z):  if i=1 or i=5 then trapsum = trapsum + f_value[i]/2;
MPRINT(TRAP_AREA_Z):  else trapsum = trapsum + f_value[i];
MPRINT(TRAP_AREA_Z):  end;
```

The values of the macro variables are substituted (e.g., 5 for &npts, 0 for &low, 1.96 for &high, etc.). These are the SAS statements that will be executed.

# Display 10.15 SAS log output produced by the MPRINT option

```
MPRINT(TRAP_AREA_Z):  data trapper;
MPRINT(TRAP_AREA_Z):  file "C:\Users\baileraj.IT\Desktop\est3.out" MOD;
MPRINT(TRAP_AREA_Z):  trapsum = 0;
MPRINT(TRAP_AREA_Z):  array x_value(5) x1-x5;
MPRINT(TRAP_AREA_Z):  array f_value(5) y1-y5;
MPRINT(TRAP_AREA_Z):  low = 0;
MPRINT(TRAP_AREA_Z):  high = 1.96;
MPRINT(TRAP_AREA_Z):  incr = (high-low)/( 5 -1);
MPRINT(TRAP_AREA_Z):  pi = arcos(-1);
MPRINT(TRAP_AREA_Z):  do i= 1 to 5;
MPRINT(TRAP_AREA_Z):  x_value[i] = low + incr*(i-1);
MPRINT(TRAP_AREA_Z):  f_value[i] = (1/sqrt(2*pi))*exp(-x_value[i]*x_value[i]/2);
MPRINT(TRAP_AREA_Z):  if i=1 or i=5 then trapsum = trapsum + f_value[i]/2;
MPRINT(TRAP_AREA_Z):  else trapsum = trapsum + f_value[i];
MPRINT(TRAP_AREA_Z):  end;
MPRINT(TRAP_AREA_Z):  output;
MPRINT(TRAP_AREA_Z):  put "est. P(0 < Z < 1.96) =" area_est "(based on 5 points)";
MPRINT(TRAP_AREA_Z):  run;
```