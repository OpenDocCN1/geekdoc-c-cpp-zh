# Display 5.13 Generating scatter plots of log₁₀(brain weight) versus log₁₀ (body weight) with different fits

```
data mreexample;
* Lunneborg (1994) - body weight brain example;
input species $ bodywt brainwt @@;

logbody = log10(bodywt);      * transform the body and brain weights;
logbrain = log10(brainwt);

idino = 0;                    * define the indicator of dinosaurs;
if (species="diplodoc" or species="tricerat" or species="brachios") then
    idino=1;
idino bod = idino*logbody;

datalines;
beaver      1.35   8.1     cow      465.   423.    wolf      36.33  119.5
goat        27.66  115.    guipig   1.04   5.5    diplodocus 11700. 50.
asielephant 2547.  4603.   donkey   187.1  419.   horse     521.   655.
potormonkey 10.    115.    cat      3.30   25.6   giraffe   529.   680.
gorilla     207.   406.    human    62.    1320.  afrelephant 6654. 5712.
triceratops 9400.  70.     rhemonkey 6.8   179.   kangaroo   35.    56.
hamster     0.12   1.      mouse    0.023  0.4    rabbit    2.5    12.1
sheep       55.50  175.    jaguar   100.   157.   chimp     52.16  440.
brachiosaurus 87000. 154.5  rat      0.28   1.9    mole      0.122  3.
pig         192.0  180
;
run;

data mreexample2;
set mreexample;
same_int_fit = 1.10958 + 0.49599*logbody;
reg_fit = 0.93879 + 0.74855*logbody-2.26674*idino;
run;

proc format;
value dinof 0="Mammal"
            1="Dinosaur";
run;

ods listing image dpi=300;
ods graphics on / reset=all width=4.5in;
proc sgplot data=mreexample2;  * same intercept fit;
scatter x=logbody y=logbrain / group=idino;
series x=logbody y=same_int_fit;
format idino dinof.;
run;

proc sgplot data=mreexample2;  * different intercept fit;
scatter x=logbody y=logbrain / group=idino;
series x=logbody y=reg_fit / group=idino;
format idino dinof.;
run;

proc glm data=mreexample;
class idino;
model logbrain = idino logbody;
format idino dinof.;
run;
```