
- [A.8] M. H. Yang and B. Moghadam. Gender classification using support vector machines. In Proceedings of IEEE International Conference on Image Processing, volume 2, pages 471–474, 2000.
- [A.9] Y. Yang and X. Liu. Re-examination of text categorization methods. In Proceedings of the 1999 22nd International Conference on Research and Development in Information Retrieval (SIGIR '99), pages 42–49, 1999.
- [A.10] N. Zhang, R. Farrell, F. Iandola, and T. Darrell. Deformable part descriptors for fine-grained recognition and attribute prediction. In IEEE International Conference on Computer Vision, 2013.

## Appendix B How to Differentiate a Function Containing a Kernel Operator

The function of Eq. 6.25 is complicated by involving a sum over all the pixels and by the use of convolution that creates terms involving more than one pixel at a time. This Appendix discusses the differentiation of such an expression. The material is placed in an appendix because it is not essential to understanding the concepts of noise removal, but is important for those who must implement software.

In previous discussions, the effects of blur were excluded and noise was assumed to be the only source of distortion. In this section, the results derived in chapter 6 are extended and include blur in the formation of the measured image, g, such that the noise terms can be written as Eq. B.1. We will illustrate differentiation of the prior and the noise terms as if both contained convolutions. First, we illustrate how to differentiate a function containing a kernel operator (or a blur operator).

\(\sum_i ((f \otimes h) - g_i)^2\) (B.1)

Taking a one-dimensional example, assume \(f_i\) is a pixel from the original (unknown) image, \(g_i\) is a pixel from the measured image, and \(h\) is the horizontal blur kernel with a finite kernel size 5, as shown below:

![](img/5f95dd954ac63cc68119f6f48ca99e18_374_0.png)

Here, the derivative of the noise term with respect to \(f\) in Eq. B.1, which is required in order to use gradient descent, is examined in detail. We will make use of the fact that we are taking a partial derivative of a summation. Therefore, any term in the sum that does not involve the denominator of the partial derivative will be zero.

![](img/5f95dd954ac63cc68119f6f48ca99e18_375_0.png)

Figure B.1 The reverse kernel in the derivation of the noise term.

First write out all the terms involving a pixel (let's pick \(f_4\)) at which a measurement (\(g_4\)) was made in the noise term \(H_\alpha\) above

```
\(E_4 = ((f \otimes h)_2 - g_2)^2 + ((f \otimes h)_3 - g_3)^2 + ((f \otimes h)_4 - g_4)^2\) (B.2)
+ ((f \otimes h)_5 - g_5)^2 + ((f \otimes h)_6 - g_6)^2
= (f h_{-2} + f h_{-1} + f h_0 + f h_1 + f h_2 - g_2)^2
+ (f h_{-2} + f h_{-1} + f h_0 + f h_1 + f h_2 - g_3)^2
+ (f h_{-2} + f h_{-1} + f h_0 + f h_1 + f h_2 - g_4)^2
+ (f h_{-2} + f h_{-1} + f h_0 + f h_1 + f h_2 - g_5)^2
+ (f h_{-2} + f h_{-1} + f h_0 + f h_1 + f h_2 - g_6)^2
```

where \((f \otimes h)\) denotes the application of kernel \(h\) to image \(f\) with the origin of \(h\) (in this case, the center) located at pixel \(f_r\).

The derivative of \(H_\alpha\) with respect to pixel \(f_4\) can then be derived as:

```
\(\frac{\partial H_\alpha}{\partial f_4} = 2((f \otimes h)_2 - g_2)h_2 + 2((f \otimes h)_3 - g_3)h_1 + 2((f \otimes h)_4 - g_4)h_0\)
+ 2((f \otimes h)_5 - g_5)h_{-1} + 2((f \otimes h)_6 - g_6)h_{-2}\) (B.3)
\(\frac{\partial H_\alpha}{\partial f_4} = ((f \otimes h) - g) \otimes h_{rev})|_{f_4}\) (B.4)
```

where the reverse of the kernel \(h\), \(h_{rev} = [h_2 | h_1 | h_0 | h_{-1} | h_{-2}]\), and \((f \otimes h - g)\) is computed at all points. The application of \(h_{rev}\) is illustrated more clearly in Figure B.1 where we assume \(n_i = ((f \otimes h) - g)\). The application of the reverse kernel with a two-dimensional image follows the same rule as that in the one-dimensional case. Equation B.5 shows a \(3 \times 3\) kernel function (\(h\)) and the corresponding reverse kernel \(h_{rev}\).

```
\(h = \left[ \begin{array}{ c c c } h_{-1,-1} & h_{-1,0} & h_{-1,1} \\ h_{0,-1} & h_{0,0} & h_{0,1} \\ h_{1,-1} & h_{1,0} & h_{1,1} \end{array} \right] , h_{rev} = \left[ \begin{array}{ c c c } h_{1,1} & h_{1,0} & h_{1,-1} \\ h_{0,1} & h_{0,0} & h_{0,-1} \\ h_{-1,1} & h_{-1,0} & h_{-1,-1} \end{array} \right]\) (B.5)
```

Thus, the general form of differentiation when a kernel function is involved is as follows: Let \(\Lambda(f \otimes h)\) be some differentiable function. The derivative with respect to \(f\) is

```
\(\frac{\partial}{\partial f} \Lambda(f \otimes h) = (\Lambda'(f \otimes h)) \otimes h_{rev}\) (B.6)
```

where \(\Lambda'(\xi) = \frac{\partial}{\partial \xi} \Lambda(\xi)\).

Besides the noise term, the prior term can also contain a kernel operator. Recall that the prior energy function models the neighborhood operation and thus can be represented as a kernel operation with the kernel selected dependent on the properties of the image. We illustrate the gradient using the following prior:

```
\(H_p = - \sum_r \exp(-(f \otimes r)^2)\) (B.7)
```

```
\(\frac{\partial H_p}{\partial f} = [2(f \otimes r) \exp(-(f \otimes r)^2)] \otimes r_{rev}\) (B.8)
```

Recall that the derivative of the prior, \(\frac{\delta H}{\delta f}\), is itself an image, and that image is derived by applying \(r\) to \(f\), multiplying (pixel by pixel) with the exponential to produce another image, and applying the reverse of \(r\) to that image.

## Author Index

- Aarts, E., 33
- Adelson, E., 69
- Aleksic, M., 115
- Alfara, M., 76
- Allen, J., 104
- Anh, V., 68, 72
- Arcelli, C., 139
- Armstrong, M., 315
- Badshah, N., 177
- Bae, E., 177
- Baigay, R., 42
- Bailey, A., 209, 215
- Bay, H., 294
- Bengio, S., 294
- Bengio, Y., xiv, 295
- Bennett, E., 115
- Besag, J., 104
- Beucher, S., 150, 187
- Bhau, B., 269
- Biniucki, W., 187
- Blostein, S., 609, 155
- Bimbo, A., 293
- Binford, T., 343
- Björck, A., 32
- Bolle, R., 338
- Bolles, R., 316
- Boone, K., 139
- Boult, T., 343
- Bovik, A., 337
- Boykov, Y., 132, 340
- Boykov, Y., 188, 190
- Boyles, R., 158
- Brady, J. M., 292
- Brue, H., 136, 138, 143
- Brice, C., 166
- Bruckstein, A., 194
- Bundes, A., 112
- Bühlmann, J., 215
- Burges, C., 197
- Burden, R., 192
- Burt, P., 69
- Canny, J., 68, 69
- Caspí, D., 331
- Chan, 177
- Chan, T., 173, 177
- Chan-Vese, 177
- Chellappa, D., 109
- Chen, C.-K., 16, 104
- Chen, C., 59
- Chen, T., 176
- Chen, Y., 156
- Cheng, H., 115
- Cheng, Y., 162, 211
- Chin, R., 194
- Choi, T., 338
- Chong, C. V., 154, 193
- Chung, G., 177
- Clifford, P., 104
- Coll, B., 112
- Comaniciu, D., 163
- Cordella, L., 139
- Corke, P., 11
- Costa, L., 194
- Cortrell, G., 294
- Courtille, A., 295
- Cox, A., 166
- Crowley, J., 69
- Dahlquist, G., 32
- Dai, X., 168
- Dalal, N., 284
- Daugman, J., 73
- deFigueiredo, R., 68
- Dempster, A., 58
- Deriche, M., 72
- Desai, U., 109
- Dollar, P., 294
- Duda, R., xiv, 166
- Eddins, L., 11
- Eischlager, R., 290
- Ess, A., 294
- Faires, J., 32
- Fatemi, E., 112
- Faugeras, O., 269
- Fei-Fei, L., 294
- Fennema, C., 166
- Fiddelaers, P., 69
- Fischler, M., 290, 316
- Flynn, P., 192
- Freeman, W., 115
- Frei, W., 59
- Fukunaga, K., 161
- Funka-Lea, G., 188
- Ganguly, G., 340
- Geiger, D., 109, 194
- Geman, D., 104, 109
- Geman, S., 104, 109
- Gil, J., 136, 138, 143
- Girosi, F., 109
- Goldfeld, D., 192
- Goma, S., 115
- Gonzalez, R., 295
- Goodman, J., 295
- Gonzalez, R., xiv, 343
- Goodfellow, I., 295
- Gool, L., 294
- Gottfried, B., 32
- Graupe, D., 295
- Groshong, B., 139
- Gupta, A., 194
- Gupta, M., 156
- Hadamard, J., 111
- Hammersley, J., 104
- Harlick, R., 68
- Hart, P., xiv, 166
- Hartley, A., 320
- Hartley, R., 304, 315
- Haykin, S., 295
- Hayley, S., 232
- Hazewinkel, S., 281
- Hinton, G., 281
- Hensel, E., 112
- Hinton, G., xiv, 295
- Hoffman, T., 215
- Hoover, A., 192
- Horn, B. K. P., 331, 332
- Hostetler, L., 161
- Hsiao, M., 139
- Huang, C., 136
- Hubel, D., 8, 72
- Illingworth, 211
- Ivins, J., 171
- Jaccard, P., 193
- Jackway, P., 72
- Jain, A., 193
- Jain, R., 87, G, 192
- Ji, Q., 208
- Jiang, X., 192
- Jones, J., 73
- Jordan, M., 188
- Joseph, E., 85
- Julez, B., 314
- Jurie, F., 294
- Kak, A., 193
- Kanade, T., 215
- Kang, S., 115
- Kappoot, S., 109
- Kashyap, R., 104
- Kelly, M., 104
- Kelly, P., 154, 193
- Kim, J., 292
- Kimmel, R., 194
- Kirkpatrick, D., 136, 138, 143
- Kiryti, N., 206, 331
- Kisworo, M., 66
- Klauser, A., 294
- Kolmogorov, V., 190
- Kondepudy, R., 332
- Kong, T. Y., 197
- Kotturi, D., 215
- Krish, K., 281
- Lai, K., 194
- Laird, N., 158
- Laptev, I., 294
- LeCun, Y., xiv, 295
- Lee, J., 269
- Lee, K., 149
- Lee, T., 74
- Levine, M., 72
- Levialdi, S., 139
- Li, S., 109
- Liang, P., 215
- Lindeberg, T., 71, 278, 294
- Liu, C., 115
- Lloyd, S., 159
- Longuet-Higgins, C., 317
- Lopez, D., 215
- Lorente, N., 275, 276
- Luo, Y., 76
- Lutton, E., 215
- Maeapna, T., 294
- Maitre, H., 215
- Malik, J., 69, 85, 188
- Malladi, R., 194
- Mart, D., 60
- Mart, T., 72
- Martin, D., 193
- Mason, J. W., 8
- McCulloch-Pitts, 8
- McLean, G., 215
- McMillan, L., 115
- Meer, P., 149, 163
- Meijster, A., 182
