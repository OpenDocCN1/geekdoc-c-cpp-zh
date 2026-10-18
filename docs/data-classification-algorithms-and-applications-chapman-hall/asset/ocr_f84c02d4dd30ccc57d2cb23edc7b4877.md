after completion of the learning scheme, and that value can be used to provide a bound on the error rate. Note that the bound does depend on the dimensionality of the input data, making the perceptron applicable to large-dimensional data. To remove dependency on $D$, it is common to normalize each training data by $\frac{\mathbf{x}_n}{\|\mathbf{x}_n\|}$, which produces the bound of the form $\frac{1}{\gamma^2}$.

# 8.3.1.2  Multi-Class Perceptrons

The original perceptron algorithm deals with a two-class problem and uses a single output unit with a threshold activation. For classification problems with $K > 2$ classes, $C_1,\cdots,C_K$, the perceptron features $K$ output units in the output layer, with one output unit per class, and all output units getting the same input data. Each output $j$ has its own set of weights $\mathbf{w}_j$. This is equivalent to a multi-class linear machine [35, 104], where the $j$-th output unit implements a linear discrimination function for class $C_j$. For an input data $\mathbf{x}=(1,x_1,\cdots,x_d)$, each output unit $j$ computes a net value $v_j=\mathbf{w}_j^t\mathbf{x}$ and an output value $o_j=v_j$, where column-vector $\mathbf{w}_j=(w_{0j},w_{1j},\cdots,w_{dj})$ is the set of weights with $w_{ij}$ representing the connection between the $i$-th input unit, and the $j$-th output unit and $w_{0j}$ is a bias. In contrast to the two-class perceptron, output units are linear units; threshold activations are not used. The use of linear activation allows for a gradual comparison of the scores produced by the outputs, which is not possible with threshold units producing either $-1$ or $1$.

Classification is done by selecting the class of the output unit that yields the highest output value:

$$\mathbf{x}\in C_k \quad \text{if } k=\underset{j}{\arg\max}\,o_j.$$  (8.25)

Supervised training of the multi-class perceptron is aimed at generating a positive value $o_k$ if the input data belongs to the representative category $C_k$ and a negative value if the input data belongs to a category other than $C_k$. To achieve this outcome, the multiclass perceptron learning implements a competitive learning scheme whenever there is misclassification. Given training data $X=\{\mathbf{x}_1,\cdots,\mathbf{x}_N\}$ with associated desired outputs $\mathbf{t}_n=(t_{n1},\cdots,t_{nK})$ with $t_{nj}$ encoded using the principle of 1-of-K in the set $\{-1,1\}$ as

$$t_{nk}=\begin{cases}1 & \text{if }\mathbf{x}_n\in C_k\\-1 & \text{otherwise,}\end{cases}$$  (8.26)

then, for an input data $\mathbf{x}_n$ of the class $C_k$ that generates an output $o_k$ the multi-class perceptron performs an update whenever $o_k$ is misclassified as a class $C_q$:

$$\mathbf{w}_j\leftarrow\mathbf{w}_j+\eta t_{nj}\mathbf{x}_n\quad\text{for }j\in\{k,q\}.$$  (8.27)

Similar to the two-class case, the update occurs only when the input data have been misclassified. The effect is to increase the weight of the output vector of the right category $(\mathbf{w}_k\leftarrow\mathbf{w}_k+\eta\mathbf{x}_n)$ and decrease the weight of competing category $\mathbf{w}_q\leftarrow\mathbf{w}_q-\eta\mathbf{x}_n$. The multi-class perceptron learning is shown in Algorithm 8.2.

# 8.3.1.3  Perceptron Enhancements

The perceptron is essentially a linear discrimination machine. Performance is guaranteed only for linearly separable classification problems within a finite number of iterative steps [35, 114]. Also, the perceptron is very sensitive to noise, which severely limits its performance in real-world scenarios.

The use of a margin $\gamma$ as a tradeoff in performance enables us to adapt the perceptron to challenging non-linear scenarios. To overcome some learning issues encountered by the original perceptron in noisy settings, more robust variants of the perceptron learning have been proposed. The pocket algorithm [44] keeps a buffer of good weights in a ”pocket” during the learning process and uses