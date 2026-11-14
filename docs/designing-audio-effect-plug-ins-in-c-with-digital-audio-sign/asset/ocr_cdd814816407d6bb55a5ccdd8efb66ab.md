Taking the z transform:

Y(z) = a_0 X(z) + a_1 X(z) z^{-1}
Y(z) = X(z) [a_0 + a_1 z^{-1}]
H(z) = \frac{Y(z)}{X(z)} = a_0 + a_1 z^{-1}

This is a really useful result—you got the final transfer function in just a handful of steps, using the simple z transform rules. Let's recap what you had to do before you learned how to take the z transform of a difference equation:

+   - Redraw the block diagram with \( e^{-j\omega n} \) operators in the \( n \)-sample delay elements.
+   - Apply the complex sinusoid \( e^{-j\omega t} \) to the input.
+   - Find out what comes out, \( y(t) \), and formulate the transfer function \( H(\omega) \).
+   - Apply the \( z \) substitution to the transfer function.

Taking the z transform does all these steps at once and we're left with the same simple polynomial in \( z \). If we evaluate the transfer function for different values of \( z = e^{j\omega} \), we can find the frequency and phase plots. You'll get more practice taking the z transforms of more difference equations soon.

# 5.11 The z Transform of an Impulse Response

The z transform of a difference equation results in the transfer function. But what if you don't have the difference equation? Suppose you only have a black box that performs some kind of DSP algorithm and you'd like to figure out the transfer function, evaluate it, and plot the frequency and phase responses. It can be done without knowing the algorithm or any details about it by taking the impulse response of the system. You apply the input sequence \( x(n) = \{1, 0, 0, 0, 0, ...\} \) and capture what comes out, which we'll call \( h(n) \). If you take the z transform of the impulse response, you get the transfer function expanded out into a series form.

In fact, this is exactly what the RackAFX software's audio analyzer does—it takes the impulse response of the filter and then runs a z transform on it to make the magnitude and phase plots you see on the screen. Mathematically, Equation 5.31 is identical to Equation 5.26 except we've changed the signal from X to H:

> The z transform of the impulse response h(n) is the transfer function H(z) as a series expansion. Evaluate the transfer function to plot the frequency and phase responses.