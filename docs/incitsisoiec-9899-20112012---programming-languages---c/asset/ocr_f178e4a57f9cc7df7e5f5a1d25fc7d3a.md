distinguish$^{279}$ values of type **double**, except that zeros may be omitted; if the precision is zero and the # flag is not specified, decimal-point character appears. The letters **abcdef** are used a conversion and the letters **ABCDEF** for a conversion. The A conversion produces a number with **X** and **P** instead of **x** and **p**. The exponent always contains at least one digit, and as many as necessary to represent the decimal exponent of 2. If the value is zero, the exponent is zero.

A **double** argument representing an infinity or NaN is converted in the style of an **f** or **F** conversion specifier.

If no 1 length modifier is present, the **int** argument is converted to an **unsigned char**, and the resulting character is written.

If an 1 length modifier is present, the **wint_t** argument is converted as if an **ls** conversion specification with no precision and an argument points to the initial element of a two-element array of **wchar_t**, the first element containing the **wint_t** argument to the **lc** conversion specification and a second null wide character.

If no 1 length modifier is present, the argument shall be a pointer to the initial element of an array of character type.${280}$ Characters from the array are written up to (but not including) the terminating null character. If the precision is specified, no more than many bytes are written. If the precision is not specified or is greater than the size of the array, the array shall contain a null character.

If an 1 length modifier is present, the argument shall be a pointer to the initial element of an array of **wchar_t**. Wide characters from the array are converted to multibyte characters (each as by a call to the **wcrtomb** function, with the conversion state described by an **mbstate_t** object initialized to zero before the first wide character is converted) up to including a terminating null character. The resulting multibyte characters are written up to (but not including) the terminating null character (byte). If no precision is specified, no more than many bytes are written (including shift sequences, if any), and the array shall contain a null character if, equal to the multibyte sequence length given by

> 279) The precision $p$ is sufficient to distinguish values of the source type if $16^{p-1} > b^n$ where $b$ is **FLT_RADIX** and $n$ is the number of base-b digits in the significand of the source type. A smaller $p$ might suffice depending on the implementation's scheme for determining the digit to the left of the decimal-point character.

> 280) No specifications are made for multibyte characters.