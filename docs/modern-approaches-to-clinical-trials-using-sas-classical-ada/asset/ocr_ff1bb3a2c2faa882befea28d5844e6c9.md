```
run;
data deg;
 do i=1 to eval(&nlevel.-1);
  degree="deg. || trim(left(i));
  output deg;
end;
run;
```

```
proc incl;
start;
  use &fich_in;
  read all var(dose) into x;
  use niv;
  read all var(level) into labco;
  use deg;
  read all var(degree) into labco;
  degmax=row(x)-1;
  p=orpol(x,degmax);
  pp=p(2:ncol(p));
  create poly from p [rowname=labco colname=labco];
  append from pp [rowname=labro];
finish;
run;
quit;
```

titel "Orthogonal polynomial coefficient contrasts"
title2 "--------------------------------------"
title3 ""
proc print data=poly noobs label;
labro="Polynomial degree";
run;
%end polyorth;

```
data pol;
input dose @@;
cards;
0 2.5 5 12.5 25 75;
run;
%polyorth(&fich_in=pol);
```

Figure 6.4 Output for Example Code 6.1

| degree | level_1 | level_2 | level_3 | level_4 | level_5 | level_6 |
|---|---|---|---|---|---|---||
| deg 1 | -0.3146 | -0.2751 | -0.2367 | -0.1983 | -0.1569 | -0.1158 |
| deg 2 | 0.4238 | 0.2543 | 0.0969 | -0.0571 | 0.1347 | 0.2687 |
| deg 3 | -0.4928 | -0.0175 | 0.3227 | 0.6425 | 0.4893 | 0.0309 |
| deg 4 | 0.4936 | -0.3451 | 0.5438 | 0.5468 | -0.1348 | -0.0223 |
| deg 5 | -0.2635 | 0.7572 | -0.5819 | 0.1040 | -0.0109 | 0.0006 |

Figure 6.4 Output for Example Code 6.1 provides the contrast coefficients for the different degrees of a polynomial regression that would be adjusted between the doses and the response:

$y = \alpha + \beta x + \gamma x^2 + \iota x^4 + \eta x^5$