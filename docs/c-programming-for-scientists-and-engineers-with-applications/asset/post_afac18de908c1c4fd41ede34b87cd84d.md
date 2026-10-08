
```c
/* height - height the projectile reaches */
/* Output Variables: */
/* initvel - initial velocity of firing ft/sec* */
/* height - height the projectile reaches */
/****************************************************************```

```c
#include <stdio.h>

int main() {
    const float GRAV_ACCEL = 32.2;
    float initvel,height;

    printf("Initial Velocity \tHeight\n\n");
    initvel = 50;
    while(initvel <= 200) {
        height = - (initvel * initvel) / (2.0 * GRAV_ACCEL);
        printf("%6.2f\t%8.2f\n", initvel, -1.0 * height);
        initvel += 50;
    }
    return 0;
}
```

Output

Initial Velocity \tHeight
50.00	38.82
100.00	155.28
150.00	349.38
200.00	621.12
```

## 4.5.3 Shear Stress of a Metallic Member

Problem Write a program to compute and print a table of torsion shear stresses for circular rods having various torsion loads at various offsets. This example demonstrates the use of nested repetitions.

Data

- diameter: 5 and 6 inches
- Load: 1000 and 12,000 pounds
- offset: 10, 15, and 20

![](img/8356e6c3bfe3b10354682c60b1e74b1d_263_0.png)

Method

Let D = diameter of the rod
P = torsion load in pounds
L = offset

The torsion shear stress is given by the formula

```
$T_s = \frac{16PL}{\pi D^3}$
```

Pseudocode

```
For each diameter of the rod
    Output the diameter of the rod
    For each load
        Output the load
        For each offset
            Shear stress ← (16 × Torsion load × Length offset) / (π × diameter × diameter)
            output shear stress
    End for
    End for
End for
Stop
```

# Program

```c
****************************************************************/
/* */
/* Print a Table of Torsion Shear Stress */
/* */
****************************************************************/
/* */ Constants: */
/* */
/* PI = 3.141593 */
/* */
/* Input Variables: */
/* */
/* diameter - diameter of rod */
/* */ torsion_load - torsion load */
/* */ applied (pounds) */
/* */ length_offset - load offset length (inches) */
/* */
/* */ Computed Variables: */
/* */
/* */ shear_stress - shear stress */
/* */ pounds/square inch */
/* */
/* */ Output Variables: */
/* */
/* */ shear_stress - shear stress */
/* */ pounds/square inch */
/* */
****************************************************************/
```

```c
#include <stdio.h>

int main()
{
    const float PI = 3.141593;
    int diameter, torsion_load, length_offset;
    float shear_stress;
    int page = 0;

    for(diameter = 5; diameter < 7; diameter++) {
        page = page + 1;
        printf("%d\n", diameter);
        printf("nTorsion load is: %d\n", torsion_load);
        printf("\n Length Offset %d\n", length_offset);
        printf(" Shear Stress%2f\n", shear_stress);

        /* computation of torsion shear stress */
        for(length_offset = 10; length_offset <= 20; length_offset += 5) {
            shear_stress = (16.0 * torsion_load * length_offset) / (PI * diameter * diameter);
            printf("%d\n", length_offset);
            printf("%8.2f\n", shear_stress);
        }
    }
    return 0;
}
```

Output

# Diameter of Rod: 5

Torsion Load is: 10000

| Length Offset | Torsion Shear Stress |
| :--- | :--- |
| 10 | 4074.37 |
| 15 | 6111.55 |
| 20 | 8148.73 |

Torsion Load is: 12000

| Length Offset | Torsion Shear Stress |
| :--- | :--- |
| 10 | 4889.24 |
| 15 | 7333.86 |
| 20 | 9778.48 |

# Diameter of Rod: 6

Torsion Load is: 10000

| Length Offset | Torsion Shear Stress |
| :--- | :--- |
| 10 | 2357.85 |
| 15 | 3536.78 |
| 20 | 4715.70 |

## 248 Control Structures

Torsion Load is: 12000

| Length Offset | Torsion Shear Stress |
| :--- | :--- |
| 10 | 2829.42 |
| 15 | 4244.13 |
| 20 | 5658.84 |

## 4.5.4 Table of Periods of a Pendulum

Problem Write a program to compute the periods of simple pendulum for arm lengths starting at 12 inches and reaching a period less than or equal to 3.45. This program uses repetition controlled by terminating limit.

Data The arm length L in feet varies from 1 to n.

Method The formula to compute the period is

![](img/8356e6c3bfe3b10354682c60b1e74b1d_267_0.png)

where $g = 32.2$ ft/sec.

$T$ is the period of the pendulum in seconds to be computed. $L$ is the arm length of the pendulum in feet.

Pseudocode

```
L $\leftarrow$ 1
Calculate period
While period $\le$ 3.45
    Calculate period
    Output length and period
    L = L + 1
Stop
```

# Program

```c
****************************************************************/
/* */
/* Print a Table of Pendulum Length and Period */
/* */
****************************************************************/
/* */ Constants: */
/* */
/* PI = 3.141593 */
/* */ GRAVITY = 32.2 ft/sec *
/* */
/* Input variables: */
/* */
/* length - length of pendulum arm (feet) */
/* */
/* Computed Variables: */
/* */
/* period - period of pendulum (seconds) */
/* */ constant - 2PI *
/* */
/* Output Variables: */
/* */
/* period - period of pendulum (seconds)
****************************************************************/
```

```c
#include <stdio.h>
#include <math.h>

int main()
{
    FILE *outptr;
    const float GRAVITY = 32.2;
    const float PI = 3.141593;
    float length, period, constant;

    outptr = fopen("pend.dat", "w");

    constant = 2.0 * PI;
    length = 1.0;
    period = constant * sqrt(length / GRAVITY);
    fprintf(outptr, "OUTPUT\n");
    fprintf(outptr, "length\n");
    fprintf(outptr, "period\n");

    while(period <= 3.45)
    {
        fprintf(outptr, "%2.0f,      %5.2f\n", length, period);
        length += 1.0;
        period = constant * sqrt(length / GRAVITY);
    }
    return 0;
}
```

| Length | period |
| :--- | :--- |
| 1 | 1.11 |
| 2 | 1.57 |
| 3 | 1.92 |
| 4 | 2.21 |
| 5 | 2.48 |
| 6 | 2.71 |
| 7 | 2.93 |
| 8 | 3.13 |
| 9 | 3.32 |

## 4.5.5 Compression Stress and Strain in Steel Rods

Problem Write a program to compute the stress and strain in steel rods of diameters D varying from 2 inches to 5 inches with increments of 1.0 subject to compression load P varying from 50,000 to 100,000 pounds per square inch in increments of 25,000. The modulus of elasticity Es for steel is $30 \times 10^6$ lb/in². This program uses nested iterative loops and writes the output to a file.

Method The compression stress is computed from the formula:

```
$\sigma_c = \frac{P}{area}$
```

Where $\sigma_c$ = compression stress in lb/in²
$P$ = compression load
area = cross-sectional area of steel rods given by the formula

```
$\frac{\pi d^2}{4}$
```

$d$ = the diameter of the steel rod.

The compression strain is computed from the formula:

```
$\varepsilon = \frac{\sigma_c}{Es}$
```

Where $\sigma_c$ = compression stress in lbs/in²
$\varepsilon$ = the strain (nondimensional)
$Es$ = the modulus of elasticity of steel in lb/in²

Data Real values of load of 50,000, 75,000, and 100,000 pounds.
Real values of diameter 2.0, 3.0, 4.0, and 5.0 inches.

Pseudocode

```
For each load
    Output the load with label
    For each diameter
        area <- (3.141593 * d * d) / 4.0
        stress <- p / area
        strain <- stress / Es

        output the diameter, stress, strain
    End for
End for
Stop
```

# Program

```c
****************************************************************/
/* Stress and Strain in Steel Rods under */
/* Compression Loading */
****************************************************************/
/* */ Constants: */
/* */ PI = 3.141593 */
/* */ ES = 30000000 */
/* */ Input variables: */
/* */ load -- compression load (pounds) */
/* */ diameter -- diameter of steel rods(inches) */
/* */ Working Variables: */
/* */ area -- cross sectional area (sq-in) */
/* */
/* Computed Variables: */
/* */ stress - compression stress (lb/in²) */
/* */ strain - nondimensional */
/* */
/* Output Variables: */
/* */ load -- compression load (pounds) */
/* */ diameter -- diameter of steel rods(inches) */
/* */ stress - compression stress (lb/in²) */
/* */ strain - nondimensional */
****************************************************************
```

```c
#include <stdio.h>
FILE *outptr;

int main ()
{
    const float PI = 3.141593;
    const float ES = 30000000;
    float load, diameter, area, stress, strain;

    outptr = fopen("fileout.dat", "w");

    for(load = 50000; load <= 100000; load += 25000)
    {
        fprintf(outptr,"\nCompression Load = %10.2f\n\n", load);
        fprintf(outptr,"Diameter      Stress      Strain\n");
        for(diameter = 2.0; diameter <= 5.0; diameter += 1.0)
        {
            area = (PI * diameter * diameter) / 4.0;
            stress = load / area;
            strain = stress / ES;
            fprintf(outptr,"%5.2f      %8.2f      %8.6f\n", diameter, stress, strain);
        }
    }
    return 0;
}
```
