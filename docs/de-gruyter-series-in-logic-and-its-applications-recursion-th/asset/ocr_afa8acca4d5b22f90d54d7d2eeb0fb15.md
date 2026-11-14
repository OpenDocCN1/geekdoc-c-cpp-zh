# 12.3 Lowness for randomness

# 12.3.1 General lowness notions

Given a notion \(\Gamma\) of randomness, we may relativize it to a real \(x\) to obtain \(\Gamma^x\). Define \(\text{Low}(\Gamma) = \{x \in 2^\omega \mid \Gamma \subseteq \Gamma^x\}\). Then every member of \(\text{Low}(\Gamma)\) is said to be low for \(\Gamma\).

One may consider a slightly stronger lowness notion. Since each \(\Gamma\) is defined in terms of \(\Gamma\)-tests, we may declare \(x\) to be low for \(\Gamma\)-tests if every \(\Gamma^x\) test covered (as a set) by a \(\Gamma\)-test. More details concerning these can be found in [111] and [24].

Hence if \(x \in \text{Low}(\Gamma)\) then it does not provide any information regarding randomness for \(\Gamma\). Nevertheless, the property of lowness seems somewhat mysterious since one has no clue on the complexity of members of \(\text{Low}(\Gamma)\). A very important and successful application of classical recursion theory is the characterization of the lowness property for various notions of randomness.

# 12.3.2 Lowness for Kurtz randomness

**Theorem 12.3.1** (Stephan, Yu [160] and Greenberg, Miller [38]). _For any real_ \(x\)_, the following are equivalent:_

+   (i) \(x\) is low for Kurtz randomness;
+   (ii) \(x\) is low for Kurtz tests;
+   (iii) \(x\) is recursively dominated and non-DNR.

It is known that there are \(2^{\aleph_0}\) many recursively dominated and non-DNR reals. Hence Theorem 12.3.1 says that there is an abundance of reals which do not provide any information about Kurtz randomness.

# 12.3.3 Lowness for Schnorr randomness

**Definition 12.3.2.** A real \(x\) is _recursively traceable_ if for any \(f \le_T x\), there is a recursive function \(g : \omega \to \mathscr{P}_{<\omega}(2^{<\omega})\) such that for any \(e\), \(f(e) \in g(e)\) and \(|g(e)| \le e\).

It is not difficult to see that every recursively traceable real is recursively dominated and non-DNR. Moreover, the construction of a recursively traceable real is quite similar to that of a set of minimal Turing degree. They are both obtained using Sacks forcing with recursive perfect trees.

**Theorem 12.3.3** (Terwijn, Zambella [163] and Kjos-Hanssen, Nies, Stephan [67]). _For any real_ \(x\)_, the following are equivalent:_

+   (i) \(x\) is low for Schnorr randomness;
+   (ii) \(x\) is low for Schnorr tests;
+   (iii) \(x\) is recursively traceable.