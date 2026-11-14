where \(\Delta' : \emptyset \vdash S'' \triangleright t' : T \triangleleft S'\) is the expected result.

+   2. [RLET] From the rule, we know that \(t = (x = v; t_2)\), \(t' = t_2 \{v/x\}\) and \(\alpha = \tau\), therefore \(\text{after}(S, \alpha) = S = S''\). Since \(t_1 = v\), by eq. (B.16b) and [RExpression], then \(\emptyset \triangleright \text{exp} : T\) holds. If we apply this latter information and eq. (B.18c) to the Substitution Lemma, we obtain \(\Delta \cdot \emptyset \vdash^w S'' \triangleright t_2 \{v/x\} : T \triangleleft S'\). This is the expected result, since by the Variable Substitution Definition, \(\text{w}[\Delta'] = \text{w}\); and by the **after** definition, \(\Delta' = \Delta\).

# [TBRANCH] From the rule, we know that for some \(n \in \mathbb{N}\) then

\(S = \& \{ ?i_1 (T_1^1, \dots, T_i^n), S_i \}_{i \in I}\) (B.19a)
\(t = \text{receive} \ \text{do} \ \{ [\langle 1_i, p_i^1, \dots, p_i^n \rangle \rightarrow t_i \}_{i \in I} \text{end}\) (B.19b)
\(S_\mu = \text{after}(\& \{ ?i_1 (T_1^1, \dots), S_i \}_{i \in I}, \alpha)\) (B.19c)

Since \(\alpha\) has to be an incoming message, we focus solely on te first case of the Session Fidelity Theorem. From the premise, we also know that some properties regarding each individual branch from the receive construct:

\(\forall i \in I . \begin{cases} \vdash^{\text{par}} p_i^j : T_i^j \triangleright \Gamma_i^j \text{ for all } j \in 1..n \\ \Delta \cdot (\Gamma_i^1, \dots, \Gamma_i^n) \vdash^w S_i \triangleright t_i : T \triangleleft S' \end{cases}\) (B.19d) (B.19e)

From the structure of \(t\) (eq. (B.19b)), term reduction (\(t \xrightarrow{\alpha} t'\)) can only be derived using [RBRANCH], where execution progresses to a single branch (i.e., \(t_\mu\)), rather than all branches. The right branch is chosen by matching its label, \(1_\mu\), to the label received in the incoming message, \(1_\mu\). Thus, for some \(k \in \mathbb{N}\), there exists some \(\mu \in I\) where \(1_\mu = 1_\mu\), and

\(\alpha = ? \{ \langle 1_\mu, \nu_1, \dots, \nu_n \rangle \}\) (B.19f)
\(\text{match}((p_\mu^1, \dots, p_\mu^n), (\nu_1, \dots, \nu_n)) = [\nu_1^{i_1} \dots \nu_n^{i_n} / x_{i_1} \dots x_{i_n}]\) (B.19g)
\(t' = t_\mu [\nu_1^{i_1} \dots \nu_n^{i_n} / x]\)

From eq. (B.19f), \(\alpha\) refers to the message received from the dual process, which is assumed (from the premise of the theorem) to be valid by the after function (eq. (B.19c)). We can compare the contents of this message to the original session type \(S\) (eq. (B.19a)), to obtain information regarding the types of the individual values inside \(\alpha\). We know that \(\alpha\) contains a label \(1_\mu\) and \(n\) values. Thus for \(j \in 1..n\), each value \(\nu_j\) has a corresponding type \(T_\mu^j\) from the session type \(S\), where \(S\) contains ?\(1_\mu (T_\mu^1, \dots, T_\mu^n). S_\mu\). Formally, this can be written as

\(\emptyset \triangleright \text{exp}_j \nu_j : T_\mu^j \text{ for all } j \in 1..n\) (B.19h)

Applying eqs. (B.20), (B.19g) and (B.19h) into Corollary 14, results in \(\widetilde{\Gamma}_\mu^j = \Gamma_\mu^1, \dots, \Gamma_\mu^n = x_1 : T_1, \dots, x_k : T_k\) and

\(\emptyset \triangleright \text{exp}_j^w : T_m \text{ for } m \in 1..k\) (B.19i)

Applying eq. (B.19i) and \(\Delta \cdot \widetilde{\Gamma}_\mu^j \vdash^w S_\mu \triangleright t_\mu : T \triangleleft S'\) (from eq. (B.19e) for \(i = \mu\)) repeatedly to the Substitution Lemma, we get

\(\Delta \cdot \emptyset \vdash^w S_\mu [\nu_1^{i_1} \dots \nu_n^{i_n} / x_{i_1} \dots x_{i_n}] : T \triangleleft S'\) (B.19j)

Since \(\text{after}(\alpha, S) = \Delta\), then eq. (B.19j) is the expected result.

# [TCHOICE] From the rule, we know that for some \(\mu \in I\), \(T = (\text{atom}, T_\mu^1, \dots, T_\mu^n)\) and

\(S = \oplus \{ \langle 1_i, (T_i^1) \rangle S_i \}_{i \in I}\) (B.20a)
\(t = \text{send} \ \langle \langle 1_\mu, e_1, \dots, e_n \rangle \rangle\) (B.20b)
\(\emptyset \triangleright \text{exp} \ e_j : T_\mu^j \text{ for all } j \in 1..n\) (B.20c)

From the structure of \(t\) (eq. (B.20b)), term reduction (\(t \xrightarrow{\alpha} t'\)) can be derived by several rules, so we have to consider two sub-cases:

+   1. Derived by the rule [RCHOICE1], we know that \(\alpha = \tau\) and

\(t' = \text{send} \ \langle \langle 1, \nu_1, \dots, v_{k-1}, e_k^i, \dots, e_n \rangle \rangle\)
\(e_k \rightarrow e_k^i\) (B.20d)