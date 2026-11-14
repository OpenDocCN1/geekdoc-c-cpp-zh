Let us now prove (15.6.5). We have

\(\Phi_\alpha^{*,S}(x) = E \int_t^{\tau_S^x} \exp - \alpha t \varphi(y_S^{*,S}(t)) dt\)
\(+ \sum_{n=1}^{n+1} E \int_{\tau_{x,n}^{S,S}}^{\tau_{x,n+1}^{S,S}} \exp - \alpha t \varphi(y_x^S(S)(t)) dt.\)

Then using conditioning and independence properties, for \(n \ge 1\)

\(E \int_{\tau_{x,n}^{S,S}}^{\tau_{x,n+1}^{S,S}} \exp - \alpha t \varphi(y_x^S(S)(t)) dt\)
\(= E \exp - \alpha \tau_{x,n}^{S,S} \int_0^{\tau_{x,n+1}^{S,S} - \tau_{x,n}^{S,S}} \exp - \alpha t \varphi(y_x^S(\tau_{x,n}^{S,S} + t)) dt\)
\(= E \exp - \alpha \tau_{x,n}^{S,S} E \int_0^{\tau_S^x} \exp - \alpha t \varphi(y_S^{*,S}(t)) dt\)
\(= E \exp - \alpha \tau_S^x (E \exp - \alpha \tau_S^x)^{n-1} E \int_0^{\tau_S^x} \exp - \alpha t \varphi(y_S^{*,S}(t)) dt.\)

We obtain the formula

(15.6.8) \(\Phi_\alpha^{n,S}(x) = E \int_0^{\tau_S^x} \exp - \alpha t \varphi(y_S^{*,S}(t)) dt\)
\(+ E \exp - \alpha \tau_S^x \frac{E \int_0^{\tau_S^x} \exp - \alpha t \varphi(y_S^{*,S}(t)) dt}{1 - E \exp - \alpha \tau_S^x}.\)

Then

(15.6.9) \(\alpha \Phi_\alpha^{*,S}(x) \rightarrow \frac{E \int_0^{\tau_S^x} \varphi(y_S^{*,S}(t)) dt}{E \tau_S^x}.\)

If we define

\(\zeta_s(x; \varphi) = E \int_0^{\tau_S^x} (\varphi(y_S^{*,S}(t)) dt,\)

then we have proven that

\(\alpha \Phi_\alpha^{*,S}(x) \rightarrow \frac{\zeta_S(S; \varphi)}{\zeta_S(S; 1)}.\)

However \(\zeta_s(x; \varphi)\) is the solution of the problem

(15.6.10) \(A \zeta_s(x) = \varphi(x) \quad x > s\)
\(\zeta_s(x) = 0 \quad x \le s\)

and it has the explicit solution

(15.6.11) \(\zeta_s(x; \varphi) = \frac{2}{\sigma^2 s} \int_s^x \Gamma(x - \xi) \int_\xi^{+\infty} \exp \beta_2(\eta - \xi) \varphi(\eta) d\eta.\)

We deduce, after some easy changes of integration

\(\zeta_S(S; \varphi) = \frac{2}{\sigma^2 s} \int_S^S \varphi(n) \exp \beta_2 \eta \left( \int_S^\eta \exp - \beta_2 \xi \Gamma(S - \xi) d\xi \right) d\eta\)
\(+ \frac{2}{\sigma^2} \int_S^{+\infty} \varphi(n) \exp \beta_2 \eta \left( \int_S^\eta \exp - \beta_2 \xi \Gamma(S - \xi) d\xi \right) d\eta\)