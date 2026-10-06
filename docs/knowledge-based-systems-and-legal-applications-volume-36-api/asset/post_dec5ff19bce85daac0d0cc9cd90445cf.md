
# The Representation of Law in Computer Programs

formalisms of various kinds, and the use of procedural PROLOG. (I explain the difference below.) Semantic networks and frame-based representations have also been used, though much less frequently. Some examples are given in later sections.

## 1.8.1. Rule-based formalisms

The law resembles a set of rules more than it does a set of detailed algorithms, and it is not surprising that many attempts to construct computer representations of law have employed rule-based formalisms. This is an innocuous remark but there is an unfortunate ambiguity that has caused some confusion.

The term 'rule-based model of the law' can have different meanings in different contexts. 'Rule-based' can refer to the law or it can refer to the chosen computational formalism, or to both. One can choose to view the law as a set of 'rules' but represent these 'rules' in some non-rule-based computational formalism. Twining and Miers' flowcharts are an example. Similarly, one can choose not to view the law as 'rules' but still employ a rule-based computational formalism for representation purposes. Waterman and Peterson's expert systems can be regarded as an example of this.

Some commentators have fallen into the trap of using a rule-based computational formalism for representation purposes implies that the authors have belong to some — possibly very extreme school of jurisprudence. Critics of the formalism are tangled with accusations of jurisprudential naivety. This section is concerned with the use of rule-based computational formalisms.

There are so many projects that used rule-based formalisms to represent law that I cannot give a comprehensive list of references. I give only a selection of some early examples.

Waterman and Peterson's systems implemented in ROSIE, and Michaels' TAXADVISOR implemented in EMYCIN have already been discussed in some detail (section 1.5).

Philip Leith has used a production system of his own design [Leith 1983] to construct ELI [Leith 1982], a system which treats parts of the UK's Security legislation.

Duncan and Elizabeth MacRae have implemented a system to advise tax lawyers and accountants on section 74 of the US Internal Revenue Code which deals with prizes and awards [MacRae 1985a, 1985b; Macrae and MacRae 1985]. This system is implemented in PRO. It should not be confused, however, with projects that have used PROLOG as a representation language or with the approach described later under the heading 'Representing law as logic programs'. The representation language used in the MacRae system is a propositional rule language of their own design. PROLOG is used only to implement the inference mechanism. An important feature of the MacRaes' system is the emphasis they have given to interface and control issues. The system is designed to be used by someone who is already an expert in the domain. The MacRaes have been concerned particularly with developing an interface which gives their users control over the execution of the system, by directing searching away from areas which are felt to be irrelevant or redundant.

David Gold and Richard Susskind collaborated on an interdisciplinary project (computing and jurisprudence) which developed a rule-based language for representing certain kinds of law [Gold 1987]; Gold and Susskind 1986; see also Susskind 1986a). Gold and Susskind illustrated the use of this language with an example based on the law of divorce in Scotland. [Susskind 1987] also describes number of particular systems which are being built by him and others with other rule-programming tools.

Another system which is classified in this general category is Jim Sprowl's ABF processor [Sprowl 1979, 1980]; see also Cook et al. 1981]. This system was designed for the computer generation of legal documents, but by McCarthy [1983a] points out it could be used for building legal analysis programs as well. The ABF system is a kind of word-processor, where the programmer specifies the ABF language how fragments of text together with data obtained from the user are to be inserted into the document being generated. The document specification can include expressions constructed from arithmetical operators and keywords like AND, IF, OR and NOT. The ABF processor evaluates these expressions when they are encountered during document generation. But the programmer is allowed to include his own terms in these too, which he defines by means of IF/THEN and IFF expressions. When the ABF processor encounters a term defined by the programmer, it evaluates its truth value by working backwards from conclusion to conditions through the definition. Since these definitions can be of arbitrary complexity, the ABF processor could be used as a backward chaining interpreter for propositional rules. (Although I have seen Sprowl's ABF processor referred to as a rule-based system on several occasions, I am not aware that it has been used in practice for anything other than document generation.)

There are many other projects described in this survey that employ rule-based formalisms to build representations of law. The main ones are LEGOL, the logic programming projects, ESPLEX, and Gardner's doctoral project. TAXMAN used a frame-based formalism and Meloused semantic networks. In both of these cases, the system can be reconstructed easily in terms of rules. These projects are not included in this section because they are all described separately in more detail later.

# The Representation of Law in Computer Programs

The programming language PROLOG can also be regarded as a rule-based formalism. I have separated out descriptions of the use of PROLOG because there are some specific comments that I want to make about this.

## 1.8.2. Procedural PROLOG

Several projects have used (procedural) PROLOG as a representation of language. Dean Scholzbohm [1985] has written a PROLOG program which helps to analyse the rules dealing with 'constructive ownership of stock' in section 318(a) of the US Internal Revenue Code. David Sherman [1986, 1987] has implemented a large PROLOG program which models the Income Tax Act of Canada.

Section 1.10 of this chapter is devoted to the applications of logic programming to law. In order to understand why the projects in this section have been listed in a separate category, it is necessary to appreciate the difference between procedural PROLOG programs and declarative logic programs (which can be executed by PROLOG but can be executed in other ways as well).

The programming language PROLOG is based on logic, specifically on a subset of first-order logic which I shall call 'extended definite clauses'; these are logical implications of the form APW where A is an atomic conclusion and W is any expression of first-order logic expressing a set of sufficient conditions for the conclusion A to hold. A set of such clauses has a declarative meaning which is quite independent of any computational uses it might have.

One way to use PROLOG is to take a set of extended definite clauses, rewrite them in PROLOG syntax, and then execute the result as a PROLOG program. But not every PROLOG program is a set of extended definite clauses written in PROLOG syntax, and not every PROLOG program can be given a coherent declarative reading. This is because PROLOG includes a number of language features which are nothing to do with logic. A PROLOG program which makes use of these features has a procedural reading only. It cannot be understood independently of its behaviour inside a machine. The projects described in this section have used PROLOG, not as a way of executing declarative representations expressed in logic, but as a procedural programming language in its own right.

Scholzbohm's program illustrates this procedural usage of PROLOG most clearly. The program operates by asking the user to supply the facts it needs to reach a conclusion. The program statement mixes conditions with procedure calls to generate the required dialogue and specify which the computation should proceed next. In this respect Scholzbohm's program is very similar to Hellabell's CORPTAX. Scholzbohm states explicitly the order in which questions
