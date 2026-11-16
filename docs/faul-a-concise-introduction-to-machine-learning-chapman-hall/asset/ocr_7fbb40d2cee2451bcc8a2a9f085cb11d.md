The likelihood of \(\mathbf{v} \in C_i\), given that we know its features \(\mathbf{v}\) is:

\(\mathcal{L}(\mathbf{v} \in C_i | \mathbf{v}) = \frac{1}{\sqrt{(2\pi)^M |\mathbf{\Sigma}_i|}} \exp \left( -\frac{1}{2} (\mathbf{v} - \mathbf{\mu}_i)^T \mathbf{\Sigma}_i^{-1} (\mathbf{v} - \mathbf{\mu}_i) \right)\)

It is the same formula, but a different interpretation.

A classifier can be built by assigning \(\mathbf{v}\) to class \(C_0\) if the likelihood of it belonging to \(C_0\) is larger than the likelihood of it belonging to \(C_1\). The boundary between the classes is given by

\(\mathcal{L}(\mathbf{v} \in C_0 | \mathbf{v}) = \mathcal{L}(\mathbf{v} \in C_1 | \mathbf{v}).\)

This is often expressed as likelihood ratio

\(\frac{\mathcal{L}(\mathbf{v} \in C_0 | \mathbf{v})}{\mathcal{L}(\mathbf{v} \in C_1 | \mathbf{v})} = \frac{\sqrt{(2\pi)^M |\mathbf{\Sigma}_1|} \exp \left( -\frac{1}{2} (\mathbf{v} - \mathbf{\mu}_0)^T \mathbf{\Sigma}_0^{-1} (\mathbf{v} - \mathbf{\mu}_0) \right)}{\sqrt{(2\pi)^M |\mathbf{\Sigma}_0|} \exp \left( -\frac{1}{2} (\mathbf{v} - \mathbf{\mu}_1)^T \mathbf{\Sigma}_1^{-1} (\mathbf{v} - \mathbf{\mu}_1) \right)} = 1.\)

Taking the logarithm, we arrive at

\(\log \frac{\mathcal{L}(\mathbf{v} \in C_0 | \mathbf{v})}{\mathcal{L}(\mathbf{v} \in C_1 | \mathbf{v})} = \frac{1}{2} \log \frac{|\mathbf{\Sigma}_1|}{|\mathbf{\Sigma}_0|} - \frac{1}{2} (\mathbf{v} - \mathbf{\mu}_0)^T \mathbf{\Sigma}_0^{-1} (\mathbf{v} - \mathbf{\mu}_0) + \frac{1}{2} (\mathbf{v} - \mathbf{\mu}_1)^T \mathbf{\Sigma}_1^{-1} (\mathbf{v} - \mathbf{\mu}_1) = \frac{1}{2} \left( \log \frac{|\mathbf{\Sigma}_1|}{|\mathbf{\Sigma}_0|} + \mathbf{\mu}_1^T \mathbf{\Sigma}_1^{-1} \mathbf{\mu}_1 - \mathbf{\mu}_0^T \mathbf{\Sigma}_0^{-1} \mathbf{\mu}_0 \right) + \mathbf{v}^T \left( \mathbf{\Sigma}_0^{-1} \mathbf{\mu}_0 - \mathbf{\Sigma}_1^{-1} \mathbf{\mu}_1 \right) + \frac{1}{2} \mathbf{v}^T \left( \mathbf{\Sigma}_1^{-1} - \mathbf{\Sigma}_0^{-1} \right) \mathbf{v} = 0.\)

Thus the boundary between classes is given by a quadratic of the form

\(\mathbf{v}^T \mathbf{A} \mathbf{v} + \mathbf{v}^T \mathbf{b} + c = 0\)

with

+   \mathbf{A} = \frac{1}{2} \left( \mathbf{\Sigma}_1^{-1} - \mathbf{\Sigma}_0^{-1} \right),\n\mathbf{b} = \mathbf{\Sigma}_0^{-1} \mathbf{\mu}_0 - \mathbf{\Sigma}_1^{-1} \mathbf{\mu}_1,\nc = \frac{1}{2} \left( \log \frac{|\mathbf{\Sigma}_1|}{|\mathbf{\Sigma}_0|} + \mathbf{\mu}_1^T \mathbf{\Sigma}_1^{-1} \mathbf{\mu}_1 - \mathbf{\mu}_0^T \mathbf{\Sigma}_0^{-1} \mathbf{\mu}_0 \right).

This is the *Quadratic Discriminant Analysis (QDA)*.

In the special case of two features, the boundaries are conic sections, that is a line, circle, ellipse, parabola or hyperbola. The MATLAB code in Listing 5.1 applies the Quadratic Discriminant Analysis to MATLAB's iris data and the result can be seen in Figure 5.1.

Recall that we arrived at the Linear Discriminant Analysis by assuming \(\mathbf{\Sigma}_0 = \mathbf{\Sigma}_1 = \mathbf{\Sigma}\). In this case,

+   \mathbf{A} = 0,\n\mathbf{b} = \mathbf{\Sigma}^{-1} (\mathbf{\mu}_0 - \mathbf{\mu}_1),\nc = \frac{1}{2} \left( \mathbf{\mu}_1^T \mathbf{\Sigma}^{-1} \mathbf{\mu}_1 - \mathbf{\mu}_0^T \mathbf{\Sigma}^{-1} \mathbf{\mu}_0 \right).