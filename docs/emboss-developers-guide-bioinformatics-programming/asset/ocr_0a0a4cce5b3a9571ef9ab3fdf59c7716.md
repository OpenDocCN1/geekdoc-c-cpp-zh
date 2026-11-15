# 6.17.3.6 long arrays

+   AjPLong 1D long array
+   AjPLong2d 2D long array
+   AjPLong3d 3D long array

# 6.17.3.7 double arrays

+   AjPDouble 1D double array
+   AjPDouble2d 2D double array
+   AjPDouble3d 3D double array

# 6.17.4 ACD datatypes

The ACD datatype for handling array input is:

+   array List of either integer or floating point numbers

# 6.17.5 ACD data definition

A typical ACD definition for array input:

```
array: thresholds
[
  information: "Values to represent 'identical', 'similar' and 'related'"
  default: "-1.5,0.0,1.5"
  minimum: "0.0"
  size: "3"
  sum: "0"
  sumtest: "Y"
]
```

# 6.17.5.1 Parameter name

All data definitions for array input should have an intuitive name (Section A.1.3, 'Parameter naming conventions') although no standard name scheme is enforced.

# 6.17.5.2 Common attributes

Attributes that are typically specified are summarised below. They are datatype-specific (Section A.5, 'Datatype-specific attributes') unless they are indicated as being global attributes (Section A.4, 'Global attributes').

+   default: A global attribute that specifies a default value.

+   minimum: Specifies the minimum permitted value.