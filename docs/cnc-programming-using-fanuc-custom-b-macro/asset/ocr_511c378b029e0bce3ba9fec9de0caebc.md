To keep things simple, G81 would be used for drilling holes, at the current spindle speed. The readers are, however, encouraged to introduce additional local variables for these, which is being left as an exercise. For a drilling cycle other than G81, information regarding dwell value (for G82) or peck distance (for G73/G83) would also be needed, necessitating the use of two more local variables for assigning values for these. Note that there is no harm in specifying a dwell value or a peck distance for a canned cycle that does not use these features. It would simply ignore such arguments. Hence, the canned-cycle block can have the same argument list, irrespective of whether it refers to G81, G82, G73, or G83.

Though a macro can be written for machining a flange with any values for the chosen parameters, a family of flanges, as described in Table 9.2, would be considered here. Note that X and Y are not really the parameters of a flange. Their values depend on how the flange has been clamped on the machine table, with respect to the active work coordinate system (G54, G65, etc.). Hence, the same values for these have been taken for all the flanges, as these values have no significance with regard to the type of a flange. It was necessary to include these variables for the sake of generality. Similarly, the start angle may not have any relevance. Hence, 0° has been taken in all cases. It has been introduced to take care of some special requirement.

We would assume the following (though it is not difficult to relax these assumptions, it has been left as an exercise for the readers):

+   1. The calling program uses absolute coordinates (G90).
+   2. The proper tool is held by the spindle that rotates with proper rpm, before calling the macro.
+   3. Tool length compensation has been incorporated in the calling program.

| Flange Number | X | Y | Z | D | H | S | R | F |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 1 | 150 | 100 | 5 | 50 | 4 | 0 | 1 | 60 |
| 2 | 150 | 100 | 10 | 100 | 6 | 0 | 1 | 50 |
| 3 | 150 | 100 | 15 | 150 | 8 | 0 | 1.5 | 40 |
| 4 | 150 | 100 | 20 | 200 | 10 | 0 | 2 | 30 |
| 5 | 150 | 100 | 20 | 300 | 12 | 0 | 2 | 30 |

Table 9.2 — Dimensions of the Flange Shown in Fig. 9.3