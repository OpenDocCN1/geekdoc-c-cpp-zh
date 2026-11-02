be used to simplify a system with complex external state. Let us look at an example.

Air density is perhaps the single most important factor affecting aircraft performance. Density altitude is a commonly used measure of air density. It is the altitude, relative to standard atmosphere conditions, at which the air density would be equal to the indicated air density at the place of observation. The density altitude at a location may be computed from the current temperature, air pressure, and humidity. Here is a specification for a package that uses external sensors to measure these three components and determine the density altitude:

```
package Density_Altitude
  with SPARK_Mode => On,
    Abstract_State => (Density_State with External => Async_Writers)
is
  type Feet is range -5.0000 .. 100.000;

  procedure Read (Value : out Feet)
    with Global => (Input => Density_State),
      Depends => (Value => Density_State);
end Density_Altitude;
```

This package encapsulates an abstract external state from which the density altitude is returned by a call to procedure Read. The abstract state, Density_State, is given the single external property Async_Writers. This property tells us and SPARK that Density_State will be updated by components external to our system. As the other three properties (Async_Readers, Effective_Writes, and Effective_Reads) are not listed, they default to false.

We refine Density_State and the Global and Depends aspects of procedure Read in the package body:

```
with Density_Altitude.Temperature_Unit,
     Density_Altitude.Pressure_Unit,
     Density_Altitude.Humidity_Unit;
package body Density_Altitude
  with SPARK_Mode => On,
    Refined_State => (Density_State => (Temperature_Unit.Temp_State,
                                        Pressure_Unit.Press_State,
                                        Humidity_Unit.Humid_State)) is

procedure Read (Value : out Feet)
  with Refined_Global => (Input => (Temperature_Unit.Temp_State,
                                    Pressure_Unit.Press_State,
                                    Humidity_Unit.Humid_State)),
```