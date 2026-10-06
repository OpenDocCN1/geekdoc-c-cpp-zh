# 8.6. THE FUTURE FOR DSS POLICY FORMULATION SUPPORT

The prototypes developed in the course of this project have, we believe, quite convincingly demonstrated the feasibility of providing this kind of advanced decision support for DSS policy makers. Nevertheless, there are many more aspects to the support that could be offered that are not apparent in P3 which we have given some, and sometimes consider- thought to. In this final section we consider some of before presenting our view of what an installed DSS policy formulation system might look like.

# 8.6.1. What to do with P3

Firstly, there are several sections of the functionality of P3 which were specified but were not implemented due to lack of programming resource. It would be possible to do further development to P3 to add the facility to use arguments in our argument format as queries to the logical model of the legislation. This would leave it still incomplete. To finish P3, the missing two stages of the policy process, evaluation and rationalization, would need to be added. There are also several more query types that should be implemented (such as compare, and statistics). The rule base revision tool specified for P3 could then be added to complete the specified functionality.

# 8.6.2. P4

Beyond the additions mentioned above, which would be necessary to fin-ish P3, there are several extra facilities that could be included go beyond the P3 specification. We might think of a system with these additional features as P4. We can think of the extra features of P4 as being either developments to the P3 functionality or additions to P3. In the "developments" category we might have:

+   1. Improvements to the argument form. At present this allows the con-struction of networks (chains) of micro-arguments. Chains as well as micro-arguments are labelled and can be used in other arguments permitting a degree of meta-argumentation. There is no sup-port for the construction of higher-level (macro) arguments, and there is no use of qualifiers in micro-arguments and is no typing of micro-arguments. All of these things are possible and it is possible to conceive of a support system making good use of such features.

+   2. More support for evaluation. In the present design, the evaluation stage is by far the most poorly supported. It is possible to add a higher degree of automation if we have a more developed argument form. Arguments of certain types (arguments from authority, say) could be ranked as of inherently lower validity than others (logical arguments, for instance), Argument qualifiers could form the basis of a Ranking. The attaching of cost and benefit weightings could also