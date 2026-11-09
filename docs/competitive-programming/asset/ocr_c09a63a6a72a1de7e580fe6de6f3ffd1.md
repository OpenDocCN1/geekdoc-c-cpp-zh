# Chapter 6

# # String Processing

> > *Human Genome has approximately 3.3 Giga base-pairs*
> > — Human Genome Project

> > *In this chapter, we present one more topic that is tested in ICPC, namely: string processing. Processing (long) string is quite common in the research field of bioinformatics and some of such problems are presented as contest problems in ICPC.*

# ## 6.1 Overview and Motivation

Although not as frequent as graph and mathematics problems in the previous two chapters, string processing problems are also found in recent ICPCs (see Table 6.1). Some string-related problems have huge inputs. Thus the solution must use efficient data structures and algorithms for string.

| LA | Problem Name | Source | String Problem (Algorithm) |
|---|---|---|---|
| 2460 | Searching Sequence ... | Singapore01 | Classical String Alignment Problem (DP) |
| 2972 | A DP Problem | Tehran03 | Tokenize Linear Equation |
| 3170 | AGTC | Manila06 | Classical String Edit Problem (DP) |
| 3669 | String Cutting | Hanoi06 | Ad Hoc String Processing |
| 3791 | Team Arrangement | Tehran06 | Ad Hoc String Processing |
| 3901 | Editor | Seoul07 | Longest Repeated Substring |
| 3999 | The longest constant gene | Danang07 | Longest Common Substring of >= 2 strings |
| 4200 | Find the Format String | Dhaka08 | Ad Hoc String Processing |
| 4657 | Top-10 | Jakarta09 | Suffix Array + Segment Tree |

Table 6.1: Some String Processing Problems in Recent ACM ICPC Asia Regional

# ## 6.2 Ad Hoc String Processing Problems

We start this chapter by mentioning Ad Hoc string processing problems. They are contest problems involving string that require no more than basic programming skills. We only need to read the requirements in the problem description carefully and code it. Sometimes, pure character array (a.k.a. string) manipulation is sufficient. Sometimes, we need string libraries like C <string.h>,