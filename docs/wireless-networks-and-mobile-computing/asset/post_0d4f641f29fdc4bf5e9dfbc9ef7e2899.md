
The transmission protocol of TSS thus consists of two steps:

## Protocol TransmitTSS

- **Step 1:** Recode the binary data to ternary using the *Binary2Ternary* protocol.
- **Step 2:** Transmit the ternary data symbol by symbol, obtained by the recoding process from step 1 using the following rules:
  - **Step 2.1:** If the symbol to be transmitted is 0, then switch off the transmitter for the symbol period.
  - **Step 2.2:** Otherwise, switch on the transmitter and transmit the symbol (1 or 2) in the time slot.

The receiver side protocol would be the reverse of that for the transmitter:

## Protocol ReceiveTSS

- **Step 1:** Receive the ternary encoded data symbol by symbol as follows:
  - **Step 1.1:** If a signal is received in the given time slot (symbol period), the received symbol is either a 1 or a 2, depending on the predetermined received signal-to-symbol mapping.
  - **Step 1.2:** Otherwise, if the channel is quiet, the received symbol is a 0.
- **Step 2:** Convert the received ternary message to binary using the *Ternary2Binary* protocol.

## 8.4.2 Performance Analysis

The TSS transmission scheme involves the recoding of an outgoing binary message to its equivalent ternary form and transmitting it. The receiver then reconverts the received ternary data to binary and passes it onto the higher layers of the communication stack for further processing.

The transmitter uses FSK modulation with two frequencies, such as $f_c$ and $f_c + \Delta f$ corresponding to the symbols 1 and 2, respectively, and is switched to *idle* state during the 0’s, when it consumes very little power compared to the *transmit* or *receive* state. Effectively, this is a hybrid modulation scheme involving FSK and ASK.

The receiver diagram as shown in Figure 8.10 for RBNSiZeComm can also be used for the TSS scheme based on non-coherent detection and the frequencies $f_c$ and $f_c + \Delta f$ will correspond to the symbols 1 and 2, respectively. Also, $q_A$ and $q_B$ will now be the binary outputs of the threshold detectors corresponding to the symbols 1 and 2, respectively. Thus, in this case, the desired output $\hat{s}$ of the receiver can be expressed as follows:

- i) If $q = 0$, $\hat{s} = 0$, corresponding to $s_A = s_B = 0$.
- ii) If $q = 1$,

$$\hat{s} = \begin{cases} 1 & \text{if } e_A > e_B,\ (\text{when } s_A = 1, s_B = 0) \\ 2 & \text{if } e_B > e_A,\ (\text{when } s_B = 1, s_A = 0). \end{cases}$$

We consider a message frame containing $n$ binary bits. Corresponding to each such frame, we consider the message frame after converting the binary to ternary form containing symbols 0, 1 and 2, and having a length of $m$ digits, where $n$ and $m$ are related as $m = \lceil n \log 2 / \log 3 \rceil = \lceil 0.6309n \rceil$.

For performing the energy saving analysis of the TSS scheme, again the conventional bit error rate (BER) will not be suitable. Instead, the frame error rate (FER) will be used as in RBNSiZeComm scheme. BER has the limitation that the propagation of errors over the higher significant digits due to an erroneously received ternary symbol cannot be captured appropriately since it considers the transmission of each bit independent of the other bits. It may be noted that due to the nature of ternary (and also other radix encodings that are not powers of 2), the number of higher significant bits in the original binary number through which an error at a received digit position (in the higher radix) will propagate is difficult to predict. This is because the conversion from binary to such a radix involves *carry propagation* from lower order digits to higher order digits. When using a radix that is a power of 2, say $2^k$ for $k > 1$, such carry propagations do not occur as the equivalent digit in the new radix of $2^k$ can be obtained by simply grouping successive $k$ bits from the least significant bit position, independent of the other bits.

Consider as an example the transmission of the binary number $(0111111)_2 = (63)_{10}$ using ternary encoding. The ternary representation of $(63)_{10}$ is $(2100)_3$. If the least significant digit of this ternary number, i.e., 0, is wrongly interpreted at the receiver as 1, the received binary number after decoding will be $(1000000)_2$, representing a propagation of error from the least significant bit to the most significant bit position. A BER-based error analysis would not be able to capture such *ripple effects* (on the original binary number) of error in interpreting a single digit (in radix other than power of 2) at the receiver.

The FER-based error analysis overcomes the limitation of BER-based error analysis in capturing the transitive nature of error propagation to the higher significant bit positions of the decoded binary number, caused by a single digit error in the received ternary data. Although we show the error analysis of only the TSS scheme based on FER, this concept of FER-based error analysis is generally applicable to any transmission scheme that uses recoding of binary data to another radix which is not a power of 2 for the reason mentioned above. We now describe the error analysis of the TSS scheme using both non-coherent and coherent receiver designs.

## 8.4.3 Non-coherent Detection

In this section, we compare the FER of communicating a binary data frame using non-coherent BFSK, with the FER of communicating the equivalent ternary data in the TSS scheme using a receiver based on non-coherent detection as shown in Figure 8.10.

In the hybrid FSK-ASK modulation scheme, let $\alpha$ be the probability that a transmitted ternary symbol was a 0 and was received correctly as a 0. Similarly, let $\beta$ (or $\delta$) be the probabilities that a transmitted symbol was a 1 (or 2) and the received symbol is also a 1 (or 2). From symmetry, $\beta = \delta$. Note that $\alpha = P\{q_A = 0|0\}\cdot P\{q_B = 0|0\}$, where $P\{q_A = 0|0\}$ and $P\{q_B = 0|0\}$ are the probabilities of correctly receiving a 0 at $q_A$ and $q_B$, respectively, given that a 0 was transmitted. Hence,

$$\alpha = P\{q_A=0|0\}\cdot P\{q_B=0|0\} = [P\{q_A=0|0\}]^2 \quad \text{(by symmetry).} \tag{8.19}$$

Also, note that $q_A$ for 0 transmission follows Rayleigh distribution. Assuming a zero mean and a standard deviation of $\sigma$ for AWGN channel, we can write

$$P\{q_A=0|0\}=\int_0^{e_{th}} \frac{e_A}{\sigma^2}e^{-e_A^2/2\sigma^2}\,de_A = (1-e^{-e_{th}^2/2\sigma^2}).$$

Hence, we have $\alpha = (1 - e^{-e_{th}^2/2\sigma^2})^2$. Next, we define $\beta$ as

$$\beta = P\{q=1|1\}P\{e_A>e_B,\forall e_A|1\}=X_1X_2 \quad \text{(say)},$$

where $X_1 = P\{q = 1|1\}$ and $X_2 = P\{e_A > e_B|1, \forall e_A|1\}$. From Figure 8.10, we write:

$$X_1=\int_0^\infty [1-P\{q_A=0|1\}P\{q_B=0|1\}]p_1(e_A)\,de_A,$$

where $P\{q_B=0|1\}$ is governed by a Rayleigh distribution, while $P\{q_A=0|1\}$ represents a Rician distribution. Thus,

$$P\{q_A=0|1\}=\int_0^{e_{th}}\frac{e_A}{\sigma^2}e^{-\frac{e_A^2+s_A^2}{2\sigma^2}}I_0\left(\frac{s_Ae_A}{\sigma^2}\right)de_A\quad\text{and,}$$
$$P\{q_B=0|1\}=\int_0^{e_{th}}\frac{e_B}{\sigma^2}e^{-e_B^2/2\sigma^2}\,de_B=1-e^{-e_{th}^2/2\sigma^2}.$$

Using the above expressions, we obtain $X_1$ and $X_2$ as

$$X_1=\int_0^\infty\left[1-\left(1-e^{-e_{th}^2/2\sigma^2}\right)\left(\int_0^{e_{th}}\frac{e_A}{\sigma^2}e^{-\frac{e_A^2+s_A^2}{2\sigma^2}}I_0\left(\frac{s_Ae_A}{\sigma^2}\right)de_A\right)\right]\frac{e_A}{\sigma^2}e^{-\frac{e_A^2+s_A^2}{2\sigma^2}}I_0\left(\frac{s_Ae_A}{\sigma^2}\right)de_A.\tag{8.20}$$

$$X_2=\int_0^\infty\left[\left(1-e^{-e_A^2/2\sigma^2}\right)\frac{e_A}{\sigma^2}e^{-\frac{e_A^2+s_A^2}{2\sigma^2}}I_0\left(\frac{s_Ae_A}{\sigma^2}\right)u(e_A)\right]de_A.\tag{8.21}$$

Let $P_0$, $P_1$ and $P_2$ be the probabilities of occurrences of the symbols 0, 1 and 2, respectively, in a transmitted message. The probability that the transmitted ternary frame with $m$ ternary digits will be received correctly by the above hybrid FSK-ASK scheme can be expressed as the *frame-correct rate* (FCR), given by:

$$FCR=\alpha^{mP_0}\times\beta^{mP_1}\times\delta^{mP_2}.\tag{8.22}$$

Assuming that all possible binary strings with $n$ bits are equally likely to appear in the binary message, the average number of 0’s in the ternary frame will be asymptotically (for large $n$) 33% and those of all non-zero symbols, i.e., 1 and 2 taken together, will be 67%. Thus, $P_0=0.33$ and $P_1+P_2=0.67$. The probability
