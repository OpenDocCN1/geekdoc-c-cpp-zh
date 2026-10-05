where $P$ is the pressure, $V$ is the volume, $n$ is the amount of the gas, $R$ is the gas constant, and $T$ is the temperature. So the volume is computed by

```
(define (* gas-volume pressure temperature amount)
  (/ amount gas-constant temperature) pressure))
```

```
(define gas-constant 8.3144621 ;J/(K*mol))
```

and the radius of a sphere is computed by

```
(define (sphere-radius volume)
  (expt (/ (* 4/3 pi)) (1/3)))
```

```
(define pi (* 4 (atan 1 1))))
```

(Note: 4/3 and 1/3 are rational constants–the slash is not an infix division operator.) The choice of gas constant makes this program use SI units, so the pressure is in newtons per square meter, the temperature is in kelvin, the amount is in moles, the volume is in cubic meters, and the radius is in meters.

This looks straightforward, but use of other units can make things complicated. Suppose we want to measure the temperature in degrees Fahrenheit, the pressure in pounds per square inch, and the radius in inches. Determining the correct formula is more complicated than computing the numerical answer. We could modify the simple formula to account for the units, but this obscures the idea of the program and specializes it to the particular problem. Alternatively, we could arrange to have a modular way to convert the units.

A unit conversion is a procedure that is linked to its inverse. We can write temperature conversions between conventional units, such as Fahrenheit and Celsius temperatures, and between SI and conventional units.

```
(define fahrenheit-to-celsius
  (make-unit-conversion (lambda f) (* 5/9 (- f 32))
  (lambda c) (+ c 9/5))))
```

```
(define celsius-to-kelvin
  (let ((zero-celsius 273.15)) ;kelvin
    (make-unit-conversion (lambda c) (+ c zero-celsius))
    (lambda k) (- k zero-celsius))))
```