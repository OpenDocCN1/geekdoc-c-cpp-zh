# Chapter 10. Functions

10.15 Write a function `rc_time_constant()` that computes the time constant $\tau$ of an RC circuit given resistance $R$ (in ohms) and capacitance $C$ (in farads). Use the formula:

$	au = R 	imes C$

Test it using the following main() function:

```
int main() {
    double R = 1000; // 1 kiloohm
    double C = 0.000001; // 1 microFarad
    printf("Time constant: %lf\n", rc_time_constant(R, C));
    return 0;
}
```

10.16 Write a function `voltage_divider()` that computes the output voltage of a voltage divider circuit given input voltage $V_{in}$, resistor $R1$, and resistor $R2$ using the formula:

$V_{out} = V_{in} 	imes rac{R_2}{R_1 + R_2}$

Test it using the following main() function:

```
int main() {
    double Vin = 12.0; // 12V input
    double R1 = 1000; // 1 kiloohm
    double R2 = 2000; // 2 kiloohm
    printf("Output Voltage: %lf\n", voltage_divider(Vin, R1, R2));
    return 0;
}
```

10.17 Write a function to compute:

$\cos \omega t = \frac{e^{j\omega t} + e^{-j\omega t}}{2}$

10.18 The following function is supposed to return the RMS (Root Mean Square) of an array of voltage readings but sometimes produces incorrect results. Find and fix the issue.

```
#include <stdio.h>
#include <math.h>

double rms(int arr[], int size) {
    double sum = 0;
    for (int i = 0; i < size; i++) {
        sum += arr[i] * arr[i];
    }
    return sqrt(sum / size); // Possible issue?
}
```