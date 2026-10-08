```
fclose(outptr);
return 0;
}
```

Input and Output
Input data file salesin.dat

17563 15 1245.56
59324 25 1567.95
65098 10 2050.76
45981 16 1850.67

Output data file salesout.dat

| id | units_sold | cost-per-unit | sales | commission |
|---|---|---|---|--|
| 17563 | 15 | 1245.56 | 18683.40 | 2242.01 |
| 59324 | 25 | 1567.95 | 39198.75 | 4703.05 |
| 65098 | 10 | 2050.76 | 20507.60 | 2460.91 |
| 45981 | 16 | 1850.67 | 29610.72 | 3553.29 |

Total sales = 108000.47
Total commission = 12960.06

# 3.5.5 Wavelength of an Electron

Problem Write a program to compute the wavelength λ of an electron at velocities of 20%, 30%,...,100% speed of light (considered as a particle) given the mass, m, in kilograms and velocity, v, in meters per second. This program uses scientific data in E format.

Method The equation (De Broglie's equation) to compute the wavelength λ of a particle is as follows:

$$\lambda = \frac{h}{mv}$