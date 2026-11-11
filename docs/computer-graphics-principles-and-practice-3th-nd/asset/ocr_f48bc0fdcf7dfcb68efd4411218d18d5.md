transform looks like the box function \(b\). Unfortunately, it’s impossible for a function \(f \in L^2(\mathbb{R})\) to have finite support and have \(\hat{f}\) also have finite support [DM85]. But we can find finitely supported filters whose transforms are nearly zero outside a small interval, as we’ll discuss presently. If we agree to replace sinc by such a filter, then the whole question of whether the extension of the source image is \(L^2\) disappears: We can simply extend the source image by an amount \(R\) that’s greater than the support of the filter, and then fill in with zeroes beyond there. This is option 4, listed above.

Finally, option 5 presents one last approach that’s somewhat unprincipled, but works well in practice. When we compute the value for a pixel with a summation of the form

\[\operatorname{target}(j)=\sum_i \operatorname{source}(i)\operatorname{sinc}(j-i), \qquad (19.7)\]

we’re computing a weighted sum of source pixels. In this particular case, the weights come from the sinc function, but more generally we’re computing something of the form

\[\operatorname{target}(j)=\sum_i \operatorname{source}(i)w(j-i), \qquad (19.8)\]

where \(w\) is a list of weights. If these weights don’t sum to one, then filtering a constant image results in an image whose values are different from that constant. An example, based on filtering in the horizontal direction with a truncated sinc, is shown in Figure 19.8. The constant signal is shown in blue; it was sampled at integer points and reconstructed with \(x \mapsto 1.4\operatorname{sinc}(1.4x)\), truncated for \(|x| > 3.5\). The resultant function was sampled far more finely and plotted in green, showing substantial ripple.

Typically, for things like a truncated sinc, the sum \(W\) of the weights is very close to one at each pixel. The sum may vary from one pixel to the next, however, resulting in a ripple when we try to reconstruct a constant image, as the figure shows. We can fix this problem somewhat by dividing by the sum of the weights at each pixel, which removes the ripple. In effect, we’ve altered the filter so that its Fourier transform is zero at all multiples of the sampling frequency. We’ve

![](bbox=[0.197, 0.678, 0.677, 0.922])