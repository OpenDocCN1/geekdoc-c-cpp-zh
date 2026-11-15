# 3. HAND EXAMPLE

For a hand example, we will compute the great circle distance between New York and London. The latitude and longitude of New York is 40.75° N and 74° W, respectively, and the latitude and longitude of London is 51.5° N and 0° W, respectively.

The spherical coordinates for New York are
φ = (90 − 40.75)° = 49.25(π/180) = 0.8596
θ = (360 − 74)° = 286(π/180) = 4.9916
ρ = 3960.

The rectangular coordinates for New York (to two decimal places) are
x = ρ sin φ cos θ = 826.90
y = ρ sin φ sin θ = −2883.74
z = ρ cos θ = 2584.93.

Similarly, the rectangular coordinates for London can be computed to be
x = 2465.16, y = 0, z = 3099.13.

The cosine of the angle between the two vectors is equal to the dot product of the two vectors divided by the product of their lengths, or 0.6408. Using an inverse cosine function, γ can be determined to be 0.875 radians. Finally, the distance between New York and London is
0.875 · 3960 = 3466 miles.

# 4. ALGORITHM DEVELOPMENT

To develop the algorithm, we must first decompose the problem solution into a set of sequentially executed steps, as follows:

# Decomposition Outline

+   1. Read latitude and longitude for the two locations.
+   2. Compute the distance between the two locations.
+   3. Print the distance computed.

After completing the hand example, converting the decomposition to pseudocode is straightforward. Since other programs may also need to determine the distance between two points that are specified with latitude and longitude, we will develop the computations using a function.

# Refinement in Pseudocode

```
main: read latitude and longitude for the two points
    compute great circle distance using a function, gc_distance
    print distance
gc_distance(lat1N,long1W,lat2N,long2W):
    convert latitude and longitude to spherical coordinates
    convert spherical coordinates to rectangular coordinates
    compute the angle between the two vectors
    compute the great circle distance for the arc between the two vectors
```