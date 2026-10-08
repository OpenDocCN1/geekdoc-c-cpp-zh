```
end;
if Score ge 7 then output passed;
else output failed;
run;

title 'Passed';\proc print data=passed;
run;
title;

title 'Failed';
proc print data=failed;
run;
title;
```

# Solutions to Student Activities (Polls/Quizzes)

#  7.01 Short Answer Poll – Correct Answer

What are the final values of the variables after the following DO statements execute? The final values are highlighted.

| do i=1 to 5; |
| end; |
| 1 2 3 4 5 6 |
| do j=2 to 8 by 2; |
| ... |
| end; |
| 2 4 6 8 10 |
| do k=10 to 2 by -2; |
| ... |
| end; |
| 10 8 6 4 2 0 |