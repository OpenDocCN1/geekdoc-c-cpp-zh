Exercise 63 Let $\mathcal{C}$ be the Hamming code $\mathcal{H}_3$ of Example 1.2.3, with parity check matrix
$$H = \begin{bmatrix} 0 & 1 & 1 & 1 & 1 & 0 & 0 \\ 1 & 0 & 1 & 1 & 0 & 1 & 0 \\ 1 & 1 & 0 & 1 & 0 & 0 & 1 \end{bmatrix}.$$

+   (a) Construct the generator matrix for $\mathcal{C}$ and use it to encode the message 0110.

+   (b) Use your generator matrix to encode $x_1 x_2 x_3 x_4$.

+   (c) Use $H$ to encode the messages $0110$ and $x_1 x_2 x_3 x_4$.

Since there is a one-to-one correspondence between messages and codewords, one often works only with the encoded messages (the codewords) at both the sending and receiving end. In that case, at the decoding end in Figure 1.1, we are satisfied with an estimate $\hat{\mathbf{c}}$ obtained by the decoder from $\mathbf{y}$, hoping that this is the codeword $\mathbf{c}$ that was transmitted. However, if we are interested in the actual message, a question arises as to how to recover the message from a codeword. If the codeword $\mathbf{c} = \mathbf{x}G$, and $G$ is in standard form, the message is the first $k$ components of $\mathbf{c}$; if the encoding is systematic, it is easy to recover the message by looking at the coordinates of $G$ containing the identity matrix. What can be done otherwise? Because $H$ has independent rows, there is an $n \times k$ matrix $K$ such that $GK = I_k$; $K$ is called a right inverse for $G$ and is not necessarily unique. As $\mathbf{c} = \mathbf{x}G$, $\mathbf{c}K = \mathbf{x}GK = \mathbf{x}$.

Exercise 64 Let $G$ be a $k \times n$ generator matrix for a binary code $\mathcal{C}$.

+   (a) Suppose $G = [I_k \ A]$. Show that
+   $$
+   \begin{bmatrix} I_k \\ O \end{bmatrix}.$$

where $O$ is the $(n-k) \times k$ zero matrix, is a right inverse of $G$.

+   (b) Find a $7 \times 3$ right inverse $K$ of $G$, where
+   $$G = \begin{bmatrix} 1 & 0 & 1 & 1 & 0 & 1 & 1 \\ 1 & 1 & 0 & 1 & 0 & 1 & 0 \\ 0 & 0 & 1 & 1 & 1 & 1 & 0 \end{bmatrix}.$$

Hint: One way $K$ can be found is by using four zero rows and the three rows of $I_3$.

+   (c) Find a $7 \times 4$ right inverse $K$ of $G$, where
+   $$G = \begin{bmatrix} 1 & 1 & 0 & 1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 1 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 & 1 & 0 & 1 \end{bmatrix}.$$

Remark: In Chapter 4, we will see that $G$ generates a cyclic code and the structure of $G$ is typical of the structure of generator matrices of such codes.

+   (d) What is the message $\mathbf{x}$ if $\mathbf{x}G = 1000110$, where $G$ is given in part (c)?