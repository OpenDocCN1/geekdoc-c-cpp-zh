```
int funcininput() {
    int flag = 1;

    scanf(inptr, "%f %f", &diameter, &velocity);
    if(diameter <= 0 || velocity <= 0)
        flag = 0;
    return flag;
}
```

```
/************************************************************************************/
/* funoutput: Output the Data */
/************************************************************************************/
/* Output Variables: */
/*    diameter - diameter of pipe in feet */
/*    velocity - velocity of water in feet per sec */
/*    flowrate - flow rate in cubic feet per sec */
/************************************************************************************/
```

FILE: progb.c

```
/************************************************************************************/
/* funcompute: Computes the Flow Rate */
/************************************************************************************/
/* Constant: */
```