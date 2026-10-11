
```c
#include <stdio.h>

float funcforce(float, float, float);
float functhrust(float, float, float);

int main( ) {
    float weight, velocity, time;
    float force, thrust;

    printf("INPUT DATA\n");
    scanf("%f %f %f", &weight, &velocity, &time);

    printf("\nOUTPUT DATA\n");
    printf("Weight = %7.2f\n", weight);
    printf("Velocity = %7.2f\n", velocity);
    printf("Time = %5.2f\n", time);

    force = funcforce(weight, velocity, time);
    thrust = functhrust(weight, force);

    printf("Force due to acceleration = %8.2f\n", force);
    printf("Total thrust due to acceleration = %8.2f\n", thrust);

    return 0;
}
```

```c
********************************************************************************************************************
/*                                                              */
/*   Function to Compute the Force on the Rocket                    */
/*********************************************************************************************************************
/*                                                              */
/*   Constants:                                                              */
/*                                                              */
/*   G = 32.2 ft/sec² - gravitational acceleration                  */
/*                                                              */
/*   Input Parameters:                                                           */
/*   weight1 - weight of the rocket (pounds)                         */
/*   velocity1 - velocity of the rocket (feet/second)               */
/* timel - duration of the thrust (seconds) */
/* Return Variable: */
/* force - force of the rocket motor */
/* ******************************************************************/
```

```c
float funcforce(float weight1, float velocity1, float timel)
{
  const float G = 32.2;
  float force;

  force = (weight1 * velocity1)/( G * timel);

  return force;
}
```

```c
/******************************************************************/
/* Function to Compute the Thrust on the Rocket */
/******************************************************************/
/* Input Parameters: */
/*  weight1 - weight of the rocket (pounds) */
/*  forcel - force on the rocket (pounds) */
/* Return Variable: */
/*  thrust1 - thrust on the rocket motor */
/******************************************************************/
```

```c
float functhrust(float weight1, float forcel)
{
  float thrust1;

  thrust1 = weight1 + forcel;

  return thrust1;
}
```

### 5.6.2 串联电流

问题 编写一个程序计算具有三个电阻的交流电路中的电流，然后计算每个电阻两端的电压降。

方法 输入电压 `V` 和电阻 `R1`, `R2`, `R3`。计算有效电阻，然后计算每个电阻两端的电压降。

有效电阻 `R = R1 + R2 + R3` (欧姆)

电流 `I = V / R` (安培)

`R1` 上的电压降 `V1 = IR1`

`R2` 上的电压降 `V2 = IR2`

`R3` 上的电压降 `V3 = IR3`

伪代码

```
main: program
input voltage v, resistances r1, r2, r3
funccurrent()
funcvoltdrop()
funcvoltdrop()
funcvoltdrop()
funcoutput()
stop
function: funccurrent
calculate the effective resistance

r <- r1 + r2 + r3

calculate the current

i <- v / r

end funccurrent

function: funcvoltdrop
calculate voltage drop across a resistance

v <- i * r

end funcvoltdrop
```

```c
function: funcoutput
print the current in the circuit
print the voltage drops across each resistance
print the total voltage drop in the circuit
end funcoutput
```

```c
/*****************************************************************/
/*
/* Compute the Current and Voltage Drop in an */
/* AC Series Circuit */
/*
/******************************************************************/
/*
/* Input Variables: */
/*/* voltage - voltage of circuit (volts) */
/* res1, res2, res3 - resistances in series(ohms) */
/*
/* Computed variables: */
/* current - current in the circuit */
/* volt1, volt2, volt3 - voltage drops across */
/* each resistance */
/*
/* Output variables: */
/*
/* current - current in the circuit */
/* volt1, volt2, volt3 - voltage drops across */
/* each resistance */
/*
/* Functions called: */
/*
/* funccurrent - function to compute the' current */
/* funcvoltdrop - function to compute the voltage */
/* drop */
/**/
```

```c
/*
* funcoutput - 输出结果的函数 */
/*
********************************************************************

#include <stdio.h>

float funccurrent(float, float, float, float);
float funcvoltdrop(float, float);
void funcoutput(float, float, float, float, float);

int main() {
    float voltage, res1, res2, res3, current, volt1,
    volt2, volt3;
    printf("INPUT DATA\n");
    scanf("%f %f %f %f", &voltage, &res1, &res2, &res3);
    current = funccurrent(voltage, res1, res2, res3);
    volt1 = funcvoltdrop(current, res1);
    volt2 = funcvoltdrop(current, res2);
    volt3 = funcvoltdrop(current, res3);

    funcoutput(current,volt1, volt2, volt3);
    volt1 + volt2 + volt3;

    return 0;
}

********************************************************************
/*
* 计算电路中电流的函数 */
/*
********************************************************************
/*
* 输入参数： */
/** voltagel - 电路中的电压 v */
/** res1 - 电路中的电阻 r1 */
/** res2 - 电路中的电阻 r2 */
/** res3 - 电路中的电阻 r3 */
/*
/** 局部变量： */
/** totres - 电路的总电阻 */
/** circurrent - 电路中的电流 */
/*
```

## 326 模块化设计与函数

```c
/*
* 调用者：
*
* main
*/
/*
* 返回变量：
*
* current - 电路中的电流
*/
********************************************************************
```

```c
float funccurrent(float voltage1, float res11,
       float res22, float res33)
{
    float totres, current;

    totres = res11 + res22 + res33;
    current = voltage1 / totres;

    return current;
}
```

```c
****************************************************************
/*
* 计算电阻两上的电压降
*/
****************************************************************
/*
* 输入参数：
* currentl1 - 电路中的电流
* res       - 电路中的电阻
*/
/*
* 输出参数：
* 无
*/
/*
* 局部变量：
* volt - 电阻上的电压降
*/
/*
* 调用者：
* main
*/
/*
* 返回变量：
* volt - 电阻上的电压降
*/
****************************************************************
```

```c
float funcvoltdrop(float current1, float res)
{
    float volt;
    volt = current1 * res;

    return volt;
}
```

```c
****************************************************************
/* *
/*
* 输出结果的函数 */
/* *
****************************************************************
/* *
/* 输入参数： */
/* current1 - 电路中的电流 */
/* volt11 - 电阻 r1 上的电压降 */
/* volt22 - 电阻 r2 上的电压降 */
/* volt33 - 电阻 r3 上的电压降 */
/* totvolt - 电路总电压降 */
/* */
/* 调用者： */
/* main */
/* *
/* 返回变量： */
/* 无 */
/* *
****************************************************************
```

```c
void funcoutput(float current1, float volt11,float volt22,
    float volt33,float totvolt)
{
    printf("\nOUTPUT DATA\n");
    printf("Current in the circuit = %4.2f\n", current1);
    printf("Voltage drop across resistance r1 = %6.2f\n",
        volt11);
    printf("Voltage drop across resistance r2 = %6.2f\n",
        volt22);
    printf("Voltage drop across resistance r3 = %6.2f\n",
        volt33);
    printf(" Total voltage drop across circuit = %6.2f\n",
        totvolt);
}
```

## 输入与输出

输入数据

`200. 50. 150.`

输出数据

电路中的电流 = `0.67`

电阻 `r1` 上的电压降 = `33.33`

电阻 `r2` 上的电压降 = `66.67`

电阻 `r3` 上的电压降 = `100.00`

电路总电压降 = `200.00`

该程序包含一个 `main` 函数和三个子函数。`main` 调用这些子函数。输入数据在 `main` 中处理。`functioncurrent` 计算电路中的电流，并通过 `return` 语句将计算结果返回给 `main` 函数。`voltagedrop` 逐计算每个电阻的电压降，并通过 `return` 语句将每个电压降返回给 `main` 函数。`functionoutput` 打印 `voltdrop` 计算的结果及其和。

### 5.6.3 平方函数

问题 写一个平方根函数，该函数在传入负参数时返回一个错误标志。编写一个主程序来测试该函数。此示例演示了值传递、指针传递以及状态标志的返回。

方法 使用牛顿-拉夫逊法计算平方根。如果参数为负，函数将返回一个标志。该算法见第 1 章第 1.6.3 节。

数据输入一个需要计算平方根的实数。

伪代码

```
main 函数：
输入数量
对于每个输入数字
调用函数：numsqrt()
如果它有平方根
    输出数字、平方根
else
    打印数字和信息：“没有实数平方根”
结束循环
停止
```

```c
function numsqrt:
计算 num 的平方根
if num < 0
    通过返回错误标志来信号错误
else if num == 0
    平方根为 0
else
    x0 <- x
    x1 <- x / 2.0
    do while |x0 - x1| > 0.0001
        x0 <- x1
        x1 <- (x0 + x/x0) / 2.0
    end do
平方根 = x1

return 成功标志;
numsqrt
```

# 程序
