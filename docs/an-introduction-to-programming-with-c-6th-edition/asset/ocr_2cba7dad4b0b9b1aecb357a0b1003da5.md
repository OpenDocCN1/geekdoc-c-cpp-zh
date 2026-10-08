# APPENDIX A Answers to Mini-Quizzes and Labs

```
{
//calculates and returns a monthly payment
double monthPay = 0.0;
monthPay = prin * monthRate /
  (1 - pow(monthRate + 1, -months));
return monthPay;
} //end of getPayment function
```

# LAB 9-4 Desk-Check

Desk-check:

| balance | amount | transaction | another |
| --- | --- | --- | --- |
| 2000.0 | 400.0 | W | ✗ |
| 1000.0 | 1000.0 | W | D |
| 2500.0 | 45.0 | D | D |
| 2755.0 | 55.0 | D | D |
| 2700.0 | 150.0 | W | D |
| 2550.0 | 15.0 | D | D |
| 2565.0 | 1050.0 | W | n |
| 1515.0 | | | |

| bal | type | amt | curBalance |
| --- | --- | --- | --- |
| 2000.0 | W | 400.0 | 1600.0 |
| 1600.0 | D | 1200.0 | 2800.0 |
| 2500.0 | W | 45.0 | 2755.0 |
| 2755.0 | W | 55.0 | 2700.0 |
| 2700.0 | W | 150.0 | 2550.0 |
| 2550.0 | D | 15.0 | 2565.0 |
| 2565.0 | W | 1050.0 | 1515.0 |

The code will display a current balance of $1515.00.