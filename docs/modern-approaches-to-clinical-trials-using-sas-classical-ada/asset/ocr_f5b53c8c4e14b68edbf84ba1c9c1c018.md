# 4.4 Bayesian Meta-Experimental Design

In this section, we present a general methodology for Bayesian meta-experimental design for the log-linear regression models. We first define the hypotheses for non-inferiority testing, which can be formulated as follows:

$H_0: e^{\gamma_1} \ge \zeta$ versus $H_1: e^{\gamma_1} < \zeta$ $(4.7)$

where $e^{\gamma_1}$ is the hazard ratio of experimental versus control and $\zeta$ is a prescribed non-inferiority margin. The meta-trials are successful if $H_0$ is rejected. The non-inferiority margin $\zeta$ is a user’s input value in the SAS macro bmed. For example, for the meta-analysis design evaluating cardiovascular risk, we may choose $\zeta=1.3$ according to [14].

Let $[\gamma, 	heta]$ denote the collection of parameters for the regression model. Following [1], let $\pi^{(S)}[\gamma, 	heta]$ and $\pi^{(F)}[\gamma, 	heta]$ denote the sampling prior and the fitting prior under the meta-experimental survival model, respectively. The sampling prior play a role to capture a certain portion of the parameter space in achieving a certain level of performance in the Bayesian meta-experimental design. As discussed in [1, 6], the sampling prior, $\pi^{(S)}[\gamma, 	heta]$, is used to generate the meta-experimental survival data $D_K$ and the fitting prior, $\pi^{(F)}[\gamma, 	heta]$, is used to fit the regression models once the meta-experimental survival data are generated.

Using the data $D_K$, the posterior distribution of $[\gamma, 	heta]$ under the meta-regression survival model is given

$\pi[\gamma, 	heta|D_K] \propto \prod_{jk=1}^L \exp\{y_{jk}(\gamma_0 + \gamma_{1jk} + \theta_k)\}\exp\{-exp(\gamma_0 + \gamma_{1jk} + \theta_k)y_{jk}\}$

$\times \pi^{(F)}[\gamma, \theta]$. $(4.8)$

In (4.8), we note that the fitting prior, $\pi^{(F)}[\gamma, 	heta]$, may be improper as the resulting fitting prior $\pi[\gamma, 	heta|D_K]$ is proper.

To complete the Bayesian meta-experimental design, we need to specify