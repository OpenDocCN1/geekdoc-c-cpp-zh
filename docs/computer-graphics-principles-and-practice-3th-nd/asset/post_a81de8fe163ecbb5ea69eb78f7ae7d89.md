
For the remainder of the chapter, we’re motivated by the question, “Suppose we have incoming light arriving at a sensor, and we want to make an image that best captures this arriving light for subsequent display or other uses; what should we store in the image array?” To answer this question, we need to do two things.

- Choose a new basis in which to represent images.
- Understand how convolution “looks” in this new basis.

The Fourier transform is how we’ll transform images into the new basis. And in the new basis, convolution of functions becomes multiplication of functions, which is much easier to understand and reason about.

### 18.9.1 Frequency-Based Synthesis and Analysis

Consider the interval H = (−1/2, 1/2], which we’ll use throughout this chapter; the letter “H” is mnemonic for “half.” By writing a sum like

$$f(x) = \cos(2\pi x) + (1/3) \cos(6\pi x), \tag{18.28}$$

![](img/f464cd0043eb5336aa0543fe20a0561b_559_0.png)

shown in Figure 18.28, we can produce an even function on that interval (i.e., one symmetric about the y-axis). In general, any sum of cosines of various integer frequencies will be an even function, because each component cosine is even. By changing how much of each frequency of cosine we mix in, we can get many different functions.

We can, for instance, find a combination of cos(0x), cos(2πx), and cos(4πx) that satisfies f(0) = 1, f(1/6) = 0, and f(1/3) = 0. These constraints are shown in Figure 18.29; the shaded constraints on the left are there because the function is even, so its values on the left half of the real line must match those on the right half of the line.

We write

$$f(x) = a \cos(0x) + b \cos(2\pi x) + c \cos(4\pi x), \tag{18.29}$$

and then plugging in the constraints, we find that

$$1 = f(0) = a + b + c, \tag{18.30}$$
$$0 = f(1/6) = a + b \cos(\pi/3) + c \cos(2\pi/3) \tag{18.31}$$
$$= a + b/2 − c/2, \text{ and} \tag{18.32}$$
$$0 = f(1/3) = a − b + c. \tag{18.33}$$

![](img/f464cd0043eb5336aa0543fe20a0561b_559_1.png)

From which we can determine that a = 0 and b = c = 1/2 (see Figure 18.30).

![](img/f464cd0043eb5336aa0543fe20a0561b_559_2.png)

This is easy to generalize: If we’re given k constraints on the values of a function on the non-negative part of the interval I, then we can find a function written as a linear combination of cos(0x), cos(2πx), …, cos(2π(k − 1)x) that satisfies those constraints. The proof relies on elementary properties of the cosine and sine.

Thus, we can “synthesize” various even functions by summing up cosines of many frequencies. We can even “direct” our synthesized function to have certain values at certain points, as in the second example above. We can synthesize odd functions by summing up sines of various frequencies as well, and by mixing sines and cosines, we can even synthesize functions that are neither even nor odd.

Whatever function we synthesize, however, will be periodic of period 1, because each term in the sum is periodic with that period. Thus, if $f$ is a sum of sines and cosines of different integer frequencies, we’ll have $f(\frac{1}{2})=f(-\frac{1}{2})$.

We’re using the term “frequency” here quite specifically: We say that $x\mapsto\cos(2\pi x)$ is a function of frequency 1. Some other texts say that $x\mapsto\cos(x)$ is a function of frequency 1. In the same way, some books prefer to define the Fourier transform on the interval $[-1,1]$, or $[0,1]$, or $[0,2\pi]$; depending on the interval, this introduces a multiplicative constant in the definition of the inner product. We’re following the convention of Dym and McKean [DM85] so that the interested reader may refer there for proofs, but there is no universal standard. Fortunately for us, we’ll mostly be concerned with qualitative properties of the Fourier transform, for which the interval of definition and multiplicative constants are not important.

![](img/f464cd0043eb5336aa0543fe20a0561b_560_0.png)

More surprising, perhaps, is that any even continuous function $f$ on the interval $H$ that satisfies $f(\frac{1}{2})=f(-\frac{1}{2})$ can be written as a sum of cosines of various integer frequencies. Even discontinuous functions can be almost written as such a sum. For instance, the square-wave function (see Figure 18.31) defined by

$$f(x)=\begin{cases}1 & -\frac{1}{4}\le x\le\frac{1}{4}\\-1 & \text{otherwise}\end{cases}\tag{18.34}$$

can be almost expressed by the infinite sum

$$\bar f(x)=\frac{4}{\pi}\left(\cos(2\pi x)-\frac{\cos(6\pi x)}{3}+\frac{\cos(10\pi x)}{5}-\cdots\right)\tag{18.35}$$
$$=\sum_{k=0}^{\infty}\frac{4}{\pi(2k+1)}(-1)^k\cos(2\pi(2k+1)x).\tag{18.36}$$

We say “almost expressed” because $\bar f(\pm\frac{1}{4})=0$—the average of the values of $f$ to the left and right of $\pm\frac{1}{4}$—rather than being equal to $f(\pm\frac{1}{4})=1$.

The sequence in Equation 18.35 can be approximated by taking a finite number of terms; a few of those approximations are shown in Figure 18.32.

As a more graphically oriented example, let’s take one row of pixels from a symmetric image like that shown in Figure 18.33. We’ve actually taken half a row and flipped it over to get a perfectly symmetric line of 3,144 pixels, shown in Figure 18.34.

![](img/f464cd0043eb5336aa0543fe20a0561b_560_1.png)

If we write this function as a sum of cosines, the sum will have 3,144 terms, which is hard to read. It starts out as

$$f(x)=129.28\cos(0x)+5.67\cos(2\pi x)-2.35\cos(4\pi x)+\cdots\tag{18.37}$$

We can make an abstract picture of this summation by plotting the coefficients: At 0 we plot 129.28, at 1 we plot 5.67, at 2 we plot −2.34, etc. The result is shown in Figure 18.35, except that since the coefficient of $\cos(0x)$ is actually 141.8, we’ve adjusted the $y$-axis so that you can see the other details, thus hiding the large coefficient for the $\cos(0x)$ term. (That coefficient is just the average of all the pixel values.)

Notice that as the frequencies get higher, the coefficients get smaller. In fact, in natural images, this “falling off with higher frequencies” is commonplace. Notice too that the function shown in Figure 18.34 has lots of variation at a very small scale, while the one shown in Figure 18.28 has variation only at a very large scale. If we made a plot for Figure 18.28 analogous to Figure 18.35, it would have only two nonzero values (at frequencies 0 and 1). In general, details at small scales mean there must be high frequencies in the image, just as we observed in Section 18.11. Since x ↦ cos(2πkx) has “features” at a scale of 1/(2k), in general any sum that stops at the cos(2πkx) term will have no features smaller than 1/(2k). This kind of relationship between the pattern of coefficients and the appearance of the pixel-value plot is a powerful reasoning tool. We’ll next formalize it using the Fourier transform.

But first, it’s useful to understand how the frequency decomposition of an image actually looks, so Figure 18.36 shows these to you, for a grayscale version of the Taj Mahal image (again, symmetrized). The frequency-0 part of the image is the average grayscale value; we’ve actually included this in both the middle- and high-frequency images to prevent having to use values less than 0.

## 18.10 The Fourier Transform: Definitions

In the next two sections we’ll define several different Fourier transforms, all of them closely related. We’ll only hint at the proofs of various claims, and instead rely mostly on suggestive examples. As motivation for you as you read these sections, here are the three main features of the Fourier transform that we’ll use in applications to computer graphics.

- The Fourier transform turns convolution into multiplication, and vice versa. If we write $F$ for the Fourier transform, this means that

  $$F(f * g) = F(f)F(g)$$ (18.38)

  $$F(fg) = F(f) * F(g)$$ (18.39)

- If we define a function $g$ like the one shown in Figure 18.37, with peaks that are equally spaced and very narrow, then the Fourier transform of $g$ looks rather like $g$ itself, except that the closer the spacing of the peaks in $g$, the wider the spacing of the peaks in the transform.
- Multiplying a function $f$ by a function like $g$ approximates “sampling $f$ at equispaced points.” Thus, functions like $g$ can be used to study the effects of sampling. Because of the convolution-multiplication duality, we’ll see that the sampled function has a Fourier transform that’s a sum of translated replicates of the original function’s transform.

## 18.11 The Fourier Transform of a Function on an Interval

We hinted in Section 18.9.1 that if we had an even function in $L^2(H)$, then its Fourier transform was the set of coefficients used to write the function as a sum of cosines. In general, however, the Fourier transform is defined for any $L^2$ function,

![](img/f464cd0043eb5336aa0543fe20a0561b_561_0.png)

*Figure 18.33:* The Taj Mahal. Original image by Jbarta, at http://upload.wikimedia.org/wikipedia/commons/b/bd/Taj_Mahal,_Agra,_India_edit3.jpg.

![](img/f464cd0043eb5336aa0543fe20a0561b_561_1.png)

*Figure 18.34:* The grayscale pixel values for one horizontal line of the image.

![](img/f464cd0043eb5336aa0543fe20a0561b_561_2.png)

*Figure 18.35:* The first few coefficients for sum representing the row of Taj Mahal pixels. We plot the coefficient of cos(2πkx) at position k.
