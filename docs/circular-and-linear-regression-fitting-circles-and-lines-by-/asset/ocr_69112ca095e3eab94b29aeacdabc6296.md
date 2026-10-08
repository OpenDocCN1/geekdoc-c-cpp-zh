# PREFACE

images is not the best idea; it inevitably forces a different treatment of the $x$ and $y$ variables, conflicting with the very nature of the problem. Instead, one fits geometric shapes that are to be found (or expected) on the given image. Those shapes are usually described geometrically: lines, rectangles and other polygons, circles, ovals (ellipses), etc. Analytically, the basic curved shapes—circles and ovals—are defined by implicit quadratic functions. More complicated curves may be approximated by cubic or quartic implicit polynomials [150, 176]; however, the latter are only used on special occasions and are rare in practice. Our book is devoted to fitting most basic geometric curves—circles and circular arcs—to observed data in image processing applications. This topic is different from the nonlinear EIV regression in other statistical applications mentioned above and covered in [27, 28]. Fitting ellipses to observed data is another important topic that deserves a separate book (the author plans to publish one in the future).

![](bbox=[0.25, 0.3, 0.72, 0.58])

Figure 0.1 The Brogar Ring on Orkney Islands [15, 178]. The stones are marked by pluses; the fitted circle is the dotted line.

The problem of fitting circles and circular arcs to observed points in 2D images dates back to the 1950s. Its first instance was rather peculiar: English engineers and archaeologists examined megalithic sites (stone rings) in the British Isles trying to determine if ancient people who had built those mysterious structures used a common unit of length. This work started in the 1950s and continued for several decades [15, 65, 177, 178, 179]; see an example in Fig. 0.1, where the data are borrowed from [178].

In the 1960s the necessity of fitting circles emerged in geography [155]. In the 1970s circles were fitted to experimental observations in microwave engineering [54, 108]; see an example in Fig. 0.2, where the data are taken from