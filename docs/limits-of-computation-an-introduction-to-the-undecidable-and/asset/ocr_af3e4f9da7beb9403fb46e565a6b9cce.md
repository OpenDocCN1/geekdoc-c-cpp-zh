$L_2 = \{1, 010, 00100, 000100, \dots\}$

$L_1 = \{\varepsilon, 00, 0000, 000000,, \dots\}$

We can also use either of the above notations for finite languages if we wish to stress the structure of their component strings.

The smallest language over any alphabet $\Sigma$ is $L_{\emptyset} = \{\}$\}$, with no strings whatsoever (the language has zero strings, or $|L_{\emptyset}| = 0$). This is distinct from any small language, $L_{\varepsilon} = \{\varepsilon\}$, a language with exactly one string in the language ($|L_{\varepsilon}| = 1$). Remember this distinction! The string $\varepsilon$ is not "nothing"; it is indeed a real string, just one with no symbols in it.

# 2. OPERATIONS ON STRINGS

There are many operations that can be done on strings—simple one, others more complicated.

The **reversal** of a string $w = \sigma_1\sigma_2 \dots \sigma_n$ (written $w^R$) is obtained by placing its characters in the opposite order, $w^R = \sigma_n\sigma_{n-1} \dots \sigma_1$. Note that the lengths are the same, $|w| = |w^R|$.

# Examples

$(abc)^R = cbba$

$(00111)^R = 11100$

$(abba)^R = abba$

$\varepsilon^R = \varepsilon$

The **concatenation** of two strings $u = \sigma_1\sigma_2 \dots \sigma_n$ and $v = \tau_1\tau_2 \dots \tau_m$ (write $uv$, $u v$, or sometimes as $u \times v$) is the string obtained by appending $v$ onto the end of $u$, as $\sigma_1\sigma_2 \dots \sigma_n\tau_1\tau_2 \dots \tau_m$.

The length $|uv| = |u| + |v|$.

# Examples

Consider the following strings over $\Sigma = \{0, 1\}:

$w = 000$