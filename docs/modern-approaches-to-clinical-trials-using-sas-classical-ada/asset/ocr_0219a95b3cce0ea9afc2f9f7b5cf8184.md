4. p2: probability that a control outcome is simultaneously less than two independent treatment outcomes

5. p3: probability that a treatment outcome is simultaneously greater than two independent control outcomes.

Example Code 11.1 MSPower for Computing Required Sample Size

```
%macro MSPower(beta, p1, p2, p3, alpha);
  data result;
    delta=1-(alpha/2);
    za=quantile('Normal', delta);
    p1=&p1; p2=&p2; p3=&p3;alpha=&alpha;
    do i = 1 to 10000;
      nsize=i;
      denom=(i**2)*(p1*(1-p1) + (i-1)*(p2 + p3) - 2*(p1**2));
      den=sqrt(denom);
      a=0.5+(i**2) + za*sqrt((i**2)*(2*i + 1)/12) - 0.5 - (i**2)*p1)/den
      beta=CDF('Normal', a);
      power=1-beta;
      output;
      if beta<=&beta then i=10000;
    end;
  end;
run;

data result2;
  set result end = __;
  end=end;
  end;
  if beta>&beta then do;
    warning=1;
    nsize2=\>10000";n  end;
  else do;
    nsize2=compress(nsize);
  end;
  label nsize2='sample size';
run;

proc format;
  value wa='required sample size greater than 10000';
run;

proc noobs label;
  var nsize2 p1 p2 p3 alpha beta power warning;
  format warning wa.;
run;
%mend MSPower;

%MSPower(0.2, 0.7, 0.6, 0.4, 0.05);
```

The results of the macro call are shown in Output from Example Code 11.1. This indicates the smallest sample size that provides 80% power for rejecting the null hypothesis is 23 patients per treatment arm. The actual power by a total sample size of 46 patients is 82%.

Table 11.3 Output from Example Code 11.1