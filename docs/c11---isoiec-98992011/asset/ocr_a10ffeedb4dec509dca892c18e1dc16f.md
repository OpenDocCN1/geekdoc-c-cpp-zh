# F.10.1.3 The atan functions

+   - atan(±0) returns ±0.
- atan(±∞) returns ±π/2.

# F.10.1.4 The atan2 functions

+   - atan2(±0, -0) returns ±π.³37³
- atan2(±0, +0) returns ±0.
- atan2(±0, x) returns ±π for x < 0.
- atan2(±0, x) returns ±0 for x > 0.
- atan2(y, ±0) returns -π/2 for y < 0.
- atan2(y, ±0) returns π/2 for y > 0.
- atan2(±y, -∞) returns ±π for finite y > 0.
- atan2(±y, +∞) returns ±0 for finite y > 0.
- atan2(±∞, x) returns ±π/2 for finite x.
- atan2(±∞, -∞) returns ±3π/4.
- atan2(±∞, +∞) returns ±π/4.

# F.10.1.5 The cos functions

+   - cos(±0) returns 1.
- cos(±∞) returns a NaN and raises the “invalid” floating-point exception.

# F.10.1.6 The sin functions

+   - sin(±0) returns ±0.
- sin(±∞) returns a NaN and raises the “invalid” floating-point exception.

# F.10.1.7 The tan functions

+   - tan(±0) returns ±0.
- tan(±∞) returns a NaN and raises the “invalid” floating-point exception.