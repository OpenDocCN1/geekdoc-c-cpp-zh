# Forward- or reverse-mode automatic differentiation: What's the difference?

Birthe van den Berg a,*, Tom Schrijvers a, James McKinna b, Alexander Vandenbroucke c

a KU Leuven, Celestijnenlaan 200A, Leuven, Belgium b Heriot-Watt University, Edinburgh Campus, G2, Edinburgh EH14 4AS, United Kingdom c Standard Chartered, 1 Basinghall Avenue, London, EC2V 5DD, United Kingdom

# ARTICLE INFO

Article history:
Received 22 December 2022
Revised 22 February 2023
Accepted 9 August 2023
Available online 15 August 2023

Keywords:
Automatic differentiation
Cayley representation
Semimodules
Nagata idealization
Kronecker

# ABSTRACT

Automatic differentiation (AD) has been a topic of interest for researchers in many disciplines, with increased popularity since its application to machine learning and neural networks. Although many researchers appreciate and know how to apply AD, it remains a challenge to truly understand the underlying processes. From an algebraic point of view, however, AD use cases appear natural: it originates from the differentiation of variants. In this work, we use Algebraic Feature Grammars to formalize two different AD variants, leveraging Haskell to illustrate our observations. Our findings stem from three fundamental algebraic abstractions: (1) the notion of semimodule, (2) Nagata’s construction of the ‘idealization of a module’, and (3) Kronecker’s delta function, that together allow us to write a single-line abstract definition of AD. From this single-line definition, and by instantiating our algebraic structures in various ways, we derive different AD variants, that have (almost) the same computational cost, but different properties, mainly in terms of (asymptotic) computational complexity. We show how the different variants obtained by means of Kronecker isomorphisms, a further elaboration of our Haskell infrastructure which guarantees correctness by construction. With this framework in place, this paper seeks to make AD variants more comprehensible, taking an algebraic perspective on the matter. © 2023 The Author(s). Published by Elsevier B.V. This is an open access article under the CC BY license (http://creativecommons.org/licenses/by/4.0/).

# 1. Introduction

Many algorithms in artificial intelligence crucially depend not only on the efficient large-scale evaluation of arithmetic expressions, but also on the evaluation of their partial derivatives at specific points [1,2]. Symbolic and numerical differentiation can be used for these computations but suffer from performance and accuracy issues, respectively. As a consequence, there is much interest in a third approach, called automatic differentiation (AD) [3]. AD efficiently and accurately evaluates the derivatives of any computation composed of basic arithmetic and exponential, logarithmic, and trigonometric functions.

The orthodox accounts of automatic differentiation, since its first introduction by Wengert [3], emphasise it as a whole-program transformation. It is coupled with a shift from evaluation of the primitive operations of the underlying language of numerical computation to those on the so-called dual numbers (due originally to Clifford [4], considerably predating