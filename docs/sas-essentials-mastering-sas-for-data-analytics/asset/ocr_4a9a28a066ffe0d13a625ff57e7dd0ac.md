# APPENDIX B: SAS® FUNCTION REFERENCE

| TABLE B.9 Special Use Functions |
| Function | Description |
| --- | --- |
| IRR (period, cash0, cash1, ...) MORT (amount, payment, rate, number) | Returns the internal rate of return as a percentage When you set the PAYMENT variable to missing. returns this payment for a loan calculation. For example, when you run DPAYMENT. SAS DATA LOAN;
PAYMENT=
MORT(30000,.,.06/12/48);
RUN;
PROC PRINT;RUN;
the of the (monthly) PAYMENT is 70.55 |
| NPV (rate, period, cash0, cash1, ...) | Returns the net present value expressed as a percentage |

# HANDS-ON EXAMPLE

+   1. Open the program file FUNC_MORT.SAS. This program uses the MORT function to calculate the payments for a loan. This example displays payment for different loan, interest, and number of payments. Run the program and observe the results in Table B.10.
DATA LOAN;
FORMAT VALUE DOLLAR12.
INTR1-INTRATE3 4.2
NUMBER 4;
INPUT INTRATE1-INTRATE3 NUMBER;
ARRAY INT (3) INTRATE1-INTRATE3;
ARRAY PAY (3);
DO I=1 to 3;
PAY(I) = MORT(VALUE,,,(I)/12,NUMBER);
END;
LABEL MORT="Mortage Payment"
LABEL INTRATE1="Int. Rate 1"
LABEL INTRATE2="Int. Rate 2"
LABEL INTRATE3="Int. Rate 3"
LABEL PAYMENT="Amount of Payment"
LABEL VALUE="Loan Amount"
LABEL NUMBER="Num. Payments";nDROP I;
DATALINES;
100000 .05 .04 .03 360
100000 .05 .04 .03 180
150000 .05 .04 .03 360
150000 .05 .04 .03 180
;
RUN;
PROC PRINT LABEL DATA=LOAN ;
RUN;