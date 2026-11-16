Since the reconstructed images also contain information that is not relevant to the microcalcifications, we need to filter out this erroneous information. The histogram threshold requires the peak value of the histogram of a given gray scale \( g_{peak} \). We formulate the following thresholding rule:

```
(9.46)
\(\begin{cases} v_r(x, y) = 0, \text{if } v_r(x, y) \le (g_{peak} + 1) + 0.5 \times \sigma_{nz}^r, \\ v_r(x, y) \text{ remain unchanged for further processing.} \end{cases}\)
```

where \( \sigma_{nz}^r \) and \( \mu_{nz}^r \) are the standard deviation and mean obtained from all nonzero (nz) pixels in the reconstructed images; and \( v_r(x,y) \) is the value of the \( (x,y) \)th pixel in the reconstructed image. After this step, the CAD algorithm adds the two images together in a spatially coherent fashion to form a composite image in which all microcalcification information is contained.

We now refer back to the original image. Since the pixel intensity from the microcalcification is greater than 137 in an 8-bit (256 levels) linear gray scale, we make use of this information to formulate a dark pixel removal threshold as follows:

```
(9.47)
\(\begin{cases} v_r(x, y) = 0, \text{if } v_r(x, y) = 0; \\ v_r(x, y) = 0, \text{if } v_r(x, y) \neq 0, \text{and } u(x, y) \le \mu_{org} + 0.5 \times \sigma_{org} \\ v_r(x_{nz}, y_{nz}) = v_r(x, y), \text{if } v_r(x, y) \neq 0, \text{and } u(x, y) > \mu_{org} + 0.5 \times \sigma_{org} \end{cases}\)
```