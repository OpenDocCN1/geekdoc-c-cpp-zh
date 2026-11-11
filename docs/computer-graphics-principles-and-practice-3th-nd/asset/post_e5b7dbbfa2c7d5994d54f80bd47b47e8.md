
The input for the algorithm is a texture image (e.g., a photograph of a brick wall) that’s called the **source**, and a size, *n* × *k*, of an image to be created. The output is an *n* × *k* image we’ll call the **target**; typically *n* × *k* is much larger than the size of the input image. The idea is that the target should look like it comes from “the same stuff as the source”; for example, like a photograph of a larger region of a brick wall. Figure 20.21 shows the idea. We fill in the target image row by row, moving left to right. At a typical point in the filling-in procedure, the blue-colored pixels have had their values determined and the yellow area is still to be processed. We select a small rectangle (2 × 3 in the figure) containing mostly known pixels, and one unknown (pink) pixel at the bottom right. (We’ll call this set of six pixels a **template**.) The goal is to determine a value for this last pixel, and then advance the template one step to the right.

We take the five known pixels in the rectangle, and look in the source image for similarly shaped clusters that match these five known pixels. We then pick one with a good fit, and copy its *sixth* pixel into the appropriate spot in the target. We then move the template one step to the right, and proceed.

This description glosses over several important points, such as “How do we get started?” and “How do we move to a new row?” and “How do we find in the source image good-matching patches for the known template pixels without taking forever to do it?” One way to start is with random pixels from the source image filling the target. As we start at the upper left, finding a “match” for the first 5-pixel patch will be very difficult—we’ll have to be happy with a not-very-good result. But as we move forward, things gradually start to work better. To improve matters, we may want to run the algorithm several times, working top to bottom, bottom to top, left to right, right to left, etc., to clean up the edges.

As for finding good candidates as matching patches, one useful observation is that if you move the template one step to the right, a good candidate for filling in the next pixel is exactly one step to the right of the source pixel you just used (i.e., the algorithm is very likely to favor copying whole rows of pixels). This can be generalized. For instance, right above the missing pixel is one that you filled in one row earlier. If we look at the corresponding source pixel, the one immediately below it is a good candidate for the missing pixel too. In fact, the source locations of all five known template pixels similarly provide (with slight offsets) good candidate locations in which to find a source for the missing sixth pixel. The algorithm proceeds by picking a pixel from this candidate set. Occasionally (e.g., when a source pixel is near the edge of the image) this may not work, in which case we have to replace this candidate with another; there are many possible choices, and the details are not important.

The results are quite impressive. Figure 20.22 shows an example in which a few berries are used to synthesize many berries. The algorithm has another advantage: It’s possible to start with the target image partly filled in! We can declare in advance that we want certain pixels to have certain colors, and when the algorithm reaches these pixels, it finds them already “filled in” and leaves them unchanged. But their presence affects how well the subsequent patches fit with one another, and hence the synthesis of subsequent pixels. Figure 20.23 shows an example.

The end result of the synthesis process is that long diagonal strips from the source tend to be copied whole, in such a way that they match up with neighboring strips. Figure 20.24 shows this structure.

In this situation, a small square of the target image around some pixel (*i, j*) tends to match a small square in the source image around some pixel (*i′, j′*), although along the edges between strips this isn’t an exact match. If we compute

$$
\mathbf{v}_{ij} = [i' - i \quad j' - j]^{\mathsf T},
$$

then we see that $\mathbf{v}$ tends to be locally constant as a function of $i$ and $j$, precisely because of the approach that the algorithm takes, namely, using nearby pixels’ $\mathbf{v}$-vectors as candidates for the $\mathbf{v}$-vector of the pixel being synthesized.

![](img/f464cd0043eb5336aa0543fe20a0561b_613_0.png)

*Figure 20.20: Reaction-diffusion textures. Top: Textures synthesized by Kass and Witkin. (Courtesy of Michael Kass, Pixar and Andrew Witkin, © 1991 ACM, Inc. Reprinted by permission.) Bottom: Texture synthesized by Greg Turk. (Courtesy of Greg Turk, © 1991 ACM, Inc. Reprinted by permission.)*

![](img/f464cd0043eb5336aa0543fe20a0561b_613_1.png)

*Figure 20.21: A partly synthesized image, and a highlighted region with one unknown pixel.*

This notion can be generalized: Given an image $A$ and an image $B$, we can extract, for each pixel $(i,j)$ of $A$, a $p \times p$ square $P$ centered there, and look at every $p \times p$ patch in $B$ to find one “closest” to $P$. We then find the center of this $B$-patch, $(i',j')$, and set $\mathbf{v}_{ij} = [i' - i \quad j' - j]^{\mathsf T}$. The resultant collection of vectors is called a **nearest-neighbor field** (for patches of size $p$). Computing this field can be very slow, but if the images $A$ and $B$ are similar, the field tends to have the same kind of coherence exhibited by the results of the Ashikhmin algorithm: Neighboring pixels tend to have similar vectors. Barnes et al. [BSFG09] use this observation to develop an approach to computing the nearest-neighbor field (or a very close approximation) for two images very quickly.

While the resultant field might be used for texture synthesis if $B$ is an example texture and $A$ is a large image that has some structural resemblance to the texture in $B$, Barnes et al. actually describe a great many *other* computational photography applications based on it, such as the “image shuffling” shown in Figure 20.25, in which the user annotates a region (in this case, the person in the photo) and a place to which to move the region. A combination of the nearest-neighbor field computation and an expectation-maximization algorithm that seeks to fill in the hole (and adjust pixels near the moved region) in a way that makes the patch matching optimal produces the image in which the person appears to have moved within the photo.

![](img/f464cd0043eb5336aa0543fe20a0561b_614_0.png)

*Figure 20.22: A tiny source image and a large image synthesized from it (Courtesy of Michael Ashikhmin, © 2001 ACM, Inc. Reprinted by permission.)*

## 20.10 Discussion and Further Reading

We’ve only touched on texture mapping here. Table 20.1 gives some hint of how powerful the method is, which should hardly be surprising, since at its essence, it’s “indirection” or “function evaluation,” both of which are at the very heart of computation.

With texture mapping, we’re (generally) altering parameters to a lighting computation. But in Chapter 31, we’ll see that what we actually want to compute for each sample in a rendering is an estimate of an integral, and the integrand has the general form of a lighting model. As we move from sample to sample, this integral varies. If the variation is not band-limited, we’ll get aliasing errors. But texture mapping makes certain that the individual parameters within the integrand are each band-limited, rather than the value of the integral. In other words, we’ve band-limited and then integrated, rather than integrated and then band-limited. Since these two operations do not generally commute, we’re producing potentially incorrect results. The degree to which they’re incorrect has not yet been thoroughly analyzed.

Although texture mapping is used in rendering, it’s also forced into service in more general computations. Both GL and DX shaders use texture maps as general-purpose RAM for storing arbitrary data structures. That is because the first graphics systems didn’t support random access memory or anything beyond primitive floating-point types. The practice of tricky uses of texture memory is losing currency with new hardware that supports arbitrary read and write operations, often using sophisticated abstractions. DirectCompute and CUDA shaders already

![](img/f464cd0043eb5336aa0543fe20a0561b_614_1.png)

*Figure 20.23: A source image, a hand-drawn “guide,” and the resulting synthesized image after five rounds of synthesis (Courtesy of Michael Ashikhmin, © 2001 ACM, Inc. Reprinted by permission.)*
