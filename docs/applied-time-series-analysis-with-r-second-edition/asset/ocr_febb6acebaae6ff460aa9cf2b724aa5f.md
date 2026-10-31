to denote the operator 1 - B, we have

$$\alpha'^t \nabla \alpha^{-t} X_t \equiv (1 - \alpha B) X_t.$$

So,

$$\alpha_1^t \nabla\left(\frac{\alpha_2}{\alpha_1}\right)^t \nabla \alpha_2^{-t} X_t = (1 - \alpha_1 B)(1 - \alpha_2 B) X_t,$$

and it follows that

$$\nabla\left(\frac{\alpha_2}{\alpha_1}\right)^t \nabla \alpha_2^{-t} X_t = \alpha_1^{-t} a_t.$$

Then, summing both sides gives

$$\sum_{k=-\infty}^t \nabla\left(\frac{\alpha_2}{\alpha_1}\right)^k \nabla \alpha_2^{-k} X_k = \sum_{k=-\infty}^t \alpha_1^{-k} a_k,$$

so

$$\left(\frac{\alpha_2}{\alpha_1}\right)^t \nabla \alpha_2^{-t} X_t - \lim_{k\to -\infty} \left(\frac{\alpha_2}{\alpha_1}\right)^k \nabla \alpha_2^{-k} X_k = \sum_{k=-\infty}^t \alpha_1^{-k} a_k,$$

and

$$\lim_{k\to -\infty} \left(\frac{\alpha_2}{\alpha_1}\right)^k \nabla \alpha_2^{-k} X_k = 0,$$

with probability 1. Thus,

$$\nabla \alpha_2^{-t} X_t = \left(\frac{\alpha_1}{\alpha_2}\right)^t \sum_{k=-\infty}^t \alpha_1^{-k} a_k,$$

and similarly