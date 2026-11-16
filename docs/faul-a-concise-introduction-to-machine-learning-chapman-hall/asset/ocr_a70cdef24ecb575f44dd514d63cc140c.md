![](bbox=[0.19, 0.1, 0.79, 0.24])

# Figure 8.3: Cone sensitivity.

# Table 8.1: Chromacy

| Chromacy | Types of cone cells | Rough number of colours perceived | Examples |
|---|---|---|---|
| Monochromacy | 1 | 100 | Marine mammals |
| Dichromacy | 2 | 10,000 | Most terrestrial mammals |
| Trichromacy | 3 | 10 million | Humans, great apes, some insects |
| Tetrachromacy | 4 | 100 million | Most reptiles, amphibians, birds and insects, rarely humans |
| Pentachromacy | 5 | 10 billion | Some insects (butterflies), some birds (pigeons). |

We cannot imagine how a butterfly sees the world. Our brain has never experienced the extra information and thus has not learned how to interpret it.

There are three primary colours: red, green, and blue. All other colours are mixed from these. In computer imaging, they are represented in an array of bytes taking values between 0 and 255: [r, g, b], where red = (255, 0, 0), green = (0, 255, 0), and blue = (0, 0, 255). Linearisation means multiplications by a number and additions are allowed. For example

+   - red + green = (255, 255, 0) = yellow,
+   - red + 0.5* green = (255, 128, 0) = orange,
+   - red + 0.5* blue = (255, 0, 128) = pink,
+   - 0.6* red + 0.8* blue = (153, 0, 204) = purple.

In regression we estimate the relationship between variables. Or in other words, given the intensity of red, green, and blue for some samples, what is the relationship between intensity values and the colour? Can we predict the colour given the intensity values, as our eyes and brain do? Regression has its applications in

+   - Computer Vision: e.g. image compression and restoration,