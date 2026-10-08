Compute the heat transfer in watts

```
q = h * a * (t_plate - t_air)
```

Convert to kilowattre and Btu/hour
Output the heat transfer value.

End

Program

```
********************************************************************/
/*                                                /
/*  Computation of Heat Transfer Through a Plate      */
/*                                                */n********************************************************************/
/* Constant:                               */
/*  HCOF = 3411.87 - heat transfer coefficient      */
/*                                                */n/*  Input Variables:                                */
/*  length - plate length in centimeters           */
/*  width - plate width in centimeters               */
/* tplate - Plate temperature degree centigrade   */
/* tair - air temperature, centigrade             */
/*                                                */n/*  Input Coefficient:                             */
/*  hcnvc - convection heat-heat transfer         */
/*  coefficient                                    */
/*                                                */
/*  Working Variables:                             */
/*  area - Area of the plate in meters             */
/*                                                */
/*  Computed Variables:                             */
/*  qheat - Heat transfer in kw or Btu/h           */
/*                                                */
/*  Output Variables:                               *
/*  qheat - Heat transfer in kw or Btu/h           */
/*                                                */
********************************************************************
```