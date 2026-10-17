for it. It is based on the probabilistic theory of a cue conflict discussed in the first section. Mathematically, this theory describes a mixture of prior assumptions that make cues informative. For the problem of finding binocular correspondence, one can model images as a mixture of at least two types of objects. One contains strong edges (e.g., outlines of objects and high contrast texture), and the other includes image regions with low-contrast intensities (e.g., uniform color of object surfaces and low contrast texture). For the first class of objects, we can use very informative edge cues, and for the second class of objects, the cues are less informative. According to the mixture of priors approach, we can express a full cue likelihood as

$$P(I\mid S)=\pi_{edge}P(I\mid S,M_{edge})+\pi_{intensity}P(I\mid S,M_{intensity}) \tag{5.4}$$

Here the first component of the likelihood is due to informative edge cues, and the second component comes from less informative intensity cues. The strength of the edge can be used to indicate the weight to which each prior model applies. Then a formula for likelihood (Coughlan, 2011, this volume) that expresses a matching error, $m(D)$ at a certain image location and disparity $D$,

$$P(m(D)\mid D)=\frac{1}{Z}e^{-\mu m(D)} \tag{5.5}$$

can be rewritten as

$$P(m(D)\mid D)=\frac{1}{Z'}\left[\pi_{edge}e^{-\mu_1m(D)}+\pi_{intensity}e^{-\mu_2m(D)}\right] \tag{5.6}$$

Where $\mu_2<\mu_1$ to reflect the fact that an intensity cue is less informative than the edge cue. In the marginal case of $\mu_2=0,\pi_{intensity}=1$, and $\pi_{edge}=0$, we obtain the above-described flattening method for likelihoods. Note that in order to detect cues with weak likelihoods, one can directly analyze likelihood peaks, which is more beneficial than measuring edge strength. The former has an advantage of finding cases when the reason for weak likelihood is not only a low contrast texture but also a highly regular texture (i.e., the one that produces multiple matching hypotheses).

As computer simulations show, flattening weak likelihoods greatly improves propagation of disparity information into regions with weak cues. Such a method is especially applicable in stereo algorithms, because they often rely on some smoothness constraint that justifies cue propagation