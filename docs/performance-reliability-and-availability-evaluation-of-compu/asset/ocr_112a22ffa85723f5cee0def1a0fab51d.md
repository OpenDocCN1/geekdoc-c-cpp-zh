# Hot Standby

![](bbox=[0.118, 0.116, 0.882, 0.303])

**Figure 21.8** Application Servers – Hot-Standby.



$$R_{Server}(t) = R_{App}(t) \times R_{OS}(t) \times R_{HW}(t),$$
\nR_{HW}(t) = R_{MB}(t) \times R_{NC}(t) \times R_{VC}(t) \times R_{DC}(t) \times R_{D}(t) \times R_{S}(t),$$
\n$$R_i(t) = e^{-\lambda_i t}, \quad i \in \{App, OS, MB, NC, VC, DC, D, S\}.$$n\nTherefore,
\n$$R_{Server}(t) = e^{-\sum \lambda_i t}, \quad i \in \{App, OS, MB, NC, VC, DC, D, S\,$$n\nwhere
\n$$\lambda_{Server} = \sum_{i} \lambda_i, \quad i \in \{App, OS, MB, NC, VC, DC, D, S\}, \quad (21.2.6)$$
\nand
\n$$MTTF_{Server} = \frac{1}{\lambda_{Server}}.$
The failure rate of the server ($\lambda_{Server}$) is assigned to the CTMC depicted in Figure 21.9.a, which is an availability model when considering only one repair facility. Assuming server time to repair is exponentially distributed with rate $\mu$, the CTMC can be used to estimate the system availability (Equation 21.2.2) and down-time in a period $T$. Hence
\n$$A = \frac{\mu(2\lambda_{Server} + \mu)}{2\lambda_{Server}^2 + 2\lambda_{Server}\mu + \mu^2}, \quad (21.2.7)$$$