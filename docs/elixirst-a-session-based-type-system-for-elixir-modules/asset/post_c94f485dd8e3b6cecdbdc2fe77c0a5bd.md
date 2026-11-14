
### [TCASE]

From the rule, we know that

```
t = case e do (p_i -> t_i)_i end
\theta \vdash \text{exp } e : U \quad \text{(B.33)}
```

By Lemma 16 and eq. (B.33), expression e can be either a value, or reduce to a new expression. Consider both sub-cases:

- 1. If expression e can be reduced (i.e., e -> e'), then case holds by [kCase$_e$], resulting in the internal transition: t -> case e' do (p_i -> t_i)_i end.
- 2. Otherwise, if e = v, then case holds by [kCase$_v$], resulting in the internal transition t -> t sigma_j, where t_j is the branch which pattern matches with v, and sigma contains the substitutions (i.e., sigma = match(p_j, v)).

### [TEXPRESSION]

From the rule, we know that

```
t = e \quad \text{(B.34a)}
\theta \vdash \text{exp } e : T \quad \text{(B.34b)}
```

Similar to the previous case. By Lemma 16 and eq. (B.34b), expression e can be either a value, or reduce to a new expression. In the former of the cases, where e can be reduced (i.e., e -> e'), then case holds immediately by [kExpression] (i.e., t -> t'), where after(S, r) is defined. In the other case, when e is a value, then t is also a value, since t = e (by eq. (B.34a)).

## References

- [1] D. Thomas. Programming Elixir: Functional, Concurrent, Pragmatic, Fun. Pragmatic Bookshelf, 2018.
- [2] C. Hewitt, P. Bishop, R. Steiger. A universal modular ACTOR formalism for artificial intelligence. In: N.J. Nilsson (ed.), Proceedings of the 3rd International Joint Conference on Artificial Intelligence. Stanford, CA USA, August 20-23, 1973, William Kaufmann, 1973, pp. 235-245.
- [3] C.A. Agha. ACTORS - A Model of Concurrent Computation in Distributed Systems. MIT Press Series in Artificial Intelligence, MIT Press, 1990.
- [4] J. Armstrong. Programming Erlang: Software for a Concurrent World. Pragmatic Bookshelf, 2013.
- [5] N. Niesen, Cowboy. GitHub repository, https://github.com/ninenines/cowboy, 2022.
- [6] D.C. Schmidt, S. Vinoski. Object Interconnections Comparing Alternative Programming Techniques for Multi-Threaded CORBA Servers (Column 7), 1996.
- [7] C. Tabone, A. Francalanza. Session types in Elixir. In: E. Castegren, J.D. Koster, S. Fowler (Eds.), Proceedings of the 11th ACM SIGPLAN International Workshop on Programming Based on Actors, Agents, and Decentralized Control, AGERE! 2021, Virtual Event / Chicago, IL, USA, 17 October 2021, ACM, 2021, pp. 12-23.
- [8] C. Tabone, A. Francalanza. Session fidelity for Elixir$^T$: a session-based type system for Elixir modules. In: C. Aubert, C. Di Giusto, L. Safina, A. Scalas (Eds.), Proceedings 15th Interaction and Concurrency Experience, ICE 2022, Lucca, Italy, 17 June 2022, in: EPTCS, vol. 365, 2022, pp. 17-36.
- [9] S. Nyström. A soft-typing system for Erlang. In: B. Däcker, T. Arts (Eds.), Proceedings of the 2003 ACM SIGPLAN Workshop on Erlang, Uppsala, Sweden, August 2003, ACM, 2003.
- [10] B.C. Pierce. Types and Programming Languages. MIT Press, 2002.
- [11] T. Lindahl, K. Sagonas. Practical type inference based on success typings. In: A. Bossi, M.J. Maher (Eds.), Proceedings of the 8th International ACM SIGPLAN Conference on Principles and Practice of Declarative Programming, July 10-12, 2006, Venice, Italy, ACM, 2006, pp. 167-178.
- [12] M.C. Rinard, P.C. Diniz. Compatibility Analysis. J. Program. Lang. 19 (1997) 35-70. https://doi.org/10.1007/s007780050020.
- [13] M. Papadakis, A. Serebrenik. A Survey of Dynamic Analysis Techniques for Testing Elixir Programs. Comput. Lang. Syst. Struct. 68 (2022) 101077. https://doi.org/10.1016/j.cl.2021.101077.
- [14] R.M. Keller. Formal verification of parallel programs. Commun. ACM 19 (1976) 371-384. https://doi.org/10.1145/360248.360251.
- [15] L. Lamport. Proving Specification types in atemporal linear logic propositions. In: CONCUR ’90, Theories of Concurrency: Unification and Extension, CONCUR 2010, Paris, August 31-September 2, 2010, pp. 222-236. 2010 - Concurrency Theory. 21st International Conference, CONCUR 2010, Paris, France, August 31-September 2, 2010, Proceedings. JAM 63 (2016) 9. https://doi.org/10.1145/2827895.
- [16] K. Honda, N. Yoshida, M. Carbone. Multiparty asynchronous session types. J. ACM 63 (2016) 9. https://doi.org/10.1145/2827695.
- [17] C. MacCart. Metaprogramming Elixir - Write Less Code, Get More Done (and Have Fun!). The Pragmatic Programmers, O’Reilly, 2015. http://www.bookshelf.dk/books/8160800407/index.htm.
- [18] R. Milner. A Calculus of Communicating Systems. Lect. Notes Comput. Sci. 32 (2022) 66. https://doi.org/10.1007/3540102353_1.
- [19] D. Mostrous, V.T. Vasconcelos. Session typing for a featherweight Erlang. In: W.D. Meuter, G. Roman (Eds.), Coordination Models and Languages - 13th International Conference, COORDINATION 2011, Reykjavik, Iceland, June 6-9, 2011. Proceedings, in: Lecture Notes in Computer Science, vol. 6721, Springer, 2011, pp. 95-109.
- [20] A. Francalanza, S. Aceto, I. Cassar. https://duffel.com/, 2023.
- [21] A. Francalanza, A. Seychell. Synthesising correct concurrent runtime monitors. Form. Methods Syst. Des. 46 (2015) 226-261. https://doi.org/10.1007/s10703-014-0217-9.
- [22] A. Francalanza, A. Theory of monitors. Inf. Comput. 281 (2021) 104704. https://doi.org/10.1016/j.ic.2021.104704.
- [23] R. Milner. Calculi for synchrony and asynchrony. Theoretical Computer Science 25 (1983) 267-310. https://doi.org/10.1016/0304-3975(83)90114-2.
- [24] C. Bartolo Buttò, A. Francalanza. A Scalable, On the monitorability of session types, in theory and practice. In: A. Möller, M. Sridharan (Eds.), 35th European Conference on Object-Oriented Programming, ECOOP 2021, July 11-17, 2021, Aarhus, Denmark (Virtual Conference), in: LIPIcs, vol. 194, Schloss Dagstuhl - Leibniz-Zentrum für Informatik, 2021, pp. 20:1-20:30.
- [25] M. Papadakis, A. Serebrenik. A Survey of Dynamic Analysis Techniques for Testing Elixir Programs. Comput. Lang. Syst. Struct. 68 (2022) 101077. https://doi.org/10.1016/j.cl.2021.101077.
- [26] Erlang Solutions. Gradient. GitHub repository. https://github.com/elixir-lang/gradient, 2022.
- [27] W.-M. Wijnga. Typecheck: fast and flexible runtime type-checking for your Elixir projects, GitHub repository. https://github.com/Qqwy/elixir-type\_check, 2022.
- [28] J. Harrison. Automatic detection of core Erlang message passing errors, in: N. Chechina, A. Francalanza (Eds.), Proceedings of the 17th ACM SIGPLAN International Workshop on Erlang, ICFP 2018, St. Louis, MO, USA, September 23-29, 2018, ACM, 2018, pp. 37-48.
- [29] M. Christakis, K. Sagonas, Detection of asynchronous message passing errors using static analysis, in: R. Rocha, J. Launchbury (Eds.), Practical Aspects of Declarative Languages - 13th International Symposium, PADL 2011, Austin, TX, USA, January 24-25, 2011. Proceedings, in: Lecture Notes in Computer Science, vol. 6539, Springer, 2011, pp. 5-18.
- [30] K. Ostermann, S. Jost, H. Loeh, J. Berthold, P. Steckler, Message passing concurrency for heterogeneous many-cores, in: A. Francalanza, V. Fodor (Eds.), Proceedings of the 18th ACM SIGPLAN International Workshop on Erlang, Erlang@ICFP 2019, Berlin, Germany, August 18, 2019, ACM, 2019, pp. 36-47.
- [31] H. Svensson, L. Fredlund, C. Earl, A unified semantics for future Erlang, in: S. F. Critch, K. Sagonas (Eds.), Proceedings of the 9th ACM SIGPLAN Workshop on Erlang, Baltimore, Maryland, USA, September 30, 2010, ACM, 2010, pp. 23-32.
- [32] M. Papadakis, K. Sagonas, A. Francalanza, Erlang/PropEr: a property-based testing tool for industrial Erlang/OTP programs, in: J. Hage (Eds.), Proceedings of the 7th ACM SIGPLAN Workshop on Erlang, Tokyo, Japan, September 22, 2008, ACM, 2008, pp. 31-40.
- [33] K. Honda, A. Mukhamedov, G. Brown, T.-C. Chen, N. Yoshida, Scribbling Interactions in a Formal Foundation, in: R. Natarajan, A. K. Ojo (Eds.), Distributed Computing and Internet Technology - 7th International Conference, ICDCIT 2011, Bhubaneswar, India, February 9-12, 2011. Proceedings, in: Lecture Notes in Computer Science, vol. 6536, Springer, 2011, pp. 55-75.
- [34] S. Fowler, An Erlang implementation of multiparty session actors, in: M. Bartoletti, L. Henrio, S. Knight, H. T. Vieira (Eds.), Proceedings 9th Interaction and Concurrency Experience, ICE 2016, Heraklion, Greece, 8-9 June 2016, in: EPTCS, vol. 223, 2016, pp. 36-50.
- [35] R. Neykova, N. Yoshida, Let it recover: multiparty protocol-induced failure recovery, in: Proceedings of the 26th International Conference on Compiler Construction, CC 2017, Association for Computing Machinery, New York, NY, USA, 2017, pp. 98–108.
- [36] A. Scalas, N. Yoshida, Less is more: multiparty session types revisited, in: Proceedings of the 43rd Annual ACM SIGPLAN-SIGACT Symposium on Principles of Programming Languages, POPL 2016, St. Petersburg, FL, USA, January 20 - 22, 2016, in: ACM, 2016, pp. 211-228.
- [37] A. Scalas, N. Yoshida, E. Benussi, Effpi: verified message-passing programs in Dotty, in: J. Bäckhans, R. Neykova, N. Yoshida (Eds.), Proceedings of the Tenth ACM SIGPLAN Symposium on Scala, Scala@ECOOP 2019, London, UK, July 17, 2019, ACM, 2019, pp. 27-31.
- [38] A. Scalas, N. Yoshida, E. Benussi, Verifying message-passing programs with dependent behavioural types, in: S. K. McKinley, K. Fisher (Eds.), Proceedings of the 40th ACM SIGPLAN Conference on Programming Language Design and Implementation, PLDI 2019, Phoenix, AZ, USA, June 22-26, 2019, ACM, 2019, pp. 502-516.
- [39] P. Harvey, S. Fowler, O. Dardha, S. J. Gay, Multiplying session types for safe runtime adaptation in an actor language, in: A. Moller, M. Sridharan (Eds.), 35th European Conference on Object-Oriented Programming, ECOOP 2021, July 11-17, 2021, Aarhus, Denmark (Virtual Conference), in: LIPIcs, vol. 194, Schloss Dagstuhl - Leibniz-Zentrum für Informatik, 2021, pp. 13:1-13:29.
- [40] T.B.L. Jespersen, P. Munksgaard, K.F. Larsen, Session types for rust, in: P. Bahr, E. Erdwadi (Eds.), Proceedings of the 11th ACM SIGPLAN Workshop on Generic Programming, WGP@ICFP 2015, Vancouver, BC, Canada, August 30, 2015, ACM, 2015, pp. 13-24.
- [41] W. Kokke, Rusty variation: deadlock-free sessions with failure in rust, in: M. Bartoletti, L. Henrio (Eds.), Proceedings 12th Interaction and Concurrency Experience, ICE 2019, Copenhagen, Denmark, 3rd-4th July 2019, in: EPTCS, vol. 304, 2019, pp. 48-60.
- [42] N. Lagaliaridis, R. Neykova, N. Yoshida, Implementing multiparty session types in Rust, in: S. Bludze, L. Bocchi (Eds.), Coordination Models and Languages - 22nd IFIP WG 6.1 International Conference, COORDINATION 2020, Held as Part of the 15th International Federated Conference on Distributed Computing Techniques, DisCoTec 2020, Valletta, Malta, June 15-19, 2020, Proceedings, in: Lecture Notes in Computer Science, vol. 12134, Springer, 2020, pp. 122-141.
- [43] Z. Cutner, N. Yoshida, Safe session-based asynchronous coordination in rust, in: F. Damiani, O. Dardha (Eds.), Coordination Models and Languages - 23rd IFIP WG 6.1 International Conference, COORDINATION 2021, Held as Part of the 16th International Federated Conference on Distributed Computing Techniques, DisCoTec 2021, Valletta, Malta, June 14-18, 2021, Proceedings, in: Lecture Notes in Computer Science, vol. 12717, Springer, 2021, pp. 80-89.
- [44] A. Francalanza, A protocol library for session types in rust, Proc. ACM Program. Lang. 7 (ICFP) (2023) 17. doi:10.1145/3607857.
- [45] H.C. Melgratti, A. Padovani, Choreography semantics for higher-order session types, Proc. ACM Program. Lang. 1 (2017) 35. doi:10.1145/3133879.
- [46] K. Honda, V. T. Vasconcelos, M. Kubo, Language primitives and type discipline for structured communication-based programming, in: Programming Languages and Systems: 7th European Symposium on Programming, ESOP'98 Held as Part of the Joint European Conferences on Theory and Practice of Software, ETAPS'98 Lisbon, Portugal, March 28-April 4, 1998 Proceedings 7, Springer, 1998, pp. 122-138.
- [47] K. Honda, V. T. Vasconcelos, M. Carbone, Key types for session types, in: K. Ogata, M. Lawford, S. Liu (Eds.), Formal Methods and Software Engineering - 18th International Conference on Formal Engineering Methods, ICFEM 2016, Tokyo, Japan, November 14-18, 2016. Proceedings, in: Lecture Notes in Computer Science, vol. 10009, 2016, pp. 296-312.
- [48] R. Hu, N. W. A. Haber, E. Kamburjan, Locally static, globally dynamic session types for active objects, in: E. S. de Boer, J. Muro (Eds.), Recent Advances in the Verification of Software and Concurrent Systems - Festschrift in Honor of César B. Festi, November 27, 2020, Bologna, Italy, in: OASICS, vol. 86, Schloss Dagstuhl - Leibniz-Zentrum für Informatik, 2020, pp. 1:1-1:24.
- [49] U. de'Liguoro, L. Padovani, Mailbox types for unordered interactions, in: T.D. Millstein (Ed.), 32nd European Conference on Object-Oriented Programming, ECOOP 2018, July 16-21, 2018, Amsterdam, the Netherlands, in: LIPIcs, vol. 109, Schloss Dagstuhl - Leibniz-Zentrum für Informatik, 2018, pp. 10:1-10:29.
- [50] S. Fowler, D. Attard, F. Sowul, S.J. Gay, P. Trinder, Special delivery: programming with mailbox types, Proc. ACM Program. Lang. (2023).
- [51] S. Balzer, F. Pfenning, Manifest sharing with session types, Proc. ACM Program. Lang. 1 (2017) 37. doi:doi.org/10.1145/31338281.
- [52] A. Francalanza, M. Hennessy, A theory for observational fault tolerance, Log. Algebraic Methods Program. 73 (2007) 22-50.
- [53] A. Francalanza, A. Seychell, A theory of system behaviour in the presence of node and link failure, Inf. Comput. 208 (2010) 711-759.
- [54] L. Bocchi, K. Honda, T. Yoshida, A. Vaynol, A model of actors and grey failures, in: COORDINATION, in: Lecture Notes in Computer Science, vol. 13271, Springer, 2022, pp. 140-158.
- [55] K. Peters, U. Nestmann, W. Vogler, Fault-tolerant multiparty session types, in: FORTE, in: Lecture Notes in Computer Science, vol. 13273, Springer, 2022, pp. 90-108.
- [56] A. Francalanza, A. Scalas, N. Yoshida, Generalised multiparty session types with crash-stop failures, in: CONCUR, in: LIPIcs, vol. 243, Schloss Dagstuhl - Leibniz-Zentrum für Informatik, 2022, pp. 35:1-35:25.
- [57] M.A.L. Brugnara, D. Maggi, Types for failure-prone communication, in: ESOP, in: Lecture Notes in Computer Science, vol. 13990, Springer, 2023, pp. 363-391.
- [58] J. Hogg, J. Lea, S. Wills, D. Detlefs, P. O'Hearn, Work analysis with resource-aware session types, in: A. Dawar, E. Grädel (Eds.), Proceedings of the 33rd Annual ACM/IEEE Symposium on Logic in Computer Science, LICS 2018, Oxford, UK, July 09-12, 2018, ACM, 2018, pp. 305-314.
- [59] A. Francalanza, E. de Vries, M. Hennessy, Compositional reasoning for explicit resource management in channel-based concurrency, Log. Methods Comput. Sci. 10 (2014). https://doi.org/10.2168/LMCS-10(2:15)2014.
- [60] C. Casagna, G. Duboc, J. Valtin, The design principles of the Elixir type system, CoRR, arXiv:2306.06391, 2023.
