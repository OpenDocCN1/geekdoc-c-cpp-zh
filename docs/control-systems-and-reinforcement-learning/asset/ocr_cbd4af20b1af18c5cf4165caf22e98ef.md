# 1.1 What You Can Find in Here

![](bbox=[0.135, 0.093, 0.833, 0.243])

Figure 1.1 Maximum Bellman error ($\hat{B}_n : n \geq 0$) for various Q-learning algorithms [107].

+   (iii) Zap Q-learning will be one of many algorithms described in the book. It is a particular ODE design based on the Newton-Raphson flow introduced in the economics literature, and first analyzed by Smale in the 1970s [325]. The Zap ODE is universally stable and consistent, and when translated to care, provides new techniques for RL design [89, 107, 110, 112]. The power of Zap design is illustrated in Figure 1.1 – Section 9.8.2 for details.

+   - Quasistochastic approximation. The theory of "stochastic approximation" amounts to justifying a discrete time algorithm based on an ODE approximation. An understanding of the general theory requires substantial mathematical background.

+   The reader will be introduced to stochastic approximation without any need to know the meaning of "stochastic." This is made possible by substituting mixtures of sinusoids for randomness, which is justified by an emerging science [11, 51, 52, 87, 93, 228]. Not only is this more accessible, but the performance in application to policy gradient methods in RL is remarkable.

+   The plots shown in Figure 1.2 are based on experiments described in Chapter 4, exploring using sinusoids versus random and identically distributed (i.i.d.) exploration. The histograms were generated over 1,000 independent experiments. The traditional approach labeled "IPSPA" requires additional training of many orders of magnitude when compared to quasistochastic approximation (QSA).

+   - Batch RL methods and convex Q-learning. One of the founders of AlphaGo admits that extension of these techniques is not trivial: "This approach won't work in ill-structured problems like natural-language understanding or robotics, where the state space isn't a clear objective function" [150].

+   In applications to controlling building systems, the energy grid, robotic surgery, or autonomous vehicles, we need to think carefully about more structured learning and control architectures, designed that we have a reliable outcome (hopefully with some guarantees on performance as well as the possibility of disaster). The basic RL engine of AlphaZero is deep Q-learning (DQN) [259–261]: a batch Q-learning method that is easily explained, and offers great flexibility to allow the inclusion of "insights from experts." Completely new in this book are convex-analytic approaches to RL that have a stronger supporting theory and can be designed to impose bounds on performance.