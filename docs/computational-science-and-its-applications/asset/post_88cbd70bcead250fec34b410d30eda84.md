
## TABLE 8.1

Multispectral vs. Panchromatic Images

| Images | Spatial Resolution | Spectral Resolution |
|---|---|---|
| Multispectral | low | high |
| Panchromatic | high | low |

Figure 8.1 shows the fusion effect of panchromatic and multispectral images into a pan-sharpened image.

Intensity hue saturation (IHS) methods begin with the transformation of RGB (Red, Green, Blue) to IHS space followed by replacing the intensity band with a Panchromatic image. Finally this new image is inversely mapped back from IHS to RGB space. This conventional IHS based method is efficient and simple to execute but it is not able to enhance an RGB-based MS image and often contains major distortions in spectral aspect, due to color changes among fused MS and the composition of re-sampled bands. Thus it misses near infrared band (NIR) which is the fourth band after RGB. [4] studies a fast pan-sharpening technique with spectral adjustment for IKONOS imagery. IKONOS is a commercial earth observing satellite collecting MS and Pan images.

In [5], two approaches are merged to form a hybrid pan-sharpening scheme: (a) local variation with contourlet transformation (CT); and (b) adaptive PCA and CT. It performs better compared to APCA+CT, APCA, PCA+CT, and PCA. Thus for multispectral satellite images, the spatial details are enhanced by introducing Pan images and extracting higher spatial details. [6] discusses a pan-sharpening method based on deep neural networks to model complex relations among independent variables by composing multiple non linear levels. Back propagation is also used for improved training as a second training phase after the pre-training phase of the complete deep neural network. In [7], sparse pan-sharpening of images based on a self-adaptive technique is studied. It makes no assumption about the spectral structure of the Pan image and inherits sparse signal reconstruction super

![](img/81c56bc4b2fca1951aff5e0ab85b66be_140_0.png)

## FIGURE 8.1

(Left) Panchromatic, (middle) multi-spectral, and (right) pan-sharpened image.

resolution capacity; it yields less spectral distortion and higher spatial resolution. In [8], a method to remove speckle noise is discussed using generalized guided filters and Bayesian non-local means. It calculates the nonlinear weight kernel and generates guidance image with homogeneity analysis considering maximum likelihood rule and local regions.

Due to its robustness and effectiveness, multi-scale pan-sharpening based on the Laplacian pyramid decomposition is used such as shiftable complex directional pyramid [9], contrast pyramid transform [10], image decomposition [11], Laplacian pyramid with multiple features (LPMF) [12], etc. These techniques have emerged as a popular method that has shown utility in many pan-sharpening–based applications. However, the number of pyramid levels increases with the image size, which implies sophisticated data management and memory accesses, as well as additional computations [13]. Due to the loss of dependence of coefficients, most of the traditional multi-scale decomposition-based image pan-sharpening methods suffer from an inaccurate image representation. To overcome these problems, nonsubsampled shearlet transform (NSST) is used. The dependence of NSST coefficients is captured by the contextual hidden Markov model [14]. Explicit luminance and contrast masking models are combined to give the perceptual importance of each coefficient of source images produced by the dual-tree complex wavelet transform. This combined model of perceptual importance is used to select which coefficients are retained and furthermore to determine how to present the retained information in the most efficient manner as in [15]. In this chapter, we present a novel image pan-sharpening approach to overcome these limitations. The proposed method evaluates weight values of the input images and then uses the corresponding pan-sharpening map to develop the final fused image. To reduce the halo and gradient reversal artifacts further, a modified non-local means-based guided image filter (MNLMGIF) is proposed and applied on the fused image as a post-processing technique. Therefore, this method maintains all the information from both images, which is not done by most of the existing pan-sharpening methods. Moreover, the proposed technique can reduce gradient and halo artifacts problems using MNLMGIF. To justify the efficiency of the proposed method quantitatively, experiments have been carried out on remotely sensed images [16], QUICKBIRD [17], IKONOS [18], and MODIS [19] sensors.

The remainder of this chapter is organized as follows: a proposed filtering-based image pan-sharpening technique is discussed in Section 8.2. To verify the effectiveness of the proposed technique, visual and quantitative results are carried out on remote sensing images in Section 8.3. In Section 8.4 the conclusion is presented along with future directions.

## 8.2 Proposed Method

This section discusses the proposed methodology. A systematic procedure is adopted to evaluate the weighted map, multiscale image pan-sharpening, guidance image generation for filtering, and finally MNLMGIF for pan-sharpening is used. Figure 8.2 demonstrates the overview of graphical flow explaining the technique.

### 8.2.1 Nonsubsampled Contourlet Transform

Nonsubsampled Contourlet Transform (NSCT) is an extension of the well-known Contourlet Transform (CT) [20]. The multiscale decomposition feature of CT is achieved

by using Laplacian Pyramids (LPs). Directional Filter Banks (DFBs) are used to generate the directional decomposition of CT. LP and DFB utilize downsamplers and upsamplers, respectively [21]. NSCT is designed using Nonsubsampled Pyramids (NSP) and nonsubsampled DFBs to achieve shift-invariant feature (see Figure 8.3) [22].

### 8.2.1.1 Nonsubsampled Pyramid (NSP)

Nonsubsampled pyramid guarantees the multiscale characteristic of NSCT. NSP depends upon two-channel nonsubsampled 2D filter banks. The three stage decomposition of NSP

## FIGURE 8.3

(a) NSFB structure that implements the NSCT; (b) idealised frequency partitioning obtained with NSFB structure (Yang et al., 2015).

is described in Figure 8.4(a). An efficient reconstruction is achieved provided the filters satisfy Bezout identity be defined as [22]:

```
H₀(z)G₀(z) + H₁(z)G₁(z) = 1
```

Here, G₀(z) and G₁(z) represent low- and high-pass reconstruction filters, respectively. H₀(z) and H₁(z) represent low- and high-pass decomposition filters, respectively.

The passband frequency support of the low-pass filter at jth level is the region [−π/2ʲ, π/2ʲ]². In the same way, the support of the high-pass filter is the complement of low-pass support

## FIGURE 8.4

Nonsubsampled pyramid: (a) three-stage pyramid decomposition; (b) frequency divisions of a nonsubsampled pyramid (Yang et al., 2015).

![](img/81c56bc4b2fca1951aff5e0ab85b66be_143_0.png)

![](img/81c56bc4b2fca1951aff5e0ab85b66be_143_1.png)

![](img/81c56bc4b2fca1951aff5e0ab85b66be_143_2.png)

![](img/81c56bc4b2fca1951aff5e0ab85b66be_143_3.png)

![](img/81c56bc4b2fca1951aff5e0ab85b66be_142_0.png)

## FIGURE 8.2

Graphical abstract of the proposed pan-sharpening technique.

saturation regions are depicted in a better form in the outcome. The saliency weighted map calculates the visibility degree relative to the neighborhood areas. It basically measures the relative coefficients of a region or a segment in an NSDFB with respect to its surroundings based upon coefficient orientation and values. As discussed in [25], the weight is defined as follows:

```
$$W_n^S = ||\text{NSDFB}_n^f - \text{NSDFB}_n^{\text{avg}}||$$
```

Here NSDFB$_n^{\text{avg}}$ is the average coefficient value of NSDFB and is of low-resolution image from where the high-frequency noise needs to be removed. It is obtained by using the high-frequency value of cut-off ($f=\pi/2.75$) into a separable binomial kernel. Therefore, the impact of these three measures is important in different aspects but the first one, which is the luminance weight map, has greater visibility impact overall. The aggregated weight map is obtained by multiplicative expression:

```
$$W_n = W_n^L \times W_C^n \times W_n^S$$
```

The normalized form of the aggregate weight guarantees that the sum will be 1 for each pixel:

```
$$\overline{W_n} = \frac{W_n}{\sum W_n}$$
```

### 8.2.3 Pan-Sharpening on Multi-Scale

During the image pan-sharpening, weighted inputs are computed in order to detect the features more significantly for each pixel:

```
$$F = \sum_n \overline{W_n} I_n \text{s.t.} \sum_n \overline{W_n} = 1$$
```

Intensity scale of the resulting image is maintained because a normalized weighted map is used in the above calculation. But this equation may result in halos artifacts where the weighted maps have stronger transitions. Therefore an approach [26] which is known as pyramidal refinement is applied to get rid of this degradation. In the proposed method, $I_n$ is actually decomposed using a Laplacian operator into a pyramid with different scales. On the parallel track, $\overline{W_n}$ is also derived from a Gaussian pyramid for each of its weighted normalized maps. Now at each respective pyramid level $i$ (default value $i=5$) the mixing is applied as follows:

```
$$F_i = \sum_n G_i(\overline{W_n}) L_i(I_n)$$
```

where $L_i$ is the Laplacian operation of the input $I$ and $G_i(\overline{W_n})$ is the Gaussian operator on the weighted normalized map $\overline{W_n}$. Bottom-up direction is adopted for respective pyramid layers and the final restored version of $I$ is calculated after adding all the pyramid levels using upsampling operator $U(x)$ with $x=2^{i-1}$.

```
$$G(x) = \sum_i F_i(x) U(x)$$
```
