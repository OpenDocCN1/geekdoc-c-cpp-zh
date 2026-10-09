very close to 0.1. Similarly, setting a variable to a large number such as Avogadro's number, $6.02 \times 10^{23}$, could lead to a representation error of approximately $10^{8}$, which after all is a tiny fraction of that number. The accuracy of a floating-point number is in proportion to the magnitude of the number it represents. A floating-point number is precise to a certain number of significant digits, not by a fixed value such as $\pm 0.01$.

C# supports the two binary floating-point number types listed in Table 2.2.

**TABLE 2.2:** Floating-Point Types

| Type | Size | Range (Inclusive) | BCL Name | Significant Digits | Literal Suffix |
| :--- | :--- | :--- | :--- | :--- | :--- |
| *float* | 32 bits | $\pm 1.5 \times 10^{-45}$ to $\pm 3.4 \times 10^{38}$ | *System.Single* | 7 | F or f |
| *double* | 64 bits | $\pm 5.0 \times 10^{-324}$ to $\pm 1.7 \times 10^{308}$ | *System.Double* | 15–16 | |


Binary numbers appear as base 10 (denary) numbers for human readability. The number of bits (binary digits) converts to 15 decimal digits, with a remainder that contributes to a sixteenth decimal digit as expressed in Table 2.2. Specifically, numbers between $1.7 \times 10^{307}$ and less than $1 \times 10^{308}$ have only 15 significant digits. However, numbers ranging from $1 \times 10^{308}$ to $1.7 \times 10^{308}$ will have 16 significant digits. A similar range of significant digits occurs with the decimal type as well.

# ## Decimal Type

C# also provides a decimal floating-point type with 128-bit precision (see Table 2.3). This type is suitable for financial calculations.

**TABLE 2.3:** Decimal Type

| Type | Size | Range (Inclusive) | BCL Name | Significant Digits | Literal Suffix |
| :--- | :--- | :--- | :--- | :--- | :--- |
| *decimal* | 128 bits | $1.0 \times 10^{-28}$ to approximately $7.9 \times 10^{28}$ | *System.Decimal* | 28–29 | M or m |