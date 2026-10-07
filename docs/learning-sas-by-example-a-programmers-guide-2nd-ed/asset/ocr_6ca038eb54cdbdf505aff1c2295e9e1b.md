```
x = 10; y = 20; z = -30;
AbsZ = abs(z);
ExpX = round(exp(x),.001);
Circumference = round(2*constant('pi')*y,.001);
put _all_;
run;
*11-9;
data fake;
do Subj = 1 to 100;
  if rand('uniform') le .4 then Gender = 'Female';
  else Gender = 'Male';
  Age = 9 + ceil(rand('uniform')*51);
  output;
end;
run;
title "Frequencies";nproc freq freq data=fake;
tables Gender / nocum
run;
title "First 10 Observations of FAKE";
proc print data=fake(obs=10);
run;
*11-11;
data convert;
set learn.char_num(rename=
(Age = Char Age
Weight = Char_Weight
SS = Num_SS));
Age = input(Char_Age,8);
Weight = input(Char_Weight,8);
SS = put(Num_SS,ssn1);
Zip = put(Num_Zip,z5);
drop Char_:Num_;
run;
title "Listing of CONVERT";
proc print data=convert noobs;
run;
*11-13;
data smooth;
set learn.stocks;
Price1 = lag(Price);
Price2 = lag2(Price);
Average = mean(Price, Price1, Price2);
run;
title "Plot of Price and Moving Average";
proc sgplot data=smooth;
series x=Date y=Price;
series x=Date y=Average;
run;
```