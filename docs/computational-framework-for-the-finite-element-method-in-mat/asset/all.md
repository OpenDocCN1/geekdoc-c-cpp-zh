![](images/cover.jpg)

![Cover: Computational Framework for the Finite Element Method in MATLAB® and Python, written by Pavel Sumets, published by CRC Press, Taylor and Francis Group, Boca Raton, London, New York, CRC Press is an imprint of the Taylor and Francis Group, an informa business; a Chapman and Hall book.](images/cover.jpg)

MATLAB^® is a trademark of The MathWorks, Inc. and is used with permission. The MathWorks does not warrant the accuracy of the text or exercises in this book. This book's use or discussion of MATLAB^® software or related products does not constitute endorsement or sponsorship by The MathWorks of a particular pedagogical approach or particular use of the MATLAB^® software.

First edition published 2023

by CRC Press

6000 Broken Sound Parkway NW, Suite 300, Boca Raton, FL 33487-2742

and by CRC Press

4 Park Square, Milton Park, Abingdon, Oxon, OX14 4RN

© 2023 Taylor & Francis, LLC

*CRC Press is an imprint of Taylor & Francis Group, LLC*

Reasonable efforts have been made to publish reliable data and information, but the author and publisher cannot assume responsibility for the validity of all materials or the consequences of their use. The authors and publishers have attempted to trace the copyright holders of all material reproduced in this publication and apologize to copyright holders if permission to publish in this form has not been obtained. If any copyright material has not been acknowledged please write and let us know so we may rectify in any future reprint.

Except as permitted under U.S. Copyright Law, no part of this book may be reprinted, reproduced, transmitted, or utilized in any form by any electronic, mechanical, or other means, now known or hereafter invented, including photocopying, microfilming, and recording, or in any information storage or retrieval system, without written permission from the publishers.

For permission to photocopy or use material electronically from this work, access [www.copyright.com](http://www.copyright.com) or contact the Copyright Clearance Center, Inc. (CCC), 222 Rosewood Drive, Danvers, MA 01923, 978-750-8400\. For works that are not available on CCC please contact [mpkbookspermissions@tandf.co.uk](mailto:mpkbookspermissions@tandf.co.uk)

*Trademark notice:* Product or corporate names may be trademarks or registered trademarks and are used only for identification and explanation without intent to infringe.

ISBN: 978-1-032-20925-8 (hbk)

ISBN: 978-1-032-20927-2 (pbk)

ISBN: 978-1-003-26597-9 (ebk)

DOI: [10.1201/9781003265979](https://doi.org/10.1201/9781003265979)

Typeset in LM Roman font

by KnowledgeWorks Global Ltd.

*Publisher's note:* This book has been prepared from camera-ready copy provided by the authors.

# Introduction

IF you are studying or working in the area of engineering, applied mathematics or physics, it is very likely that you have already heard about the finite element method (FEM). Probably, you have readsome literature on FEM and have tried to solve your particular problem using some FEM software package. Based on my own experience of doing so, it is not easy for the newcomer to get into the subject matter. Things become more complicated if you are a researcher and try to solve a nonstandard problem, which requires building customized programming code. Apart from the underlying mathematics, implementing FEM involves scientific programming, which includes coding various numerical methods such as polynomial interpolation, integrating with quadrature rules and a linear solver for matrix equations. Not to mention that building geometric representation for a particular customized problem is not always a trivial problem, all these tasks form quite a complicated FEM algorithm to be solved. Probably, implementing each individual component of the algorithm does not represent a challenge, but combining them all together in one interconnected system which should work efficiently and correctly is what makes FEM implementation challenging.

When an engineer or researcher faces a need to solve a problem using FEM, basically, there are three possible options: use existing standard FEM software packages, rewrite and optimize some third-party FEM library for particular needs or write everything from scratch. Obviously, if someone writes everything from scratch, the subject knowledge should cover all aspects of an underlying FEM algorithm. The advantage of having comprehensive knowledge about how FEM works is that it allows us to understand any existing FEM software packages as well. The content of this book is written with an idea to give necessary knowledge to develop numerical coding skills and become flexible with solving FEM.

**Who this book is intended for:**

This book is for those who want to gain skills in scientific programming numerical methods and better understand their advantages and drawbacks. Although the pivot point of the book is the FEM algorithm, various complementary tasks are considered. To be specific, the book provides a programming framework for coding linear FEM algorithms using the matrix-based MATLAB^® language and the Python scripting language in application to solving ordinary and partial differential equations. Special attention is paid to building numerical algorithms and its efficient implementation for both one- and two-dimensional problems. A reader can follow a step-by-step process of developing algorithms with explanations of their underlying mathematics and how to put them into MATLAB and Python code with corresponding analysis of their efficiency.

The content is focussed on aspects of numerical methods and coding FEM algorithms rather than FEM mathematical analysis; however, basic mathematical formulations for numerical techniques needed to implement FEM algorithms are provided.

**Level of presentation**:

The mathematical background is assumed to be covered by matrix algebra, vector calculus and the basics of ordinary and partial differential equations. It is going to be a demonstration of how the FEM works in the one- and two-dimensional case, written as applied mathematicians usually write it. The content throughout the book is not restricted to either Laplace or Poisson equations but rather covers general linear elliptic boundary value problems. Unlike the majority of the books on the FEM method which imply that a reader is familiar with structural mechanics, the current book is based on more generic formulations without assuming any mechanics background. Structural finite elements are not considered in examples and they are not discussed at all since, contrary to expectations, the structural elements are much more complicated to describe and use. They are left to an advanced FEM course. The book has a number of appendices which contain more detailed explanations of the numerical methods used in the main body of the book, so a reader can refresh or enrich their corresponding knowledge.

We use MATLAB and Python as programming languages to code the steps of the FEM algorithm. Throughout the book, the ideas of coding are illustrated using MATLAB with complementary translation to Python as well. Providing the code examples in both programming languages is done to add flexibility in framework implementation.

In terms of programming background, it is expected that a reader is familiar with basic matrix and vector manipulation using MATLAB and the NumPy package in Python. Every code example given in the book is explained in detail so that even a programmer with little experience could understand the underlying algorithm logic and implementation. We pay attention to an efficient programming style using sparse matrices.

**Distinctive features of the book**:

There is a large number of books on FEM including FEM mathematical analysis, coding FEM and solving application problems using FEM (mostly problems on mechanics). However, not many of them cover both theory and numerical implementation with coding examples. Usually, the programming implementation comes as complementary to the theoretical part just to illustrate implementation for basic simple cases. Very often, programming implementation is provided for specific application problems with tailored code, and the majority of these applications comes from the structural mechanics.

The current book is designed with an idea to describe FEM algorithm implementation itself and to do this in the most generic formulation so as to make it possible to apply this algorithm to as many application problems as possible. Here, the theoretical part is given as much as needed to implement the corresponding numerical methods which are part of the FEM algorithm. The book pays attention to the important practical details which arise when an engineer writes programming code. Overall, the book considers the FEM method from the scientific programming point of view.

**Topics covered by the book content**:

The content of the book is divided into six chapters and covers the following subjects:

*   Lagrange interpolating polynomials;

*   quadrature rules for numerical integration;

*   defining parameters of the FEM and its influence on solution errors;

*   calculating matrices of the FEM;

*   assembling matrices of the FEM;

*   incorporating boundary conditions into FEM matrices;

*   FEM data structures;

*   defining geometry and building two-dimensional triangular mesh;

*   adaptation to curved boundaries (isoparametric finite elements);

*   solving model problems using FEM.

We shall start with formulation of the model boundary value problem for the linear one-dimensional ordinary differential equation. Then, by introducing interpolating functions and finite elements, FEM algorithms for solving model problems are derived. The two-dimensional problem for a linear partial differential equation is considered afterwards and the corresponding two-dimensional FEM algorithms are derived. Each step of the algorithms is provided in detail with programming function implementations. We discuss data structures to represent mesh triangulation and boundary conditions, and compare different approaches of the matrices assembling process. Full programming code is given for an example problem with validating computational efficiency.

The source code for listings in the book is downloadable and can be found in the repository [https://github.com/psumets/FEM_lib](https://github.com)

# Background and Basic Concepts

THE finite element method (FEM) is a numerical method to solve ordinary and partial differential equations arising in mathematical modelling. Originally developed for solving problems in solid-state mechanics, it proved to be efficient and robust in various practical applications ranging from traditional fields of structural analysis, heat transfer, fluid flow, mass transport and electromagnetic potential, to simulating geometry deformation in computer character animation.

The fundamental idea of the FEM is subdividing the computational domain into smaller and simpler parts that are called finite elements, and finding local solutions within the boundary of these elements. By stitching the individual solutions on final elements back together, a global solution can be obtained. Some of the FEM advantages are the ability of accurate representation of complex geometry, capture of local effects and easy solution representation.

The history of the method is quite instructive. FEM concepts were initially introduced by Courant in 1943 in his work on solving the torsion problem, but this work did not attract much attention. Later, in the 1950s, structural engineers put the FEM on the map as a practical technique for solving their elasticity problem. The method had now become an important technique from both the practical and theoretical point of view, and the number of the method's applications began to increase at a tremendous rate. In the 1970s, mathematicians gave a comprehensive account of the method and its underlying theory. By the current time, the FEM has evolved into a universal tool for solving differential equations numerically. Numerous software packages adapted FEM to use with applications in all areas of computational physics and engineering. ANSYS, ADINA and LS-DYNA are examples of general-purpose computer codes for industrial users of the FEM.

Any numerical modelling of a phenomenon starts with formulating a *mathematical model* to be solved. Then, a *numerical model* is constructed that can be solved using computers. The final stage is development of a *computer model* (computer code) to simulate behaviour of the system. The FEM represents a numerical model, so it describes how to transform model equations, geometry and boundary conditions into a discretized form suitable to be consumed by numerical methods. An original mathematical model could have various forms and the resulting numerical model varies as well, but the FEM approach dictates a certain tactic of obtaining a numerical model and it follows certain basic concepts. As such, algorithms of the FEM can be considered as universal tools to approach numerical modelling. Finally, a computer model represents a software package which usually has a form of library with computer implementation of numerical methods that make up FEM algorithms (for example, numerical integration or a linear solver). Building a library code is an art of scientific programming which implies not only good knowledge of the mathematics behind the numerical methods but good programming skills as well. Choice of programming language affects all of the development process as every language has its own unique features and it could come with existing numerical libraries which can be reused or tailored for use with the FEM. Also, very often the code should be optimized to have good performance with the lowest possible calculation error. In case of FEM, a numerical model is often modified slightly so as to take shape of an optimized algorithm which is ready to be coded.

Let us outline the main steps of solving a problem using FEM. As a starting point, we have a mathematical model formulated in terms of a differential equation along with geometry and boundary conditions. First, this model needs to be converted in the form of integral equations with integrals over a geometry domain (in some cases, the original mathematical model is already expressed in an integral form). Once the integral formulation is obtained, the next step is to perform discretization when continuous variables or functions are transformed into discrete counterparts. Discretization includes splitting the geometry domain into individual small patches (final elements) and representing initially continuous functions and integrals as combinations of its interpolation over finite elements. In other words, the solution is sought in the form of piecewise interpolation and coefficients of this interpolation are unknowns which can be found from the discrete model representation. Usually, after discretization, the model transforms into a system of equations which could be either linear or nonlinear, depending on the initial form of the differential equation. The final step is to solve the system and represent the final solution through a piecewise interpolating polynomial.

Programming FEM involves coding various numerical methods and binding them together into one pipeline. It is worth noting that every piece of the pipeline matters as any error introduced at any stage propagates further with accumulative effect which could invalidate the final result. That is why coding numerical implementation is an important part of numerical simulation which should not be underestimated. At a high level, coding includes the following main stages: Firstly, an algorithm of geometry discretization comes into play where final elements are generated. Then, based on the shape and distribution of these elements, implementation of particular numerical integration methods has to be coded. The next important part is to define an algorithm of assembling all these calculated values over individual finite elements into a matrix which forms linear system to be solved numerically.

Once the FEM algorithm is coded, validation is carried out to make sure that the implementation is correct. This is usually done against a benchmark with a known analytical solution so that we can estimate error and convergence of the method with various discretization parameters.

There are a large number of books on FEM including FEM mathematical analysis, coding FEM and solving application problems using FEM which could be helpful for understanding FEM algorithms. For example, a reader could find a comprehensive FEM analysis in [[1](#ref01.xhtml_refbib_1)] which covers finite elements of different types. The book by [[3](#ref01.xhtml_refbib_3)] is focussed on steady-state boundary value problems. It contains thorough theoretical and practical aspects of implementing FEM and explains how to write a finite element code from scratch. MATLAB implementation of FEM algorithms with detailed descriptions of numerical analysis and meshing techniques can be found in [[5](#ref01.xhtml_refbib_5)] and [[2](#ref01.xhtml_refbib_2)]. Reading [[4](#ref01.xhtml_refbib_4)] and [[7](#ref01.xhtml_refbib_7)] is useful to learn about using Python for scientific computing. For better understanding of how to use specific MATLAB tools to solve differential equations, see documentation [[6](#ref01.xhtml_refbib_6)].

# Chapter 1 Finite Element Method for the One-Dimensional Boundary Value Problem

DOI: [10.1201/9781003265979-1](https://doi.org/10.1201/9781003265979-1)

IT was mentioned in the introduction of basic concepts that the development of the finite element method (FEM) in practical terms was established by engineers to solve their structural problems. For this reason, the FEM is usually approached through considering displacement of a system of linear springs under applied force. This technique is developed from the stiffness approach applied to structural problems and equations arising from this technique are force-displacement relationships which model specific mechanics. Unlike this conventional approach, the method of introducing FEM in this book is based on broader formulation considering a generic differential equation without any structural mechanics reference. All particular problems, including structural ones, can be modelled as a special case of this generic equation.

In this chapter we obtain FEM algorithm for linear one-dimensional second-order ordinary differential equation (ODE) with mixed boundary conditions. First, we derive integral equation for the boundary value problem and outline basic approach of the FEM. Then, finite elements and basis functions are introduced along with polynomial interpolation techniques. We show how the integral equation can be discretized with finite elements and how the FEM is reduced to solving linear system.

## GLOSSARY

****u**, **v**, …:** vectors are written using bold fonts.

**(**u** ⋅ **v**):** dot product of two vectors, $\mathbf{\mathbf{u}} \cdot \mathbf{\mathbf{v}} = {\sum\limits_{i = 1}^{n}{u_{i}v_{i}}}$.

***U*, *V*, …:** matrices are denoted by capital letters.

***f*(*x*):** a function of a single variable.

***f*^′, *f*^″, …:** derivatives of a single variable function *f*(*x*).

***C*(*a*, *b*):** set of continuous on the interval (*a*, *b*) functions.

***C*^(*k*)(*a*, *b*):** set of continuous functions that have continuous first *k* derivatives.

***L*[2](*a*, *b*):** space of functions defined on (*a*, *b*) for which the second power of the absolute value is Lebesgue integrable. If *v*(*x*) ∈ *L*[2](*a*, *b*), then ∥*v*∥[*L*[2]]² = ∫[*a*]^(*b*)|*v*|[2]*d**x* < ∞.

***H*¹(*a*, *b*):** Sobolev space defined as *H*¹(*a*, *b*) :  = {*v* ∈ *L*[2](*a*, *b*) : *v*^′ ∈ *L*[2](*a*, *b*)}. If *v*(*x*) ∈ *H*¹(*a*, *b*), then ∥*v*∥[*H*¹]² = ∫[*a*]^(*b*)(|*v*^′|²)*d**x* < ∞.

**𝒢[*m*]:** set of polynomials of degree not greater than *m*.

## 1.1 FORMULATION OF THE BOUNDARY VALUE PROBLEM FOR LINEAR SECOND-ORDER ODE

Throughout the chapter, we consider linear ODE of the form

$$\begin{array}{l} {- \left( {c(x)u'(x)} \right)' + b(x)u'(x) + a(x)u(x) = f(x),\quad x \in (s_{0},s_{1}).} \end{array}$$(1.1)

Here, *c*(*x*), *b*(*x*), *a*(*x*) and *f*(*x*) are known functions; *u*(*x*) is unknown function to be found, and *u*^′ = *d**u*/*d**x*. It is assumed that *c* ∈ *C*¹[*s*[0], *s*[1]]; *b*, *a*, *f* ∈ *C*[*s*[0], *s*[1]] and *c*(*x*) > 0 ∀*x* ∈ [*s*[0], *s*[1]]. Negative sign in equation (1.1) is for convenience and the reason of keeping this sign will be clarified later. We are going to derive FEM algorithm, which is based on equation (1.1).

By considering equation of the form (1.1), we cover the problem in most generic formulations which allows solving specific problems as well; for example, when *c*(*x*) = −1, *b*(*x*) = *a*(*x*) = 0, we come to Poisson equation, *u*^″(*x*) = *f*(*x*). Another example could be one-dimensional steady-state heat equation with heat sink, −(*c*(*x*)*u*^′(*x*))^′) + *u*(*x*) = 0, where *u*(*x*) is a temperature and *c*(*x*) is a thermal conductivity. This equation is a special case of more generic one (1.1).

Note that an ODE allows multiple solutions and addition conditions are needed to obtain unique solution. To find a unique solution to equation (1.1), two boundary conditions are needed (second-order equation needs two extra conditions to be uniquely resolved). If both boundary conditions are specified at a single point (either *s*[0] or *s*[1]), then this problem is called *Cauchy problem*. Problem (1.1) with boundary conditions specified at both, *s*[0] and *s*[1], boundary points is called *boundary value problem* (BVP). Cauchy problem and BVP have distinct properties and solution methods. This book is focussed on BVP only.

Let us consider various types of conditions, which can be specified at a boundary point *s* (here, *s* could be any of {*s*[0], *s*[1]}). For example, solution is known at point *s* with *u*(*s*) = *u*[*s*], which gives us Dirichlet (or first-type) boundary condition. Another situation is when a derivative of solution at boundary point is defined *u*^′(*s*) = *u*[*s*]^′ which is called Neumann (or second-type) boundary condition. Combination of Dirichlet and Neumann boundary conditions gives Robin (or third-type) boundary condition having form *u*^′(*s*) + *ρ**u*(*s*) = *μ*, or ±(*c**u*^′)(*s*) + *σ**u*(*s*) = *μ* with corresponding choice of *σ* and *μ* (here, function *c*(*x*) is a coefficient of equation (1.1)). Usually, these conditions have some meaning depending on particular application problem. For example, in application to the heat equation with *u*(*x*) being a temperature, Dirichlet boundary condition means that a temperature at a boundary point is known, and Neumann boundary condition specifies heat flux at a boundarypoint.

If boundary conditions (BC) of different types are given for a BVP, then it is called that a mixed boundary condition is defined. For example, problem (1.1) can be complemented by BC

$$\begin{array}{l} {u(s_{0}) = u_{s_{0}},\quad(cu')(s_{1}) + \sigma u(s_{1}) = \mu.} \end{array}$$(1.2)

Here, Dirichlet BC is specified at *s*[0] and Robin BC is given at *s*[1] which all together give mixed BC. Further, conditions (1.2) are used as a BC to find a unique solution to the problem (1.1). Now, let us give a definition of the solution function *u*(*x*).

It is assumed that there exists a unique solution *u*(*x*), and further we are focussed on solving BVP (1.1)–(1.2) using FEM. To reach this goal, we need to transform the problem to an integral equation which is shown in the next section.

## EXERCISE

*   ▶ To see clearly how solution property depends on particular BC, solve the equation

    $$\begin{array}{l} {u^{''} + 3u' - 4u = 0,\quad x \in (0,1)} \end{array}$$

    with two sets of BC:

    $$\begin{array}{l} {(\text{a})\quad u(0) = 1,u'(0) = 0;} \end{array}$$

    $$\begin{array}{l} {(\text{b})\quad u(0) = 1,u(1) = 0.} \end{array}$$

    Case (a) is Cauchy problem having solution, which increases exponentially while solution corresponding to case (b) decreases.

*   ▶ Unlike Cauchy problem, even a simple BVP could have no solution. Explore the problem:

    $$\begin{array}{l} {u^{''} + u = 0,\quad x \in (0,\pi),\quad u(0) = 1,\quad u(\pi) = \alpha,} \end{array}$$

    where *α* is a parameter. Find values of *α* for which solution exists. Is this solution unique?

*   ▶ Find solution to the problem

    $$\begin{array}{l} {- u^{''} + u = 0,\quad x \in (0,\pi),\quad u(0) = 1,\quad u(\pi) = \alpha,} \end{array}$$

    and show that it has unique solution for any value of parameter *α*.

## 1.2 INTEGRAL EQUATION

Let us transform the problems (1.1)–(1.2) into an integral equation suitable for applying FEM. There are several approaches of doing this, which include variational and projective methods. In this book we use projective method while variational approach is discussed in [Appendix A](#appA.xhtml_appA). Projective method is based on the orthogonal *L*[2] projection on the Sobolev space, *H*¹(*s*[0], *s*[1]).

In analogy with projection onto subspaces of ℝ^(*n*), (1.3) defines a projection of *f* onto *H*¹, since the difference *f* − *P**r*(*f*) is required to be orthogonal to all functions *v* in *H*¹ (see [figure 1.1](#chapter1.xhtml_fig1_1)).

![Image of a vector, a plane and orthogonal projection of a vector on a plane. A vector to be projected represents a function and a plane represents a set of functions belonging to a Sobolev space.](images/fig1_1.jpg)

[Figure 1.1:](#chapter1.xhtml_b1fig1_1) Illustration of *L*[2] orthogonal projection.

From [Definition 1.2](#chapter1.xhtml_defi1_2), it follows that *L*[2] projection can be viewed as a technique for approximating functions, which gives a weighted average approximation of function *f* by its projection and weights *v*(*x*)

$$\begin{array}{l} {\int\limits_{s_{0}}^{s_{1}}f(x)v(x)dx = \int\limits_{s_{0}}^{s_{1}}Pr(f)v(x)dx,\quad\begin{array}{l} {Pr(f) \in H^{1}(s_{0},s_{1}),} \\ {\forall v(x) \in H^{1}(s_{0},s_{1}).} \end{array}} \end{array}$$(1.4)

In this context, the function *v*(*x*) is referred to as a weight or *test function*. Now, considering *f* in (1.4) to be right hand side of equation (1.1), projection *P**r*(*f*) corresponds to projecting left hand side of equation (1.1) on to the space *H*¹(*s*[0], *s*[1]), as a result we obtain an integral expression

$$\begin{array}{ll} {\int\limits_{s_{0}}^{s_{1}}\left( {\left( {- c(x)u'(x)} \right)' + b(x)u'(x) + a(x)u(x)} \right)} & {v(x)dx} \\ & {= \int\limits_{s_{0}}^{s_{1}}f(x)v(x)dx,} \end{array}$$(1.5)

where *u*(*x*), *v*(*x*) ∈ *H*¹(*s*[0], *s*[1]). The intuition behind representing original BVP (1.1) in the integral form (1.5) can be viewed as follows: If *u*(*x*) were an exact solution over the whole interval (*s*[0], *s*[1]), equation (1.1) would be exact everywhere. But, given that in real engineering problems this will not be the case, we try to obtain an approximate solution *u*(*x*) for which it meets the BVP equation in a spatially averaged sense (1.5). In other words, the residual or error (i.e., the amount by which the differential equation is not satisfied exactly at a point) is distributed evenly over the interval.

Let us rewrite expression (1.5) in the form with integrals over individual terms

$$\begin{array}{ll} {- \int\limits_{s_{0}}^{s_{1}}\left( {c(x)u'(x)} \right)'v(x)dx} & {+ \int\limits_{s_{0}}^{s_{1}}b(x)u'(x)v(x)dx} \\ + & {\int\limits_{s_{0}}^{s_{1}}a(x)u(x)v(x)dx = \int\limits_{s_{0}}^{s_{1}}f(x)v(x)dx.} \end{array}$$(1.6)

By applying integration by parts[¹](#chapter1.xhtml_fn1_1) to the first integral in (1.2) we come to

$$\begin{array}{l} {\int\limits_{s_{0}}^{s_{1}}(cu'v' + bu'v + auv)dx - (cu'v)|_{s_{0}}^{s_{1}} = \int\limits_{s_{0}}^{s_{1}}fvdx.} \end{array}$$(1.7)

By inspecting second term in (1.7) and taking into account BC (1.2), we see that

$$\begin{array}{ll} {(cu'v)|_{s_{0}}^{s_{1}} = c(s_{1})} & {u{(s_{1})}'v(s_{1}) - c(s_{0})u{(s_{0})}'v(s_{0})} \\ & {\quad = \mu v(s_{1}) - \sigma u(s_{1})v(s_{1}) - c(s_{0})u{(s_{0})}'v(s_{0}).} \end{array}$$(1.8)

If function *v*(*x*) is defined so that *v*(*s*[0]) = 0, then it follows from (1.7) and (1.8) that

$$\begin{array}{l} {\int\limits_{s_{0}}^{s_{1}}\left( {cu'v' + bu'v + auv} \right)dx + \sigma u(s_{1})v(s_{1}) = \int\limits_{s_{0}}^{s_{1}}fvdx + \mu v(s_{1}).} \end{array}$$(1.9)

Expression (1.9) is an integral equation, and it can be seen that if *u*(*x*) is a solution to BVP (1.1)–(1.2), then it satisfies (1.9). Inverse would be valid if we complement integral equation (1.9) by the condition *u*(*s*[0]) = *u*[*s*[0]]. As a result, equation (1.1) and BC (1.2) are now transformed into one expression (1.9) where *u*(*s*[0]) = *u*[*s*[0]] and *v*(*s*[0]) = 0. It is worth noting here that original BVP suggests that the solution *u* should have derivatives up to second order. On the other hand, the integral form (1.9) refers only to the first derivatives of *u*(*x*), which implies weaker conditions on property of solution function. Moreover, due to property of Sobolev space, *L*[2] projection *u*(*x*) does not require the function we seek to have continuous derivatives. As such, we relax some conditions on solution of BVP by saying that the function *u*(*x*) is now integrable continuous function having piecewise continuous derivatives of the first order (in other words, it belongs to Sobolev space). For this reason, (1.9) is called a *weak form* of the original BVP. The integral weak form of (1.1)–(1.2) can now be defined in terms of the Sobolev space by introducing two subspaces

$$\begin{array}{ll} \mathcal{W} & {: = \left\{ w \in H^{1}(s_{0},s_{1}):w(s_{0}) = u_{s_{0}} \right\},} \\ \mathcal{W}^{0} & {: = \left\{ w \in H^{1}(s_{0},s_{1}):w(s_{0}) = 0 \right\},} \end{array}$$

as follows.

Obtaining expression (1.9) is the first step in the FEM formulation for the BVP. Next step is to represent solution through polynomial approximation. Since we consider *u*(*x*) to be piecewise smooth, piecewise polynomial interpolation is used to approximate *u*(*x*). Generally speaking, FEM can be expressed as following: *FEM=integral equation+piecewise polynomial interpolation*. In the next section we explore polynomial interpolation methods.

## EXERCISE

*   ▶ Prove that (1.1)–(1.2) follow from (1.9). Instruction: take any point *x*[0] ∈ (*s*[0], *s*[1]); consider an interval [*x*[0] − *h*, *x*[0] + *h*] ⊂ (*s*[0], *s*[1]) and use the expression (1.7) defined on this interval with *v* ∈ *C*¹[*s*[0], *s*[1]] and *v*(*x*) = 0 for *x* ∉ [*x*[0] − *h*, *x*[0] + *h*]; perform passage to the limit *h* → 0 and obtain (1.1).

*   ▶ Deduce integral equation and define sets 𝒲 and 𝒲⁰ for the problem (1.1) with following BC:

    *   (a) BC of the third order is specified at the point *s*[0] and BC of the first order at the point *s*[1].

    *   (b) BC of the third order is specified at both points, *s*[0] and *s*[1].

## 1.3 LAGRANGE INTERPOLATING POLYNOMIALS AND THE FINITE ELEMENT APPROXIMATION

Let us consider function approximation methods. Here, we discuss two approaches: using single global interpolating polynomial and piecewise polynomial interpolation. Both approaches are based on Lagrange interpolating polynomials. Since the concept of piecewise interpolation is an extension of the global one, we start with considering global interpolation first.

### 1.3.1 Global Interpolating Polynomial

Let *u* = *u*(*x*) be a continuous on the closed interval [*s*[0], *s*[1]] function with defined set of nodes

$$\begin{array}{l} {s_{0} = x_{1} < x_{2} < \cdots < x_{m + 1} = s_{1},\quad h = s_{1} - s_{0},} \end{array}$$

and *u*[*i*] = *u*(*x*[*i*]), *i* = 1, …, *m* + 1. Then, there is a unique polynomial *u*[*h*] of degree not greater than *m* satisfying

$$\begin{array}{l} {u_{h}(x_{i}) = u_{i},\quad i = 1,\ldots,m + 1.} \end{array}$$(1.10)

Note that *u*[*h*](*x*) is not the same as *u*(*x*), but rather an approximation, which coincides with *u*(*x*) in a given set of nodes. Polynomial approximation *u*[*h*](*x*) can be created in different ways, but we are interested in Lagrange interpolating polynomials having the form

$$\begin{array}{l} {u_{h}(x) = {\sum\limits_{i = 1}^{m + 1}{u_{i}\varphi_{i}(x)}},\quad\varphi_{i}(x) = {\prod\limits_{j = 1,j \neq i}^{m + 1}\frac{x - x_{j}}{x_{i} - x_{j}}}.} \end{array}$$(1.11)

In other words, we seek an approximation in the form of linear combination of the polynomials *φ*[*i*](*x*) with known weights *u*[*i*].

It can be seen that

$$\begin{array}{l} {\varphi_{i} \in \mathcal{G}_{m},\quad\varphi_{i}(x_{j}) = \delta_{ij},\quad j = 1,\ldots,m + 1,} \end{array}$$

where 𝒢[*m*] denotes a set of polynomials of degree not greater than *m*, and *δ*[*i**j*] is the Kronecker delta.[²](#chapter1.xhtml_fn1_2) Functions *φ*[*i*](*x*) are called basis due to the fact that they form a basis in 𝒢[*m*] and any polynomial *p* ∈ 𝒢[*m*] can be represented through this basis (see 1.11). Particularly, if *u*[*h*] ≡ 1, then it follows from (1.11) that

$$\begin{array}{l} {{\sum\limits_{i = 1}^{m + 1}{\varphi_{i}(x)}} = 1,\quad x \in \lbrack s_{0},s_{1}\rbrack.} \end{array}$$(1.12)

It is worth noting that evaluating the basis functions *φ*[*i*](*x*) using expression (1.11) requires *O*(*m*²) operations which becomes computationally expensive for large values of *m*. For this reason, it is desired to rewrite (1.11) in another form of interpolation formula, which can be referred as the barycentric formula

$$\begin{array}{l} {\varphi_{i}(x) = w(x)\frac{\beta_{i}}{x - x_{i}},\quad u_{h}(x) = w(x){\sum\limits_{i = 1}^{m + 1}{\frac{\beta_{i}}{x - x_{i}}u_{i}}},} \end{array}$$(1.13)

where

$$\begin{array}{l} {w(x) = {\prod\limits_{j = 1}^{m + 1}{(x - x_{j})}},\quad\beta_{i} = \left( {\prod\limits_{j = 1,j \neq i}^{m + 1}{(x_{i} - x_{j})}} \right)^{- 1},} \end{array}$$(1.14)

and coefficients *β*[*i*] are called weights of barycentric formula. It follows from (1.12) that

$$\begin{array}{l} {1 = {\sum\limits_{i = 1}^{m + 1}{\varphi_{i}(x)}} = w(x){\sum\limits_{i = 1}^{m + 1}\frac{\beta_{i}}{x - x_{i}}},} \end{array}$$

and by using this fact, we come to the final form of the barycentric interpolation formula

$$\begin{array}{l} {u_{h}(x) = \left( {\sum\limits_{i = 1}^{m + 1}\frac{\beta_{i}}{x - x_{i}}} \right)^{- 1}{\sum\limits_{i = 1}^{m + 1}{\frac{\beta_{i}}{x - x_{i}}u_{i}}},} \end{array}$$(1.15)

and basis functions

$$\begin{array}{l} {\varphi_{i}(x) = \left( {\sum\limits_{i = 1}^{m + 1}\frac{\beta_{i}}{x - x_{i}}} \right)^{- 1}\frac{\beta_{i}}{x - x_{i}}.} \end{array}$$(1.16)

It is easy to see that calculations of *u*[*h*](*x*) using expression (1.15) for any given *x* require *O*(*m*) operations. Weights *β*[*i*] do not depend on *x* and ones precomputed can be reused for each evaluation of *u*[*h*](*x*).

An important property of representations (1.15)–(1.16) is that they remain valid when weights *β*[*i*] are multiplied by an arbitrary constant value. The weights in the denominator are exactly the same as in the numerator, and this means that any common factor in all the weights may be cancelled. As such, weights *β*[*i*] can be defined up to constant factor.

For particular case of nodes distribution, explicit formulas for barycentric weights can be given. For instance, in case of evenly spaced points *x*[*i* + 1] − *x*[*i*] = *h*/*m*, weights can be calculated through formula

$$\begin{array}{l} {\beta_{i} = {( - 1)}^{i}\frac{m!}{(m - i + 1)!(i - 1)!},\quad i = 1,\ldots,m + 1.} \end{array}$$(1.17)

To illustrate calculation of weights *β*[*i*], let us consider 4 nodes {*x*[1] = 0, *x*[2] = 1, *x*[3] = 2, *x*[4] = 3}. Using expression (1.14), we come to values {*β*[1] = −1/6, *β*[2] = 1/2, *β*[3] = −1/2, *β*[4] = 1/6}, while formula (1.17) gives {*β*[1] = −1, *β*[2] = 3, *β*[3] = −3, *β*[4] = 1}, which differ by factor 6; nevertheless, they can be equally used in (1.15)–(1.16). [Figure 1.2](#chapter1.xhtml_fig1_2) illustrates four basis functions created from the given four nodes and each basis is a polynomial of the third order. Note that using this basis allows to interpolate exactly any cubic polynomial (and polynomial of degree less than three), which is shown in [figure 1.3](#chapter1.xhtml_fig1_3).

![A graph with four lines illustrating Lagrange basis functions corresponding to four nodes on a finite element. Lines have sinusoidal shape so that to have unity value at the node with which they are associated and zeroth value at other nodes.](images/fig1_2.jpg)

[Figure 1.2:](#chapter1.xhtml_b1fig1_2) Lagrange basis functions corresponding to nodes {*x*[1] = 0, *x*[2] = 1, *x*[3] = 2, *x*[4] = 3}.

![Two parts image of graphs showing source functions and its interpolation. Part (a) shows two graphs running through 4 points and they are indistinguishable. The source function and interpolation are all cubic function. Part (b) shows two graphs running through 4 points with hitting interpolation nodes, but the graphs are not coincided. Interpolation with 4 nodes gives cubic function but source function is of forth order.](images/fig1_3.jpg)

[Figure 1.3:](#chapter1.xhtml_b1fig1_3) Examples of interpolations with four nodes corresponding to functions: (a) *u*(*x*) = 0.5(*x* − 1.5)³; (b) *u*(*x*) = 0.5(*x* − 1.5)⁴. Here, the dashed line is the source function and the solid line is the interpolation. Cubic function is interpolated exactly; however, the fourth-order polynomial is interpolated exactly only at nodes but not between nodes.

Accuracy and some drawbacks of the global approximation are discussed in [Appendix B](#appB.xhtml_appB), where it is shown that the strategy of increasing polynomial order to interpolate function having large number of interpolation nodes is not always a good approach. Below, we consider alternative approach representing piecewise polynomial interpolation.

### 1.3.2 Piecewise Polynomial Interpolation and the Finite Element Approximation

Now, we turn our attention to the piecewise interpolation, which is effectively a number of localized interpolation stitched together. Let us consider a set of *n* + 1 nodes defined on the interval [*s*[0], *s*[1]]

$$\begin{array}{l} {s_{0} = x_{1} < x_{2} < \cdots < x_{n + 1} = s_{1},} \end{array}$$

and subintervals *e*[*i*] = [*x*[*i*], *x*[*i* + 1]], *i* = 1, …, *n*. Then, a set of *m* + 1 different nodes are specified on each *e*[*i*] so that

$$\begin{array}{l} {x_{i} = x_{i}^{(1)} < x_{i}^{(2)} < \cdots < x_{i}^{(m + 1)} = x_{i + 1},} \end{array}$$

and the total number of nodes can be easily calculated to be *N* = *n**m* + 1. Given a function *u*(*x*) ∈ *C*[*s*[0], *s*[1]], its approximation *u*[*h*](*x*) ∈ *C*[*s*[0], *s*[1]] can be defined as follows:

$$\begin{array}{ll} & {u_{h}(x) \in \mathcal{G}_{m},\quad x \in e_{i},\quad i = 1,\ldots,n,} \\ & {u_{h}(x_{j}) = u(x_{j}),\quad j = 1,\ldots,N,} \end{array}$$

where *h* = max {*h*[*i*], *i* = 1, …, *n*}. In other words, $\lbrack s_{0},s_{1}\rbrack = {\underset{i = 1}{\overset{n}{\cup}}e_{i}}$ and function *u*(*x*) is interpolated on each subinterval *e*[*i*] through Lagrange polynomial of the *m*^(*t**h*) order.

We can see that each finite element is associated with continuous polynomial 𝒢[*m*], while the spline itself is a piecewise smooth continuous function, which is smooth on each subinterval *e*[*i*] and continuous across the interval [*s*[0], *s*[1]] (see [figure 1.4](#chapter1.xhtml_fig1_4)).

![A graph showing four lines of Lagrange basis functions corresponding to two finite elements. At the node of the finite element junction these functions are continuous but not smooth.](images/fig1_4.jpg)

[Figure 1.4:](#chapter1.xhtml_b1fig1_4) Lagrange basis functions corresponding to the spline with two finite elements *e*[1] = [0, 3] and *e*[2] = [3, 6] having nodes {*x*[1] = 0, *x*[2] = 1, *x*[3] = 2, *x*[4] = 3, *x*[5] = 4, *x*[6] = 5, *x*[7] = 6}. It is seen that spline at the node *x*[4] = 3 is continuous but not smooth function.

Let us introduce a space of Lagrange splines of degree *m*

$$\begin{array}{l} {H_{h}^{m}(s_{0},s_{1}): = \left\{ w \in C\lbrack s_{0},s_{1}\rbrack:w(x) \in \mathcal{G}_{m},\, x \in e_{i},\, i = 1,\ldots,n \right\}.} \end{array}$$

Space *H*[*h*]^(*m*)(*s*[0], *s*[1]) is considered to be an approximation of the space *H*¹(*s*[0], *s*[1]), and *H*[*h*]^(*m*)(*s*[0], *s*[1]) ⊂ *H*¹(*s*[0], *s*[1]). Indeed, if *w*(*x*) ∈ *H*[*h*]^(*m*)(*s*[0], *s*[1]) then *w*(*x*) is a continuous and piecewise differentiable function which means that *w* ∈ *H*¹(*s*[0], *s*[1]). Analogously, approximations of the subspaces 𝒲 and 𝒲⁰ associated with integral equation (1.8) can be introduced.

$$\begin{array}{ll} \mathcal{W}_{h} & {: = \left\{ w \in H_{h}^{m}(s_{0},s_{1}):w(s_{0}) = u_{s_{0}} \right\},} \\ \mathcal{W}_{h}^{0} & {: = \left\{ w \in H_{h}^{m}(s_{0},s_{1}):w(s_{0}) = 0 \right\}.} \end{array}$$

Now, we have come to the state when we are ready to give a definition of the FEM corresponding to the BVP (1.1)–(1.2).

Next, we are going to explain how to find the approximate solution *u*[*h*] through reducing the problem to a linear system.

### 1.3.3 Linear System of the FEM

As shown above, the FEM of the BVP (1.1)–(1.2) solves equation (1.18) for unknown function *u*[*h*] and with arbitrary *v*[*h*]. Introducing a basis in *H*[*h*]^(*m*)(*s*[0], *s*[1]) allows reducing this problem to solving a linear system.

By considering the interval [*s*[0], *s*[1]] having *n* finite elements with *m* + 1 nodes each, we obtain the total number of *N* = *n**m* + 1 nodes, which can be enumerated from 1 to *N*:

$$\begin{array}{l} {s_{0} = x_{1} < x_{2} < \cdots < x_{N} = s_{1}.} \end{array}$$

Each node *x*[*i*] can be associated with a Lagrange basis function *φ*[*i*](*x*) ∈ *H*[*h*]^(*m*)(*s*[0], *s*[1]). Basis introduced in [section 1.3.1](#chapter1.xhtml_sec1_3_1) comprises smooth functions while *u*[*h*] ∈ *H*[*h*]^(*m*)(*s*[0], *s*[1]) is a piecewise smooth Lagrange spline and corresponding basis comprises piecewise smooth functions as well. Functions *φ*[*i*](*x*) have a property of taking nonzero value only in the corresponding finite element interval and zero otherwise. A basis function associated with a node, which is shared by two finite elements, is nonzero in these two elements (see [figure 1.5](#chapter1.xhtml_fig1_5)). As such, every *φ*[*i*](*x*) takes nonzero values in either one or two finite elements. Recall that *φ*[*i*](*x*[*j*]) = 0 if *i* ≠ *j*, and *φ*[*i*](*x*[*i*]) = 1.

![Two parts image of graphs showing basis functions associated with Lagrange spline. Part (a) shows a basis associated with a node located within a finite element and the graph only spans single element. Part (b) shows a basis associated with a node being junction node of two finite elements and a graph spans two elements.](images/fig1_5.jpg)

[Figure 1.5:](#chapter1.xhtml_b1fig1_5) Examples of basis functions associated with Lagrange spline having two finite elements *e*[1] = [0, 3], *e*[2] = [3, 6], and seven nodes {*x*[1] = 0, *x*[2] = 1, …, *x*[7] = 6}: (a) basis *φ*[2](*x*) corresponding to the node *x*[2] = 1; (b) basis *φ*[4](*x*) corresponding to the node *x*[4] = 3.

Let us denote function node values as *u*[*i*] = *u*[*h*](*x*[*i*]) and *v*[*i*] = *v*[*h*](*x*[*i*]), then any functions *u*[*h*] ∈ 𝒲[*h*] and *v*[*h*] ∈ 𝒲[*h*]⁰ can be decomposed in terms of basis *φ*[*i*](*x*) ∈ *H*[*h*]^(*m*)(*s*[0], *s*[1]) as following [³](#chapter1.xhtml_fn1_3)

$$\begin{array}{ll} {u_{h}(x)} & {= {\sum\limits_{j = 1}^{N}{u_{j}\varphi_{j}(x)}} = u_{s_{0}}\varphi_{1}(x) + {\sum\limits_{j = 2}^{N}{u_{j}\varphi_{j}(x)}},} \\ {v_{h}(x)} & {= {\sum\limits_{i = 1}^{N}{v_{i}\varphi_{i}(x)}},\quad x \in \lbrack s_{0},s_{1}\rbrack,} \end{array}$$(1.19)

or

$$\begin{array}{l} {u_{h}(x) = \mathbf{\mathbf{\varphi}}^{T}\mathbf{\mathbf{u}},\quad v_{h}(x) = \mathbf{\mathbf{\varphi}}^{T}\mathbf{\mathbf{v}},} \end{array}$$(1.20)

where **u** = {*u*[*i*]}[*i* = 1]^(*N*), **v** = {*v*[*i*]}[*i* = 1]^(*N*) and **φ** = {*φ*[*i*](*x*)}[*i* = 1]^(*N*) are column-vectors. By substituting (1.20) into equation (1.18), we come to the expression[⁴](#chapter1.xhtml_fn1_4)

$$\begin{array}{ll} \int\limits_{s_{0}}^{s_{1}} & {\left( {c\mathbf{\mathbf{v}}^{T}\mathbf{\mathbf{\varphi}}'{(\mathbf{\mathbf{\varphi}}')}^{T}\mathbf{\mathbf{u}} + b\mathbf{\mathbf{v}}^{T}\mathbf{\mathbf{\varphi}}{(\mathbf{\mathbf{\varphi}}')}^{T}\mathbf{\mathbf{u}} + a\mathbf{\mathbf{v}}^{T}\mathbf{\mathbf{\varphi}}\mathbf{\mathbf{\varphi}}^{T}\mathbf{\mathbf{u}}} \right)dx} \\ & {\text{\quad\quad}\text{\quad\quad} + \sigma\mathbf{\mathbf{v}}^{T}\mathbf{\mathbf{\varphi}}(s_{1})\mathbf{\mathbf{\varphi}}{(s_{1})}^{T}\mathbf{\mathbf{u}} = \int\limits_{s_{0}}^{s_{1}}f\mathbf{\mathbf{v}}^{T}\mathbf{\mathbf{\varphi}}dx + \mu\mathbf{\mathbf{v}}^{T}\mathbf{\mathbf{\varphi}}(s_{1}).} \end{array}$$(1.21)

By introducing a matrix *Ã* ∼ (*N* × *N*) and a vector **F̃** ∼ (*N* × 1) having components

$$\begin{array}{l} {{\widetilde{A}}_{ij} = \int\limits_{s_{0}}^{s_{1}}\left( {c\varphi_{i}'\varphi_{j}' + b\varphi_{i}\varphi_{j}' + a\varphi_{i}\varphi_{j}} \right)dx + \sigma\varphi_{i}(s_{1})\varphi_{j}(s_{1}),} \end{array}$$(1.22)

$$\begin{array}{l} {{\widetilde{F}}_{i} = \int\limits_{s_{0}}^{s_{1}}f\varphi_{i}dx + \mu\varphi_{i}(s_{1}),} \end{array}$$(1.23)

we can rewrite (1.21) in the form

$$\begin{array}{l} {\mathbf{\mathbf{v}}^{T}\widetilde{A}\mathbf{\mathbf{u}} = \mathbf{\mathbf{v}}^{T}\mathbf{\widetilde{F}}.} \end{array}$$(1.24)

Expression (1.24) can be seen as a sum of equations defined by the system *Ã***u** = **F̃** with each equation being multiplied by *v*[*i*] (actually, we can ignore the first equation since it corresponds to the value *v*[1] ≡ 0). Identity (1.24) is valid for arbitrary **v**, so by cancelling it out and by splitting the vector **u** into unknown and known parts, we come to the linear system

$$\begin{array}{l} {{\sum\limits_{j = 2}^{N}{\widetilde{A}}_{ij}}u_{j} = {\widetilde{F}}_{i} - u_{s_{0}}{\widetilde{A}}_{i1},\quad i = 2,\ldots,N.} \end{array}$$(1.25)

From solving linear system (1.25), we obtain values for *u*[*j*] and the final approximate solution to the BVP can be found using the first formula in (1.19).

Elements of the stiffness matrix and forcing vector are calculated using expressions (1.22) and (1.23); however, it is impractical to use these formulas directly. Below, we consider efficient method of assembling matrices and derive corresponding computational algorithm for calculating their elements.

## EXERCISE

*   ▶ Plot the Lagrange basis functions corresponding to the spline with final elements *e*[1] = [0, 1], *e*[2] = [1, 2] and *e*[3] = [2, 3] having nodes {*x*[1] = 0, *x*[2] = 1, *x*[3] = 2, *x*[4] = 3} (linear basis functions).

*   ▶ Deduce a linear system of the FEM corresponding to the following BC:

    *   (a) BC of the first order is specified at both points, *s*[0] and *s*[1].

    *   (b) BC of the third order is specified at both points, *s*[0] and *s*[1].

## 1.4 ILLUSTRATIVE PROBLEM

One of the reasons of the success of the FEM is that it may be applied to problems of great complexity; however, to use such problems for illustrative purpose tends to obscure the underlying ideas. In this section a simple problem is solved. Note that this is not to suggest that the FEM is the best method for solving such problems. In fact, there are other numerical methods available which are superior. However, this particular problem involves only small amount of algebra, and the algorithm ideas come through quite well.

Consider the BVP having the form

$$\begin{array}{l} {- u^{''} + u = x,\quad x \in (0,1),\quad u(0) = 1,\quad u'(1) = 1,} \end{array}$$(1.26)

with known exact solution

$$\begin{array}{l} {u = \frac{e^{2 - x} + e^{x}}{1 + e^{2}} + x.} \end{array}$$(1.27)

It can be seen from comparing with generic BVP (1.1)–(1.2) that the problem (1.26) corresponds to the coefficient values *c*(*x*) = 1, *b*(*x*) = 0, *a*(*x*) = 1, *σ*(*x*) = 0, *μ*(*x*) = 1. Consider a three-element discretization of *[*0,1*]* with nodes {*x*[1] = 0, *x*[2] = 1/3, *x*[3] = 2/3, *x*[4] = 1}.

$$\begin{array}{l} {e_{1} = \left\lbrack {0,\frac{1}{3}} \right\rbrack,\quad e_{2} = \left\lbrack {\frac{1}{3},\frac{2}{3}} \right\rbrack,\quad e_{2} = \left\lbrack {\frac{2}{3},1} \right\rbrack.} \end{array}$$(1.28)

There are four basis functions associated with four interpolation nodes which gives the following form of the approximate solution

$$\begin{array}{l} {u_{h} = u(0)\varphi_{1}(x) + u\left( \frac{1}{3} \right)\varphi_{2}(x) + u\left( \frac{2}{3} \right)\varphi_{3}(x) + u(1)\varphi_{4}(x).} \end{array}$$(1.29)

Function value *u*(0) = 1 is known from the BC and the rest values, *u*(1/2), *u*(2/3) and *u*(1) have to be found.

In each element there are just two nodes; hence, the interpolation polynomials for each element must be linear. Basis functions associated with each node are found from (1.11) and have the form

$$\begin{array}{ll} & {\varphi_{1}(x) = \left\{ \begin{array}{ll} {- 3x + 1,} & {0 \leq x \leq \frac{1}{3},} \\ {0,} & {\frac{1}{3} < x < 0,} \end{array}~ \right.} \end{array}$$(1.30)

$$\begin{array}{ll} & {\varphi_{2}(x) = \left\{ \begin{array}{ll} {3x,} & {0 \leq x \leq \frac{1}{3},} \\ {- 3x + 2,} & {\frac{1}{3} \leq x \leq \frac{2}{3},} \\ {0,} & {\frac{2}{3} < x < 0,} \end{array}~ \right.} \end{array}$$(1.31)

$$\begin{array}{ll} & {\varphi_{3}(x) = \left\{ \begin{array}{ll} {3x - 1,} & {\frac{1}{3} \leq x \leq \frac{2}{3},} \\ {- 3x + 3,} & {\frac{2}{3} \leq x \leq 1,} \\ {0,} & {1 < x < \frac{1}{3},} \end{array}~ \right.} \end{array}$$(1.32)

$$\begin{array}{ll} & {\varphi_{4}(x) = \left\{ \begin{array}{ll} {3x - 2,} & {\frac{2}{3} \leq x \leq 1,} \\ {0,} & {1 < x < \frac{2}{3}.} \end{array}~ \right.} \end{array}$$(1.33)

Basis functions are shown in [figure 1.6](#chapter1.xhtml_fig1_6) and they have so-called hat shapes. Note that *φ*[1] and *φ*[4] are nonzero over one element while *φ*[2] and *φ*[3] span two finite elements.

![A graph shows four linear basis functions having “hat” like shapes. Every basis function hits the value of one at the interpolation point with which it is associated and has zeroth value outside the boundary of corresponding finite element.](images/fig1_6.jpg)

[Figure 1.6:](#chapter1.xhtml_b1fig1_6) Lagrange linear basis functions corresponding to the spline with three finite elements *e*[1] = [0, 1/3], *e*[2] = [1/3, 2/3] and *e*[3] = [2/3, 1] having nodes {*x*[1] = 0, *x*[2] = 1/3, *x*[3] = 2/3, *x*[4] = 1}.

Now, elements of stiffness matrix (1.22) and forcing vector (1.23) have to be found to solve linear FEM system (1.25). First, consider the stiffness matrix in which elements are defined through

$$\begin{array}{l} {{\widetilde{A}}_{ij} = \int\limits_{0}^{1}\left( {\varphi_{i}'\varphi_{j}' + \varphi_{i}\varphi_{j}} \right)dx,\quad i,j = 1,2,3,4.} \end{array}$$(1.34)

It is worth looking into expressions for every element to better understand patterns and matrix formation.

$$\begin{array}{l} {{\widetilde{A}}_{11} = \int\limits_{0}^{1}\left( {\left( \varphi_{1}' \right)^{2} + \left( \varphi_{1} \right)^{2}} \right)dx = \int\limits_{0}^{\frac{1}{3}} \cdot dx,} \end{array}$$(1.35)

$$\begin{array}{l} {{\widetilde{A}}_{12} = {\widetilde{A}}_{21} = \int\limits_{0}^{1}\left( {\varphi_{1}'\varphi_{2}' + \varphi_{1}\varphi_{2}} \right)dx = \int\limits_{0}^{\frac{1}{3}} \cdot dx,} \end{array}$$(1.36)

$$\begin{array}{l} {{\widetilde{A}}_{13} = {\widetilde{A}}_{31} = \int\limits_{0}^{1}\left( {\varphi_{1}'\varphi_{3}' + \varphi_{1}\varphi_{3}} \right)dx = 0,} \end{array}$$(1.37)

$$\begin{array}{l} {{\widetilde{A}}_{14} = {\widetilde{A}}_{41} = \int\limits_{0}^{1}\left( {\varphi_{1}'\varphi_{4}' + \varphi_{1}\varphi_{4}} \right)dx = 0,} \end{array}$$(1.38)

$$\begin{array}{l} {{\widetilde{A}}_{22} = \int\limits_{0}^{1}\left( {\left( \varphi_{2}' \right)^{2} + \left( \varphi_{2} \right)^{2}} \right)dx = \int\limits_{0}^{\frac{1}{3}} \cdot dx + \int\limits_{\frac{1}{3}}^{\frac{2}{3}} \cdot dx,} \end{array}$$(1.39)

$$\begin{array}{l} {{\widetilde{A}}_{23} = {\widetilde{A}}_{32} = \int\limits_{0}^{1}\left( {\varphi_{2}'\varphi_{3}' + \varphi_{2}\varphi_{3}} \right)dx = \int\limits_{\frac{1}{3}}^{\frac{2}{3}} \cdot dx,} \end{array}$$(1.40)

$$\begin{array}{l} {{\widetilde{A}}_{24} = {\widetilde{A}}_{42} = \int\limits_{0}^{1}\left( {\varphi_{2}'\varphi_{4}' + \varphi_{2}\varphi_{4}} \right)dx = 0,} \end{array}$$(1.41)

$$\begin{array}{l} {{\widetilde{A}}_{33} = \int\limits_{0}^{1}\left( {\left( \varphi_{3}' \right)^{2} + \left( \varphi_{3} \right)^{2}} \right)dx = \int\limits_{\frac{1}{3}}^{\frac{2}{3}} \cdot dx + \int\limits_{\frac{2}{3}}^{1} \cdot dx,} \end{array}$$(1.42)

$$\begin{array}{l} {{\widetilde{A}}_{34} = {\widetilde{A}}_{43} = \int\limits_{0}^{1}\left( {\varphi_{3}'\varphi_{4}' + \varphi_{3}\varphi_{4}} \right)dx = \int\limits_{\frac{2}{3}}^{1} \cdot dx,} \end{array}$$(1.43)

$$\begin{array}{l} {{\widetilde{A}}_{44} = \int\limits_{0}^{1}\left( {\left( \varphi_{4}' \right)^{2} + \left( \varphi_{4} \right)^{2}} \right)dx = \int\limits_{\frac{2}{3}}^{1} \cdot dx.} \end{array}$$(1.44)

We can see that due to the symmetry of formula (1.34), index order is not important and the stiffness matrix becomes symmetrical. In addition, elements *Ã*[13], *Ã*[31], *Ã*[14], *Ã*[41], *Ã*[24] and *Ã*[42] equal to zero since corresponding, basis functions are non-overlapping, which gives zeroth integrands (the only coupling occurs between nodes associated with the same element). Also, the domain integrals over the interval *[*0,1*]* can be replaced by the sum of integrals taken separately over the finite elements and only those integrals can be left which have non-zero values. Elements *Ã*[22] and *Ã*[33] include two integrals because corresponding integrands are non-zero over two finite elements. As a result, the stiffness matrix can schematically be represented as follows:

$$\begin{array}{ll} & {\widetilde{A} = \left( \begin{array}{llll} * & * & 0 & 0 \\ * & * & * & 0 \\ 0 & * & * & * \\ 0 & 0 & * & * \end{array} \right) = \int\limits_{0}^{\frac{1}{3}} \cdot dx + \int\limits_{\frac{1}{3}}^{\frac{2}{3}} \cdot dx + \int\limits_{\frac{2}{3}}^{1} \cdot dx} \\ & {= \left( \begin{array}{llll} * & * & 0 & 0 \\ * & * & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{array} \right) + \left( \begin{array}{llll} 0 & 0 & 0 & 0 \\ 0 & * & * & 0 \\ 0 & * & * & 0 \\ 0 & 0 & 0 & 0 \end{array} \right) + \left( \begin{array}{llll} 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & * & * \\ 0 & 0 & * & * \end{array} \right)} \\ & {= {\overline{A}}^{e_{1}} + {\overline{A}}^{e_{2}} + {\overline{A}}^{e_{3}}.} \end{array}$$(1.45)

Here, ${\overline{A}}^{e_{1}},\,{\overline{A}}^{e_{2}}$ and ${\overline{A}}^{e_{3}}$ are local to each finite element stiffness matrices, which can be found separately and then summed up to obtain the matrix *Ã*. One more important observation from (1.45) is that matrices are sparse and *Ã* is a tridiagonal matrix.

Now, consider matrix ${\overline{A}}^{e_{1}}$ and calculate its first element integral

$$\begin{array}{ll} \left. {\overline{A}}_{11}^{e_{1}} = \int\limits_{0}^{\frac{1}{3}}\left( {{({( - 3x + 1)}')}^{2} + {( - 3x + 1)}^{2}} \right)dx = \middle| \begin{array}{l} {3x = \hat{x},\, dx = \frac{1}{3}d\hat{x},} \\ {\frac{d}{dx} = \frac{d}{d\hat{x}}\frac{d\hat{x}}{dx} = 3\frac{d}{d\hat{x}}} \end{array} \right. & | \\ {= \int\limits_{0}^{1}\left( {{(3{(1 - \hat{x})}')}^{2} + {(1 - \hat{x})}^{2}} \right)\frac{1}{3}d\hat{x} = \int\limits_{0}^{1}\left( {9 + {(1 - \hat{x})}^{2}} \right)\frac{1}{3}d\hat{x} = \frac{28}{9}.} & \end{array}$$(1.46)

Here, we introduce a new variable, *x̂* = 3*x*, so that *x* ∈ [0, 1/3] → *x̂* ∈ [0, 1], which results in basis functions to be *φ*[1](*x̂*) = 1 − *x̂* and *φ*[2](*x̂*) = *x̂*. This transformation, as we see later, allows simplifying calculation of integrals and applying unified numerical integration methods (quadrature rules). Similarly, integrals ${\overline{A}}_{12}^{e_{1}}$ and ${\overline{A}}_{22}^{e_{1}}$ can be found over *x̂* space.

$$\begin{array}{ll} & {{\overline{A}}_{12}^{e_{1}} = \int\limits_{0}^{\frac{1}{3}}\left( {{( - 3x + 1)}'{(3x)}' + ( - 3x + 1)(3x)} \right)dx} \\ & {= \int\limits_{0}^{1}\left( {3{(1 - \hat{x})}'3{\hat{x}}' + (1 - \hat{x})\hat{x}} \right)\frac{1}{3}d\hat{x} = \int\limits_{0}^{1}\left( {- 9 + (1 - \hat{x})\hat{x}} \right)\frac{1}{3}d\hat{x} = - \frac{53}{18}.} \end{array}$$(1.47)

$$\begin{array}{l} {{\overline{A}}_{22}^{e_{1}} = \int\limits_{0}^{1}\left( {{(3{\hat{x}}')}^{2} + {\hat{x}}^{2}} \right)\frac{1}{3}d\hat{x} = \int\limits_{0}^{1}\left( {9 + {\hat{x}}^{2}} \right)\frac{1}{3}d\hat{x} = \frac{28}{9}.} \end{array}$$(1.48)

Likewise, change of variables for the element *e*[2], *x̂* = 3*x* − 1, results in *x* ∈ [1/3, 2/3] → *x̂* ∈ [0, 1] and the basis functions are *φ*[2](*x̂*) = 1 − *x̂*, *φ*[3](*x̂*) = *x̂*. One important observation is that in the space *x̂* basis functions *φ*[2](*x̂*) and *φ*[3](*x̂*) over the element *e*[2] are identical to the functions *φ*[1](*x̂*) and *φ*[2](*x̂*) over the element *e*[1]. This leads to the fact that the integrals over the element *e*[2] are expected to be similar to those over the element *e*[1]

$$\begin{array}{l} {{\overline{A}}_{22}^{e_{2}} = \int\limits_{0}^{1}\left( {{(3{(1 - \hat{x})}')}^{2} + {(1 - \hat{x})}^{2}} \right)\frac{1}{3}d\hat{x} = \int\limits_{0}^{1}\left( {9 + {(1 - \hat{x})}^{2}} \right)\frac{1}{3}d\hat{x} = \frac{28}{9}.} \end{array}$$(1.49)

$$\begin{array}{l} {{\overline{A}}_{23}^{e_{2}} = \int\limits_{0}^{1}\left( {- 9 + (1 - \hat{x})\hat{x}} \right)\frac{1}{3}d\hat{x} = - \frac{53}{18}.} \end{array}$$(1.50)

$$\begin{array}{l} {{\overline{A}}_{33}^{e_{2}} = \int\limits_{0}^{1}\left( {9 + {\hat{x}}^{2}} \right)\frac{1}{3}d\hat{x} = \frac{28}{9}.} \end{array}$$(1.51)

Finally, for the last element *e*[3] we have *x̂* = 3*x* − 2 and *x* ∈ [2/3, 1] → *x̂* ∈ [0, 1] and *φ*[3](*x̂*) = 1 − *x̂*, *φ*[4](*x̂*) = *x̂*. Again, *φ*[3](*x̂*) and *φ*[4](*x̂*) over *e*[3] are identical to *φ*[2](*x̂*) and *φ*[3](*x̂*) over element *e*[2].

$$\begin{array}{l} {{\overline{A}}_{33}^{e_{3}} = \int\limits_{0}^{1}\left( {9 + {(1 - \hat{x})}^{2}} \right)\frac{1}{3}d\hat{x} = \frac{28}{9}.} \end{array}$$(1.52)

$$\begin{array}{l} {{\overline{A}}_{34}^{e_{3}} = \int\limits_{0}^{1}\left( {- 9 + (1 - \hat{x})\hat{x}} \right)\frac{1}{3}d\hat{x} = - \frac{53}{18}.} \end{array}$$(1.53)

$$\begin{array}{l} {{\overline{A}}_{44}^{e_{3}} = \int\limits_{0}^{1}\left( {9 + {\hat{x}}^{2}} \right)\frac{1}{3}d\hat{x} = \frac{28}{9}.} \end{array}$$(1.54)

Once the local stiffness matrices ${\overline{A}}^{e_{1}},\,{\overline{A}}^{e_{2}}$ and ${\overline{A}}^{e_{3}}$ are found, the final stiffness matrix can be assembled

$$\begin{array}{ll} & {\widetilde{A} = \left( \begin{array}{llll} \frac{28}{9} & {- \frac{53}{18}} & 0 & 0 \\ {- \frac{53}{18}} & \frac{28}{9} & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{array} \right) + \left( \begin{array}{llll} 0 & 0 & 0 & 0 \\ 0 & \frac{28}{9} & {- \frac{53}{18}} & 0 \\ 0 & {- \frac{53}{18}} & \frac{28}{9} & 0 \\ 0 & 0 & 0 & 0 \end{array} \right)} \\ & {+ \left( \begin{array}{llll} 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & \frac{28}{9} & {- \frac{53}{18}} \\ 0 & 0 & {- \frac{53}{18}} & \frac{28}{9} \end{array} \right) = \left( \begin{array}{llll} \frac{28}{9} & {- \frac{53}{18}} & 0 & 0 \\ {- \frac{53}{18}} & \frac{56}{9} & {- \frac{53}{18}} & 0 \\ 0 & {- \frac{53}{18}} & \frac{56}{9} & {- \frac{53}{18}} \\ 0 & 0 & {- \frac{53}{18}} & \frac{28}{9} \end{array} \right).} \end{array}$$(1.55)

For the forcing vector expression (1.23) gives

$$\begin{array}{l} {{\widetilde{F}}_{i} = \int\limits_{0}^{1}x\varphi_{i}dx + \varphi_{i}(1),\quad i = 1,2,3,4.} \end{array}$$(1.56)

Following the same logic as for stiffness matrix, let us consider individual integrals and deduce vector formation pattern.

$$\begin{array}{l} {{\widetilde{F}}_{1} = \int\limits_{0}^{1}x\varphi_{1}dx + \varphi_{1}(1) = \int\limits_{0}^{\frac{1}{3}}x\varphi_{1}dx,} \end{array}$$(1.57)

$$\begin{array}{l} {{\widetilde{F}}_{2} = \int\limits_{0}^{1}x\varphi_{2}dx + \varphi_{2}(1) = \int\limits_{0}^{\frac{1}{3}}x\varphi_{2}dx + \int\limits_{\frac{1}{3}}^{\frac{2}{3}}x\varphi_{2}dx,} \end{array}$$(1.58)

$$\begin{array}{l} {{\widetilde{F}}_{3} = \int\limits_{0}^{1}x\varphi_{3}dx + \varphi_{3}(1) = \int\limits_{\frac{1}{3}}^{\frac{2}{3}}x\varphi_{3}dx + \int\limits_{\frac{2}{3}}^{1}x\varphi_{3}dx,} \end{array}$$(1.59)

$$\begin{array}{l} {{\widetilde{F}}_{4} = \int\limits_{0}^{1}x\varphi_{4}dx + \varphi_{4}(1) = \int\limits_{\frac{2}{3}}^{1}x\varphi_{4}dx + 1.} \end{array}$$(1.60)

Here, we take into account the fact that only *φ*[4](1) is non-zero with the unity value. By splitting domain integral into individual integrals over the finite elements, we come to the following schematic representation for the forcing term

$$\begin{array}{ll} & {\widetilde{F} = \left( \begin{array}{l} * \\ * \\ * \\ * \end{array} \right) = \int\limits_{0}^{\frac{1}{3}} \cdot dx + \int\limits_{\frac{1}{3}}^{\frac{2}{3}} \cdot dx + \int\limits_{\frac{2}{3}}^{1} \cdot dx + \varphi_{4}(1)} \\ & {= \left( \begin{array}{l} * \\ * \\ 0 \\ 0 \end{array} \right) + \left( \begin{array}{l} 0 \\ * \\ * \\ 0 \end{array} \right) + \left( \begin{array}{l} 0 \\ 0 \\ * \\ * \end{array} \right) + \left( \begin{array}{l} 0 \\ 0 \\ 0 \\ 1 \end{array} \right) = {\overline{F}}^{e_{1}} + {\overline{F}}^{e_{2}} + {\overline{F}}^{e_{3}} + \left( \begin{array}{l} 0 \\ 0 \\ 0 \\ 1 \end{array} \right).} \end{array}$$(1.61)

Vectors ${\overline{F}}^{e_{1}},\,{\overline{F}}^{e_{2}}$ and ${\overline{F}}^{e_{3}}$ are considered to be local to each element forcing vectors which can be found separately. Note that local vectors are sparse while the vector *F̃* is dense. By introducing new variables *x̂* for each finite element (see above), corresponding vector elements can be calculated as follows:

$$\begin{array}{l} {{\overline{F}}_{1}^{e_{1}} = \int\limits_{0}^{\frac{1}{3}}x( - 3x + 1)dx = \int\limits_{0}^{1}\frac{1}{3}\hat{x}(1 - \hat{x})d\hat{x} = \frac{1}{54}.} \end{array}$$(1.62)

$$\begin{array}{l} {{\overline{F}}_{2}^{e_{1}} = \int\limits_{0}^{\frac{1}{3}}3x^{2}dx = \int\limits_{0}^{1}\frac{1}{3}{\hat{x}}^{2}d\hat{x} = \frac{1}{27}.} \end{array}$$(1.63)

$$\begin{array}{l} {{\overline{F}}_{2}^{e_{2}} = \int\limits_{\frac{1}{3}}^{\frac{2}{3}}x( - 3x + 2)dx = {\int\limits_{0}^{1}{\frac{1}{9}(1 + \hat{x})(1 - \hat{x})d\hat{x}}} = \frac{2}{27}.} \end{array}$$(1.64)

$$\begin{array}{l} {{\overline{F}}_{3}^{e_{2}} = \int\limits_{\frac{1}{3}}^{\frac{2}{3}}x(3x - 1)dx = {\int\limits_{0}^{1}{\frac{1}{9}(1 + \hat{x})\hat{x}d\hat{x}}} = \frac{5}{54}.} \end{array}$$(1.65)

$$\begin{array}{l} {{\overline{F}}_{3}^{e_{3}} = \int\limits_{\frac{2}{3}}^{1}x( - 3x + 3)dx = \int\limits_{0}^{1}\frac{1}{9}(2 + \hat{x})(1 - \hat{x})d\hat{x} = \frac{7}{54}.} \end{array}$$(1.66)

$$\begin{array}{l} {{\overline{F}}_{4}^{e_{3}} = \int\limits_{\frac{2}{3}}^{1}x(3x - 2)dx = \int\limits_{0}^{1}\frac{1}{9}(2 + \hat{x})\hat{x}d\hat{x} = \frac{4}{27}.} \end{array}$$(1.67)

Assembling the final forcing vector gives

$$\begin{array}{l} {\widetilde{F} = \left( \begin{array}{l} \frac{1}{54} \\ \frac{1}{27} \\ 0 \\ 0 \end{array} \right) + \left( \begin{array}{l} 0 \\ \frac{2}{27} \\ \frac{5}{54} \\ 0 \end{array} \right) + \left( \begin{array}{l} 0 \\ 0 \\ \frac{7}{54} \\ \frac{4}{27} \end{array} \right) + \left( \begin{array}{l} 0 \\ 0 \\ 0 \\ 1 \end{array} \right) = \left( \begin{array}{l} \frac{1}{54} \\ \frac{1}{9} \\ \frac{2}{9} \\ \frac{31}{27} \end{array} \right).} \end{array}$$(1.68)

From (1.55) and (1.68), the equations can be written in the form

$$\begin{array}{l} {\left( \begin{array}{llll} \frac{28}{9} & {- \frac{53}{18}} & 0 & 0 \\ {- \frac{53}{18}} & \frac{56}{9} & {- \frac{53}{18}} & 0 \\ 0 & {- \frac{53}{18}} & \frac{56}{9} & {- \frac{53}{18}} \\ 0 & 0 & {- \frac{53}{18}} & \frac{28}{9} \end{array} \right)\left( \begin{array}{l} 1 \\ {u\left( \frac{1}{3} \right)} \\ {u\left( \frac{2}{3} \right)} \\ {u(1)} \end{array} \right) = \left( \begin{array}{l} \frac{1}{54} \\ \frac{1}{9} \\ \frac{2}{9} \\ \frac{31}{27} \end{array} \right),} \end{array}$$(1.69)

or

$$\begin{array}{cl} {\left( \begin{array}{l} \frac{28}{9} \\ {- \frac{53}{18}} \\ 0 \\ 0 \end{array} \right) + u\left( \frac{1}{3} \right)\left( \begin{array}{l} {- \frac{53}{18}} \\ \frac{56}{9} \\ {- \frac{53}{18}} \\ 0 \end{array} \right) + u\left( \frac{2}{3} \right)\left( \begin{array}{l} 0 \\ {- \frac{53}{18}} \\ \frac{56}{9} \\ {- \frac{53}{18}} \end{array} \right)} & \\ {+ u(1)\left( \begin{array}{l} 0 \\ 0 \\ {- \frac{53}{18}} \\ \frac{28}{9} \end{array} \right) = \left( \begin{array}{l} \frac{1}{54} \\ \frac{1}{9} \\ \frac{2}{9} \\ \frac{31}{27} \end{array} \right).} & \end{array}$$(1.70)

Note that BC specifies *u*(0) = 1 and there are only three unknowns left in the system (1.70). Then, moving first vector in (1.70) to the right hand side of the equation and removing first row in the entire system (see (1.25)) we come to the final linear system for the function values

$$\begin{array}{l} {\left( \begin{array}{lll} \frac{56}{9} & {- \frac{53}{18}} & 0 \\ {- \frac{53}{18}} & \frac{56}{9} & {- \frac{53}{18}} \\ 0 & {- \frac{53}{18}} & \frac{28}{9} \end{array} \right)\left( \begin{array}{l} {u\left( \frac{1}{3} \right)} \\ {u\left( \frac{2}{3} \right)} \\ {u(1)} \end{array} \right) = \left( \begin{array}{l} \frac{55}{18} \\ \frac{2}{9} \\ \frac{31}{27} \end{array} \right).} \end{array}$$(1.71)

Solving equations (1.71) gives

$$\begin{array}{l} {u\left( \frac{1}{3} \right) = 1.129,\quad u\left( \frac{2}{3} \right) = 1.345,\quad u(1) = 1.646.} \end{array}$$(1.72)

From the expression (1.27) the exact solutions at these points are 1.131, 1.351 and 1.648, respectively. It can be seen that FEM solution approximates the exact one quite well.

## 1.5 ALGORITHMS OF THE FINITE ELEMENT METHOD

Below, we are going to compose algorithms needed for programming implementation of the FEM using from top to bottom approach with increasing granularity of details. We start with an algorithm for composing system (1.25), then, assembling matrices is considered, and finally, explanation of how to calculate elements of these matrices is given. Each subsequent step in the hierarchy of algorithms increases granularity of the previous one by introducing more details.

### 1.5.1 Composing Linear System of the FEM

We have seen that solving BVP using FEM effectively comes down to solving the linear system (1.25) which, in turn, is defined by the matrix *Ã* and the vector **F̃**. It is straightforward to create a generic algorithm for composing FEM linear system (1.25).

![](images/comp01_1.jpg)

There are two points in this algorithm which have to be clarified, namely, how to assemble matrices and how to solve a linear system. Regarding a method of solving linear system, we will discuss it later that this is a sparse linear system which possess a unique, well-defined solution, which allows applying any standard linear solver. As to the method of assembling matrices, this is crucial feature in the context of the FEM, since this is a computationally expensive part which affects effectiveness of the entire FEM (especially when *N* is large). Next we focus on the assembling algorithm.

### 1.5.2 Assembling Global Matrices

Let us consider the stiffness matrix (1.22). It is seen from (1.22) that the matrix *Ã* is a square one and can be viewed as a sum of two matrices, namely *Ã* = *A* + *S*, where

$$\begin{array}{l} {\begin{array}{l} {A_{ij} = \int\limits_{s_{0}}^{s_{1}}\left( {c\varphi_{i}'\varphi_{j}' + b\varphi_{i}\varphi_{j}' + a\varphi_{i}\varphi_{j}} \right)dx,} \\ {S_{i,j} = \sigma\varphi_{i}(s_{1})\varphi_{j}(s_{1}),} \end{array}\quad i,j = 1,\ldots,N.} \end{array}$$(1.73)

Here, *N* = *n**m* + 1 and the matrix *S* is defined by the boundary conditions. Recall that the interval [*s*[0], *s*[1]] is split by *n* + 1 points into *n* finite elements each having *m* + 1 points so that $\lbrack s_{0},s_{1}\rbrack = {\underset{l = 1}{\overset{n}{\cup}}e_{l}}$. As such, the integral in (1.73) can be represented through the sum of local integrals over the finite elements *e*[*l*]

$$\begin{array}{l} {A_{ij} = {\sum\limits_{l = 1}^{n}\int\limits_{e_{l}}}\left( {c\varphi_{i}'\varphi_{j}' + b\varphi_{i}\varphi_{j}' + a\varphi_{i}\varphi_{j}} \right)dx.} \end{array}$$(1.74)

Now, let us consider more closely an integral over a local finite element *e*[*l*] and determine only those basis functions which are nonzero over the element *e*[*l*]. It is easy to see that *l*^(*t**h*) element spans the points *x*[*m*(*l* − 1) + 1], …, *x*[*m**l* + 1], or, by introducing a local numeration index *β* = 1, …, *m* + 1 and a global starting index notation *n*[*l*] = *m*(*l* − 1), we can write that *x*[*n*[*l*] + *β*] ∈ *e*[*l*]. As a result, *φ*[*n*[*l*] + *β*] are the basis functions associated with *e*[*l*] which are nonzero over this element. These nonzero values form a matrix $\left. {\overline{A}}^{l} \right.\sim\left( {(m + 1) \times (m + 1)} \right)$ with elements

$$\begin{array}{cl} {{\overline{A}}_{\alpha\beta}^{l} = \int\limits_{x_{n_{l} + 1}}^{x_{n_{l} + m + 1}}\left( {c\varphi_{n_{l} + \alpha}'\varphi_{n_{l} + \beta}' + b\varphi_{n_{l} + \alpha}\varphi_{n_{l} + \beta}' + a\varphi_{n_{l} + \alpha}\varphi_{n_{l} + \beta}} \right)} & {dx,} \\ {\alpha,\beta = 1,\ldots,m + 1.} & \end{array}$$(1.75)

Introducing a local stiffness matrix allows us in representing global stiffness matrix through a sum of local ones. By inspecting (1.74) we observe that *A*[*i**j*] has zero value if *φ*[*i*] and *φ*[*j*] are nonoverlapping functions (|*i* − *j*| > *m*), and nonzero value otherwise. Moreover, the sum (1.74) has single nonzero summand if *j* ≠ *j* (|*i* − *j*| < *m*) and two summands if *i* = *j*. As such, elements *A*[*i**j*] can be expressed as

$$\begin{array}{l} {A_{ij} = {\sum\limits_{l,\alpha,\beta:i = n_{l} + \alpha,j = n_{l} + \beta}{\overline{A}}_{\alpha\beta}^{l}}.} \end{array}$$

To incorporate all zero elements as well, let us extend a local stiffness matrix by introducing matrix *A*^(*l*) ∼ (*N* × *N*) which is a matrix with zero value elements except of a block corresponding to the finite element *e*[*l*] and defined by the local stiffness matrix (1.75)

$$\begin{array}{l} {A_{n_{l} + \alpha,n_{l} + \beta}^{l} = {\overline{A}}_{\alpha\beta}^{l},\quad\alpha,\beta = 1,\ldots,m + 1.} \end{array}$$(1.76)

Summarizing, we can see that the global stiffness matrix, *A*, can be obtained from summation of the extended local stiffness matrices, *A*^(*l*), which, in turn, are calculated through the local matrices (1.75).

$$\begin{array}{l} {A = {\sum\limits_{l = 1}^{n}A^{l}}.} \end{array}$$

Analogously, global forcing vector is a sum of two vectors, **F̃** = **F** + **M**, where (see (1.23))

$$\begin{array}{l} {F_{i} = \int\limits_{s_{0}}^{s_{1}}f\varphi_{i}dx,\quad M_{i} = \mu\varphi_{i}(s_{1}),\quad i = 1,\ldots,N.} \end{array}$$(1.77)

By introducing a local forcing vector, $\left. \mathbf{\overline{F}} \right.\sim\left( {(m + 1) \times 1} \right)$, through

$$\begin{array}{l} {{\overline{F}}_{\alpha}^{l} = \int\limits_{x_{n_{l} + 1}}^{x_{n_{l} + m + 1}}f\varphi_{n_{l} + \alpha}dx,\quad\alpha = 1,\ldots,m + 1,} \end{array}$$(1.78)

and extended local forcing vector, **F** ∼ (*N* × 1), as following

$$\begin{array}{l} {F_{n_{l} + \alpha}^{l} = {\overline{F}}_{\alpha}^{l},\quad\alpha = 1,\ldots,m + 1,} \end{array}$$(1.79)

we come to the expression

$$\begin{array}{l} {\mathbf{\mathbf{F}} = {\sum\limits_{l = 1}^{n}\mathbf{\mathbf{F}}^{l}}.} \end{array}$$

Note that the extended local forcing vector, **F**^(*l*), contains all zero elements except of values defined by the local forcing vector (1.79).

Matrix *S* and vector **M** result from the boundary conditions and they are specified at the single point *s*[1]. Since *φ*[*i*](*x*[*j*]) = *δ*[*i**j*] and *s*[1] = *x*[*N*], then each of *S* and **M** has the single nonzero value, namely, *S*[*N**N*] = *σ* and *M*[*N*] = *μ*.

As a result, we come to the algorithm for assembling stiffness matrix and forcing vector.

![](images/comp01_2.jpg)

Later, we create a programming code implementing this algorithm and discuss it in details. One problem which has not been illuminated so far is how to calculate elements of local matrices. Below, we turn our attention to this problem and deduce an algorithm for calculating these elements.

### 1.5.3 Calculating Elements of the Local Matrices

We start with a simpler case of calculating elements of the local forcing vector defined by the integral (1.78) for the *l*^(*t**h*) finite element. By inspecting expression (1.78) we observe that the integrand depends on the local basis functions *φ*[*n*[*l*] + *α*] having form of Lagrange polynomial

$$\begin{array}{l} {\varphi_{n_{l} + \alpha}(x) = {\prod\limits_{j = 1,j \neq \alpha}^{m + 1}\frac{x - x_{n_{l} + j}}{x_{n_{l} + \alpha} - x_{n_{l} + j}}},\quad x \in \lbrack x_{n_{l} + 1},x_{n_{l} + m + 1}\rbrack,} \end{array}$$(1.80)

which depends on the global index *n*[*l*]. We are aimed to transform expression (1.80) to the one which is independent on the global index so that to obtain invariant basis expression across all finite elements. To achieve this, let us introduce a local variable, *x̂*, and transformation as follows:

$$\begin{array}{ll} {\hat{x} = \frac{x - x_{n_{l} + 1}}{h_{l}},\quad x = x_{n_{l} + 1} + \hat{x}h_{l},} & \\ {dx = h_{l}d\hat{x},\quad h_{l} = x_{n_{l} + m + 1} - x_{n_{l} + 1}.} & \end{array}$$(1.81)

It can be seen the expression (1.81) specifies linear transformation so that *x*[*n*[*l*] + *j*] → *x̂*[*j*], or

$$\begin{array}{l} \left. x_{n_{l} + 1},\ldots,x_{n_{l} + m + 1}\rightarrow 0 = {\hat{x}}_{1},\ldots,{\hat{x}}_{m + 1} = 1, \right. \end{array}$$

and *e*[*l*] = [*x*[*n*[*l*] + 1], *x*[*n*[*l*] + *m* + 1]] → *ê* = [0, 1], ∀*n*[*l*]. As a result, any finite element is transformed into a canonical, or basis, element of the unity length. Moreover, substitution (1.81) into (1.80) gives

$$\begin{array}{l} {\varphi_{n_{l} + \alpha}(x) = \varphi_{n_{l} + \alpha}(x_{n_{l} + 1} + \hat{x}h_{l}) = {\prod\limits_{j = 1,j \neq \alpha}^{m + 1}\frac{\hat{x} - {\hat{x}}_{j}}{{\hat{x}}_{\alpha} - {\hat{x}}_{j}}} = {\hat{\varphi}}_{\alpha}(\hat{x}),} \end{array}$$(1.82)

where basis functions *φ̂*[*α*] are now expressed in terms of the local variable *x̂*. If we denote *f̂* = *f*(*x*[*n*[*l*] + 1] + *x̂**h*[*l*]), then integral (1.78) can be rewritten as

$$\begin{array}{l} {{\overline{F}}_{\alpha}^{l} = h_{l}\int\limits_{0}^{1}\hat{f}{\hat{\varphi}}_{\alpha}d\hat{x},\quad\alpha = 1,\ldots,m + 1.} \end{array}$$(1.83)

Integral (1.83) can be evaluated exactly in a limited number of cases (linear *φ̂*[*α*] or *f̂* = *c**o**n**s**t*), and, generally speaking, we have to apply a numerical approximation technique to calculate (1.83). We utilize a quadrature rule[⁶](#chapter1.xhtml_fn1_6) which gives

$$\begin{array}{l} {{\overline{F}}_{\alpha}^{l} \approx h_{l}{\sum\limits_{k = 1}^{q}{{\hat{\gamma}}_{k}\hat{f}({\hat{d}}_{k}){\hat{\varphi}}_{\alpha}({\hat{d}}_{k})}},\quad 0 \leq {\hat{d}}_{k} \leq 1,\quad\alpha = 1,\ldots,m + 1,} \end{array}$$(1.84)

where *q* is a number of quadrature nodes, *γ̂*[*k*] and *d̂*[*k*] are quadrature weights and nodes, respectively. Currently, we do not look at the construction of a particular rule leaving this task for the next section. The main result is that we have defined a numerical method allowing calculation of the local forcing vector through the formula (1.84).

In a similar way, computation of the local stiffness matrix can be reduced to the numerical calculations through the approximate quadrature rule. By using transformation (1.81) and introducing functions *â*, *b̂* and *ĉ*, integral (1.75) reduces to

$$\begin{array}{l} {{\overline{A}}_{\alpha\beta}^{l} = \int\limits_{0}^{1}(h_{l}^{- 1}\hat{c}{\hat{\varphi}}_{\alpha}'{\hat{\varphi}}_{\beta}' + \hat{b}{\hat{\varphi}}_{\alpha}{\hat{\varphi}}_{\beta}' + h_{l}\hat{a}{\hat{\varphi}}_{\alpha}{\hat{\varphi}}_{\beta})d\hat{x},\quad\alpha,\beta = 1,\ldots,m + 1.} \end{array}$$

Here, we use the fact that *φ*(*x*)^′ = *φ̂*(*x̂*)^′/*h*[*l*]. Thereby,

$$\begin{array}{cl} {{\overline{A}}_{\alpha\beta}^{l} \approx {\sum\limits_{k = 1}^{q}{\hat{\gamma}}_{k}}(h_{l}^{- 1}\hat{c}{\hat{\varphi}}_{\alpha}'{\hat{\varphi}}_{\beta}' + \hat{b}{\hat{\varphi}}_{\alpha}{\hat{\varphi}}_{\beta}' + h_{l}\hat{a}{\hat{\varphi}}_{\alpha}{\hat{\varphi}}_{\beta})} & {({\hat{d}}_{k}),} \\ {\alpha,\beta =} & {1,\ldots,m + 1.} \end{array}$$(1.85)

Expressions (1.84) and (1.85) define approximate numerical calculations of the local matrices. Intuitively, it is clear that the higher precision of quadrature approximation, the higher accuracy of the FEM. Below, we imply that integral calculations are performed approximately and the symbol ‘≈’ is substituted by ‘=’ to avoid complicated notations.

Let us rewrite expressions (1.84) and (1.85) in matrix forms. To achieve this, we introduce complementary matrices *Ê*[*k**α*] = *φ̂*[*α*](*d̂*[*k*]) and *D̂*[*k**α*] = *φ̂*[*α*]^′(*d̂*[*k*]) having dimension *q* × (*m* + 1). With the help of these matrices, formula (1.84) for the local forcing vector takes the matrix form

$$\begin{array}{l} {\mathbf{\overline{F}}^{l} = {\hat{E}}^{T}\mathbf{\hat{F}}^{l},\quad\mathbf{\hat{F}}^{l} = h_{l}\left( {{\hat{\gamma}}_{1}\hat{f}({\hat{d}}_{1}),\ldots,{\hat{\gamma}}_{q}\hat{f}({\hat{d}}_{q})} \right)^{T}.} \end{array}$$(1.86)

One interesting observation following from (1.86) is that in case of *h*[*l*] = *c**o**n**s**t* ∀*l*, and when distribution of quadrature nodes, *d̂*[*k*], remains the same across all finite elements, then the local forcing vector is calculated only once (all local vectors are equal to each other).

Now, it is easy to represent calculations of the local stiffness matrix (1.85) in the form of matrix expression

$$\begin{array}{l} {{\overline{A}}^{l} = {\hat{D}}^{T}{\hat{C}}^{l}\hat{D} + {\hat{E}}^{T}{\hat{B}}^{l}\hat{D} + {\hat{E}}^{T}{\hat{A}}^{l}\hat{E},} \end{array}$$

where

$$\begin{array}{ll} {\hat{A}}^{l} & {= h_{l}\text{~diag~}\left( {{\hat{\gamma}}_{1}\hat{a}({\hat{d}}_{1}),\ldots,{\hat{\gamma}}_{q}\hat{a}({\hat{d}}_{q})} \right),} \\ {\hat{B}}^{l} & {= \text{~diag~}\left( {{\hat{\gamma}}_{1}\hat{b}({\hat{d}}_{1}),\ldots,{\hat{\gamma}}_{q}\hat{b}({\hat{d}}_{q})} \right),} \\ {\hat{C}}^{l} & {= h_{l}^{- 1}\text{~diag~}\left( {{\hat{\gamma}}_{1}\hat{c}({\hat{d}}_{1}),\ldots,{\hat{\gamma}}_{q}\hat{c}({\hat{d}}_{q})} \right).} \end{array}$$

Generally speaking, matrices *Ê* and *D̂* can be associated with interpolating matrix and differentiating matrix, respectively. Indeed, for the function *u*[*h*](*x*) we have local representation for *x* ∈ *e*[*l*] (see(1.20))

$$\begin{array}{l} {u_{h}(x) = {\sum\limits_{\alpha = 1}^{m + 1}{\varphi_{n_{l} + \alpha}(x)u_{n_{l} + \alpha}}} = {\sum\limits_{\alpha = 1}^{m + 1}{{\hat{\varphi}}_{\alpha}(\hat{x})u_{n_{l} + \alpha}}} = \mathbf{\hat{\varphi}}{(\hat{x})}^{T}\mathbf{\mathbf{u}}^{l},} \\ {\mathbf{\mathbf{u}}^{l} = \left\{ u_{n_{l} + \alpha} \right\}_{\alpha = 1}^{m + 1},\quad x \in e_{l}.} \end{array}$$

For any given point *x* = *d*[*k*] ∈ *e*[*l*] (for example, *d*[*k*] is a quadrature node), we obtain that *u*[*h*](*d*[*k*]) = **φ̂**(*d̂*[*k*])^(*T*)**u**^(*l*), where **φ̂**(*d̂*[*k*])^(*T*) is the *k*^(*t**h*) row of the matrix *Ê*. Consequently, **u**[*h*](**d**) = *Ê***u**[*l*], where **d** and **u**[*h*] are the vectors of points and function values to be interpolated. As such, matrix *Ê* can be viewed as interpolating matrix. By performing similar reasoning we observe, that **u**[*h*]^′(**d**) = *h*[*l*]^(−1)*D̂***u**[*l*], and the matrix *D̂* can be associated with differentiating operation. These matrices can be used not only for calculation of stiffness matrix, but when plotting functions*u*[*h*] and *u*[*h*]^′.

![](images/comp01_3.jpg)

Summarizing, we come to the algorithm for calculating elements of the local stiffness matrix and forcing vector corresponding to the *l*^(*t**h*) finite element.

As we can see, this is the very stage where basis functions come into play, and this algorithm depends on the choice of particular quadrature rule. It is worth noting that if the final elements are of the same length having the same quadrature and interpolation node distribution, then matrices *Ê* and *D̂* have to be calculated only once.

Quadrature nodes and weights distribution have to meet certain criteria to be suitable for numerical integration with appropriate accuracy. Below, we discuss some strategies of choosing nodes distribution.

## 1.6 QUADRATURE RULES

As we have seen, calculating elements of FEM matrices includes numerical integration which can be done through applying some quadrature rule.

$$\begin{array}{l} {\int\limits_{0}^{1}\hat{f}d\hat{x} \approx {\sum\limits_{k = 1}^{q}{{\hat{\gamma}}_{k}\hat{f}({\hat{d}}_{k})}}.} \end{array}$$

Choosing particular values of number *q*, node values, *d̂*[*k*], and weights, *γ̂*[*k*], results in different quadrature rules. Below, we utilize two types of quadrature, namely, Gaussian quadrature and Lobatto quadrature rule. [Appendix C](#appC.xhtml_appC) gives some theoretical background for these rules where basic explanations and examples are given. In addition, theory on calculations of weights and nodes using orthogonal polynomials is given in [Appendix D](#appD.xhtml_appD). Below, we use expressions without detailed explanations which can be found in the given appendices.

First, we consider Gaussian quadrature for integrals over the interval [−1, 1] which is the most common and well-studied domain of integration. Integration over the interval *[*0,1*]* can be obtained from the integration over the interval [−1, 1] through the transformation *x̂* = 1/2 + *x̃*/2, *x̃* ∈ [−1, 1]

$$\begin{matrix} {\int\limits_{0}^{1}\hat{f}d\hat{x} = \frac{1}{2}\int\limits_{- 1}^{1}\widetilde{f}d\widetilde{x} \approx \frac{1}{2}{\sum\limits_{k = 1}^{q}{{\widetilde{\gamma}}_{k}\widetilde{f}({\widetilde{d}}_{k})}} = {\sum\limits_{i = 1}^{q}{{\hat{\gamma}}_{k}\hat{f}({\hat{d}}_{k})}},} \\ {{\hat{\gamma}}_{k} = \frac{1}{2}{\widetilde{\gamma}}_{k},\quad{\hat{d}}_{k} = \frac{1}{2} + \frac{{\widetilde{d}}_{k}}{2}.} \end{matrix}$$

It is worth mentioning that Gaussian quadrature is a type of quadrature formula, which has the highest order of precision with the given number of nodes, *q*, which is equal to 2*q* − 1. Nodes, *d̃*[*k*], are the roots of Legendre polynomials, *L*[*q*](*x̃*), of order *q*. In general, nodes and weights can be calculated using eigenvalue decomposition of the following square matrix

$$\begin{array}{l} {Q = \left( \begin{array}{lllll} 0 & \beta_{1} & & & \\ & & & & \\ \beta_{1} & 0 & \beta_{2} & & \\ & & & & \\ & \ddots & \ddots & \ddots & \\ \, & & \beta_{q - 2} & 0 & \beta_{q - 1} \\ & & & \beta_{q - 1} & 0 \end{array} \right),\quad\begin{array}{l} {\beta_{j} = \frac{j}{\sqrt{4j^{2} - 1}},} \\ {\,\,\, j = 1,\ldots,q - 1.} \end{array}} \end{array}$$(1.87)

If *Q* = *U**Λ**U*^(−1), where *Λ* =  diag (*λ*[1], …, *λ*[*q*]) is a diagonal matrix of ordered eigenvalues and *U* is a matrix of corresponding eigenvectors, then Gaussian quadrature nodes are *d̃*[*k*] = *λ*[*k*] and the weights are *γ̃*[*k*] = 2*U*[1*k*]².

One important observation about Gaussian quadrature is that there is no guarantee that the set of nodes contains boundary points, −1 or 1\. In order to include the end points of the integration, Lobatto quadrature can be used

$$\begin{array}{l} {\int\limits_{- 1}^{1}\widetilde{f}d\widetilde{x} \approx {\widetilde{\gamma}}_{1}\widetilde{f}( - 1) + {\sum\limits_{k = 2}^{q - 1}{{\widetilde{\gamma}}_{k}\widetilde{f}({\widetilde{d}}_{k})}} + {\widetilde{\gamma}}_{q}\widetilde{f}( - 1).} \end{array}$$

This type of quadrature has the precision of order 2*q* − 3 where quadrature nodes are roots of the polynomial (1 − *x̃*²)*L*[*q* − 1]^′(*x̃*). Value of nodes and weights can be found through the eigenvalue decomposition *Q* = *U**Λ**U*^(−1) of the matrix

$$\begin{array}{l} {Q = \left( \begin{array}{lllll} 0 & \beta_{1} & & & \\ & & & & \\ \beta_{1} & 0 & \beta_{2} & & \\ & & & & \\ & \ddots & \ddots & \ddots & \\ \, & & \beta_{q - 2} & 0 & \beta_{q - 3} \\ & & & \beta_{q - 3} & 0 \end{array} \right),\quad\begin{array}{l} {\beta_{j} = \sqrt{\frac{j(j + 2)}{(2j + 1)(2j + 3)}},} \\ {\,\,\, j = 1,\ldots,q - 3.} \end{array}} \end{array}$$

Nodes of Lobatto quadrature are **d̃** = {−1, *λ*[*i*], 1} and weights to be

$$\begin{array}{l} {\mathbf{\widetilde{\gamma}} = \left\{ {\frac{2}{q^{2} - q},\frac{4U_{1i}^{2}}{3(1 - \lambda_{i})},\frac{2}{q^{2} - q}} \right\},\, i = 1,\ldots,q - 2,} \end{array}$$

where *λ*[*i*] and *U*[*i*] are the eigenvalues of matrix *Q*. Lobatto quadrature nodes can be chosen to be interpolation nodes on the basis element. In this case, *q* = *m* + 1 and *x̂*[*α*] = *d̂*[*α*] = (1 + *d̃*[*α*])/2.

## 1.7 DEFINING PARAMETERS OF THE FEM

From the previous sections we have learned that there are three parameters defining particular FEM scheme: the number of finite elements, *n*, the degree of approximating polynomial, *m*, and the number of quadrature nodes on the basis element, *q*. To build an efficient FEM implementation, it is worth analysing influence of these parameters since they affect property of stiffness matrices and accuracy of the FEM. Below we discuss various points which need to be taken into account when creating particular FEM scheme.

**Structure of the stiffness matrix**. Numbers *n* and *m* determine uniquely the structure of the global stiffness matrix, *A*, in terms of distribution of the non-zero entries. If *n* ≫ *m*, then the matrix *A* is the sparse one containing large number of zeroth elements. Contrarily, when *n* is small but *m* is large, then the matrix *A* is considered to be dense (see [figure 1.7](#chapter1.xhtml_fig1_7)).

![Two parts image illustrating how a matrix is filled with elements. Matrix is shown as a square with grid, non-zero elements are marked with dots and zeroth elements are unmarked. Part (a) shows matrix with many small diagonal blocks. Part (b) shows a matrix with only two large diagonal blocks.](images/fig1_7.jpg)

[Figure 1.7:](#chapter1.xhtml_b1fig1_7) Examples of non-zero entries distribution for the global stiffness matrix: (a) *n* = 5, *m* = 4. Matrix has 121 non-zero elements; (b) *n* = 2, *m* = 10. Matrix has 241 non-zero elements.

The total number of non-zeroth elements is equal to *n*(*m* + 1)² − (*n* − 1), and this number estimates computer memory consumption and computational costs to solve linear system. It is seen that costs increase linearly with *n* but have quadratic growth with *m*.

**Accuracy of the solution and choice of parameters *n* and *m***. Numbers *n* and *m* influence accuracy of the approximate solution *u*[*h*]. Let us briefly illustrate this influence. Assuming that numerical integration is not used (all integrals are calculated exactly), it is stated in the FEM theory that

$$\begin{array}{l} {\| u - u_{h}\|_{H^{1}} \leq C\frac{h^{k - 1}}{m^{k - 1}}\| u\|_{H^{k}},\quad\| u\|_{H^{k}}^{2} = \int\limits_{s_{0}}^{s_{1}}\left( {u^{2} + \left| \frac{d^{k}u}{dx^{k}} \right|^{2}} \right)dx.} \end{array}$$

Here *C* is a constant, *u* is the exact solution, 2 ≤ *k* ≤ min {*m* + 1, *r*} where number *r* is defined from the criteria ∥*u*∥[*H*^(*r*)] < ∞. In connection to this, two cases are of interest to us, namely, (a) solution is not sufficiently smooth function, and *r* < (*m* + 1); (b) solution is quite smooth function, and *r* ≫ (*m* + 1). By choosing highest value for *k*, we obtain estimations

$$\begin{array}{l} {\text{(a)}\,\| u - u_{h}\|_{H^{1}} = O\left( \frac{h^{r - 1}}{m^{r - 1}} \right),\quad\text{(b)}\,\| u - u_{h}\|_{H^{1}} = O\left( \frac{h^{m}}{m^{m}} \right).} \end{array}$$

We can see that parameter *m* affects the solution accuracy differently. To clarify this, let us consider a simplified example when all elements are of the same length, *h* = (*s*[1] − *s*[0])/*n*. In this case, *h* = *O*(*n*^(−1)) and we come to the estimations

$$\begin{array}{l} {\text{(a)}\,\| u - u_{h}\|_{H^{1}} = O\left( \frac{1}{{(nm)}^{r - 1}} \right),\quad\text{~(b)}\,\| u - u_{h}\|_{H^{1}} = O\left( \frac{1}{{(nm)}^{m}} \right).} \end{array}$$(1.88)

Consequently, case (a) corresponds to the power growth of accuracy with respect to both parameters, *n* and *m*, unlike the case (b) where only increase of *n* leads to power growth of accuracy while increasing *m* results in exponential growth.

Thereby, it could be recommended three strategies of how to choose parameters *m* and *n*:

1.  Having chosen small *m* (practically, 1 ≤ *m* ≤ 5), the desired accuracy is reached by increasing *n* (decreasing *h*).

2.  Having chosen small *n* (it is allowed to take *n* = 1 which corresponds to the single finite element), the desired accuracy is reached by increasing *m* (practically, *m* = 5, …, 50, …).

3.  Polynomial degree, *m*, is not fixed for all elements and can vary. This strategy is useful when solution behaves differently on the interval [*s*[0], *s*[1]]. If there is a region with rapidly increasing derivative of the solution, then within this region the value of *m* is chosen to be fixed and small, but elements are refined (*n* increases). The value of *n* in the rest of interval is fixed but the polynomial degree increases.

It is worth noting that the Euclidean condition number of the stiffness matrix, *A*, is of order *O*(*h*^(−2)), so refining finite elements is sensible to some extent. Extremely small elements leads to solving ill-conditioned linear system.

In addition, following circumstance has to be taken into account when choosing elements distribution. In practise, differential equation coefficients could be functions having singularities (discontinuities of a function or its derivative) at particular points. In this case, it is advisable to take these points to be boundary nodes of finite elements, that is *x*[*n*[*l*]]. As a result, all functions would be smooth within each finite element and this suffices to obtain desired accuracy of the FEM; otherwise, accuracy decreases significantly.

**Accuracy of the solution and distribution of points within finite elements**. Vector of points within a basis element (0 = *x̂*[1], …, *x̂*[*m* + 1] = 1) defines distribution of nodes for each finite element. Theoretically (in the exact computer arithmetic), solution *u*[*h*] does not depend on the way of choosing distribution of these points. Practically (in floating point computation), this distribution plays an important role, particularly, it affects conditional number of the stiffness matrix. When the value of *m* is small (*m* < 7), nodes *x̂*[*i*] can be evenly spaced with a constant step. However, when the value of *m* is relatively large, it is recommended to choose nodes *x̂*[*i*] so that they are roots of some orthogonal polynomial of the order *m* + 1. For instance, a good choice would be Chebyshev polynomials or Legendre polynomials.

**Quadrature rule and choice of quadrature nodes distribution**. Theory states (and results of FEM practical calculation confirm) that the following conditions should be satisfied for a quadrature rule:

*   quadrature weights are positive, *γ* > 0,

*   number of nodes *q* ≥ *m*,

*   a quadrature has to be exact for polynomials of degree 2*m* − 1 and higher[⁷](#chapter1.xhtml_fn1_7)

Practically, there are two quadrature rules meeting these criteria, namely, Gaussian quadrature having number of nodes *q* ≥ *m*, and Lobatto quadrature with *q* ≥ (*m* + 1). There is a possibility to obtain quadrature nodes, *d̂*[*i*], which coincide with interpolation nodes on the basis elements, *x̂*[*i*], and *q* = *m* + 1. In this case, Lobatto quadrature rule is used for numerical integration since the nodes of this rule include endpoints of the basis element and, in addition, the nodes are roots of orthogonal Legendre polynomial which, in turn, can be taken as nodes of interpolating polynomials on the basis element.

# Chapter 2 Programming One-Dimensional Finite Element Method for the Linear Boundary Value Problem

DOI: [10.1201/9781003265979-2](https://doi.org/10.1201/9781003265979-2)

IN this chapter, we are going to compose MATLAB^® codes for finding numerical solution to the BVP using FEM described in the previous chapter. In addition, algorithm implementation for calculating solution first derivative and solution error will be considered.

Before we start coding FEM algorithm, let us outline the strategy of how it is going to be done. Programming implementation will have a form of library with set of functions with code for particular numerical method or piece of algorithm. We are aimed to group steps of the FEM algorithms into functions according to their logic. For example, from generic high-level FEM [algorithm 1](#chapter2.xhtml_comp02_1) follows that it is convenient to have at least four stand-alone functions for each step of the algorithm, and probably some complementary helper functions as well. The approach we consider below is bottom to top which is opposed to top to bottom consideration in [chapter 1](#chapter1.xhtml). We will start with programming quadrature rules and splitting interval into finite elements; then we will look into coding assembling stiffness matrices and BC. As a last step, the high-level main function will be considered which implements logic of [algorithm 1](#chapter2.xhtml_comp02_1).

The main data structure used in the code implementation is a matrix, so it is assumed that a reader is familiar with basic skills of matrix manipulation commands in MATLAB and Python. There is, however, a special case of matrices which we will discuss in detail, namely, sparse matrices. As we have seen from [chapter 1](#chapter1.xhtml), FEM results in matrices with sparse structure which we need to reflect in coding.

## 2.1 SPARSE MATRICES IN MATLAB^®

The basic structure to be utilized in the implementation of FEM algorithm is a sparse matrix. The main feature of sparse matrices is the compact data representation when zeroth elements are ignored and not kept in memory. Operations with sparse matrix in MATLAB are similar to operations with full (dense) matrix. The difference is that sparse matrix should be created with specification sparse(). There are three methods to create a sparse matrix in MATLAB.

1.  Creating a sparse matrix from the full one. In this case the argument of the function sparse() is a dense matrix and returning value is a sparse matrix with the shape and values of the dense one. For example,

    ![](images/comp02_1.jpg)

    The sparse matrix is represented in the form of indices of nonzero elements and corresponding values. As a result we see arrays of indices (i,j) and values.

2.  Creating a sparse matrix by elements. The previous matrix can be specified as follows

    ![](images/comp02_2.jpg)

    Here, we specify matrix dimensions as arguments of the function sparse() followed by assigning values of matrix elements.

3.  Creating a sparse matrix from the arrays of indices and values. For example, the next code creates the matrix A from previous examples.

    ![](images/comp02_3.jpg)

    In general case, values in vectors of indices could repeat and in this case the corresponding values are summed up. This allows formation of the matrix A by accumulating its elements. For example, the matrix A can be specified as

    ![](images/comp02_4.jpg)

    Here A(1,1)=0.3+0.7. It is worth noting that (i,j) could be specified as two-dimensional matrices. In this case, function sparse() treats them as column vectors. In addition, the value v could be a scalar and it would be automatically extended to the vector of the corresponding length with all elements of v.

The third method is preferable for creating large sparse matrices since it is more generic and it reflects the way in which matrices are represented in MATLAB internally.

## 2.2 INPUT DATA STRUCTURES

Let us define input data structure to be used in MATLAB implementation. Particular BVP problem is defined by:

1.  numbers *s*[0] and *s*[1] specifying boundary;

2.  functions *c*(*x*), *b*(*x*), *a*(*x*) and *f*(*x*) specifying BVP coefficients;

3.  type of boundary conditions at the points *s*[0] and *s*[1].

There is nothing special about item (1) while representation of (2) and (3) in terms of MATLAB structures needs to be clarified. Functions in MATLAB can be defined either through anonymous inline declaration

f = @(x) sin(x)

or using stand-along .m file containing function definition

![](images/comp02_5.jpg)

Whenever it is possible, we strive to use vectorized computations which are much more efficient in terms of computational costs. Having a vector

x = [x1,…,xn],

function call y = f(x) returns a vector

y = [f(x1),…,f(xn)]

and we operate with variables being vectors rather than with individual components.

Considering item (3), we can use matrix to specify boundary conditions. Let us introduce a matrix bc having dimension 2 × 3 which packs all boundary condition data. First row corresponds to BC at the point s0 and the second row contains data for the boundary point s1. First column indicates type of BC while second and third columns contain corresponding data values. For example, bc(1,:)=[1,0,u_s0] is for the BC of the first type at the point s0 and bc(2,:)=[3,sigma,mu] is for the BC of the third type at the point s1.

Below, MATLAB codes for algorithm implementation will be given in reverse order with regards to above considered BEM algorithmic steps, namely, we start with coding quadrature rules and finish with solving linear system of the BEM. All implementations will be based on derived expressions.

## 2.3 CODING QUADRATURE RULES

Nodes and weights of Gaussian quadrature on arbitrary interval [s1,s2] can be calculated using [listing 2.1](#chapter2.xhtml_list2_1). Function GaussQuad() inputs the number of points, n, left boundary of the interval, s0, right boundary, s1, and returns a pair of vectors, d and w, which are quadrature nodes and weights accordingly. Here, quadrature nodes are zeroes of Legendre polynomial. The function can take either three or one argument and in case of a single argument, it is assumed the nodes are sought on the interval [-1,1]. This logic is implemented in lines 2–4 with MATLAB function **nargin** which returns the number of function input arguments given in the call to the currently executing function. The code lines 8–10 compute the elements of matrix Q (see (1.87)) and compose the matrix using diagonal assembling. Function **diag**(bta,k) places the elements of vector bta on the k-th diagonal (k=0 represents the main diagonal, k=1 is above the main diagonal, and k=-1 is below the main diagonal). Then, we perform eigen value decomposition (line 11) and extract sorted eigen values (line 12). To perform eigen values extraction, first, we use MATLAB function **diag**() which being called with matrix L returns its main diagonal, then we call the function **sort**() which returns sorted nodes, d, and it also returns an index vector, k, that describes the rearrangement of elements such that d = L(k,:). We need this index vector to keep correspondence between sorted eigen values and unsorted eigen vectors, U. The last step is to calculate weights on the interval [-1,1] (line 13) and to perform transformation for extended region [s0,s1] (lines 14–15). Note that all calculations here are vectorized, namely, we do not use loops to iterate over vector or matrix elements, but rather use vectors itself in calculation formulas. This significantly improves performance and simplifies code readability.

![](images/comp02_6.jpg)

Similarly, Lobatto quadrature implementation can be coded as shown in [listing 2.2](#chapter2.xhtml_list2_2). We need to make sure that input number of nodes is equal or greater than two to make calculation possible (lines 2–5). Compared with Gaussian quadrature rule, matrix elements are calculated differently (line 14) and boundary points are added to the nodes and weights (lines 19–20). Recall that the nodes of Lobatto quadrature can be taken to be interpolation nodes on the interval [s0,s1].

![](images/comp02_7.jpg)

## 2.4 IMPLEMENTATION CODE FOR INTERPOLATING AND DIFFERENTIATING MATRICES

Interpolating and differentiating matrices (*Ê* and *D̂*) are used for calculation of the function *u*[*h*] and its derivative at arbitrary points. These matrices are defined by basis functions for calculation of which we utilize expressions (1.13) and (1.14)

$$\begin{array}{ll} \beta_{\alpha} & {= \left( {\prod\limits_{j = 1,j \neq \alpha}^{m + 1}{({\hat{x}}_{\alpha} - {\hat{x}}_{j})}} \right)^{- 1},} \end{array}$$(2.1)

$$\begin{array}{ll} {\hat{E}}_{k,\alpha} & {= {\hat{\varphi}}_{\alpha}({\hat{d}}_{k}) = \beta_{\alpha}{\prod\limits_{j = 1,j \neq \alpha}^{m + 1}{({\hat{d}}_{k} - {\hat{x}}_{j})}},} \end{array}$$(2.2)

$$\begin{array}{ll} {\hat{D}}_{k,\alpha} & {= {\hat{\varphi}}_{\alpha}'({\hat{d}}_{k}) = \beta_{\alpha}{\sum\limits_{l = 1,l \neq \alpha}^{m + 1}{\prod\limits_{j = 1,j \neq \alpha,j \neq l}^{m + 1}{({\hat{d}}_{k} - {\hat{x}}_{j})}}}.} \end{array}$$(2.3)

The code in [listing 2.3](#chapter2.xhtml_list2_3) implements calculation of *Ê* and *D̂* defined on the basis element. Function interpolatingMat() returns interpolation matrix, E, and differentiation matrix, D, with input arguments to be interpolation points, x, and arbitrary nodes at which interpolation is calculated, d. Since the formulas for matrix elements are nonlinear we cannot fully apply vectorized calculations and have to use loops to iterate over elements. First, elements *β*[*α*] are calculated in the loop lines 4–7 where the variable b is used to store the values of *β*[*α*]. Vector j forms indices which span the range of product operator in (2.1) and function prod() returns the product of the vector elements. Listing lines 8–21 implement matrices E and D calculations with two nested loops for matrix elements k and i to calculate the product and one more loop to calculate the sum in (2.3). The indices are processed consistently in ascending order, so lines 14–15 perform this logic for product and summation calculation. Indices formation in the lines 5, 9 and 15 follows the same pattern with skipping i-th element.

![](images/comp02_8.jpg)

In addition to the function interpolatingMat(), it is useful to have a functionality which allows performing mesh refinement and calculating function values along with its derivatives on the refined mesh. This is helpful, for example, when plotting solution. [Listing 2.4](#chapter2.xhtml_list2_4) illustrates the code for generating corresponding refined mesh values. It makes use previous function interpolatingMat() to obtain matrices E and D and new mesh is generated by splitting each element into k subelements. Function getRefinedValues() has following arguments: u is a vector of function values on the coarse mesh, xl is a vector of finite element nodes, d is a vector of points on the basis element [0,1] and k is a number of refined mesh points on each finite element. Returning vectors are refined mesh points, x, new function values, y, and new function derivative values on refined mesh, dy. New points are generated using MATLAB command linspace(x1,x2,k) which generates k evenly distributed points in the interval [x1,x2] (see lines 2 and 12). For better readability, [listing 2.4](#chapter2.xhtml_list2_4) is complemented with comments.

![](images/comp02_9.jpg)

So far, we have created flexible computational tools for manipulation with mesh and quadrature points which lays a foundation for the next step to implement numerical integration.

## EXERCISE

*   ▶ Verify that the number of operations to calculate E and D using function interpolatingMat() has the order of *O*(nx²nd) and *O*(nx³nd), respectively.

*   ▶ Perform a number of running function interpolatingMat() with different value of dimension nx when x=d and estimate running time. Define dependence of calculation time on value nx.

*   ▶ Show that when x=d then the matrix D can be calculated through

    $$\begin{array}{l} {{\hat{D}}_{ij} = \frac{\beta_{j}}{\beta_{i}({\hat{x}}_{i} - {\hat{x}}_{j})},\quad i \neq j,\quad{\hat{D}}_{ij} = - {\sum\limits_{j = 1,j \neq i}^{n}{\hat{D}}_{ij}}.} \end{array}$$

    Usage of these expressions results in complexity of calculation matrix D to be *O*(nx²) rather than *O*(nx⁴) compared to the implementation function interpolatingMat().

*   ▶ Compose your own version of function interpolatingMat().

## 2.5 IMPLEMENTATION CODE FOR CALCULATING AND ASSEMBLING FEM MATRICES

As discussed above, composing of the global stiffness matrix, *Ã*, and global forcing vector, **F̃**, can be decomposed into two parts (see 1.73 and 1.77): assembling matrix *A* and vector **F** which do not take into account boundary condition and assembling matrix *S* and vector **M** which account for boundary conditions. Function assemblingAF() in [linsting 2.5](#chapter2.xhtml_list2_5) implements the first part where we compute *A* and **F**.

Generally speaking, the function assemblingAF() returns stiffness matrix A and forcing vector F corresponding to the equation −(*c**u*^′)^′ + *b**u*^′ + *a**u* = *f* with homogeneous Neumann boundary conditions *c**u*^′ = 0. Arguments have the following meaning: c,b,a,f are equation coefficients, xl is a vector of finite elements nodes, x is a vector of interpolation points on the basis element, d is a vector of quadrature nodes on the basis element and w is a vector of quadrature weights on the basis element. The code fully implements [algorithm 3](#chapter2.xhtml_comp02_3) for calculating elements of local matrices and then it incorporates assembling global matrices without taking into account boundary conditions (first two steps of [algorithm 2](#chapter2.xhtml_comp02_2)). Code line 5 corresponds to the first step of [algorithm 2](#chapter2.xhtml_comp02_2) and lines 6–17 implement second step with looping over finite elements, computing local matrices (lines 7–14) and accumulating components of global matrices (lines 15–16).

![](images/comp02_10.jpg)

It is worth stressing attention on the line A(ne,ne)=A(ne,ne)+Al. Here, A is n_total by n_total global stiffness matrix, Al is (m+1) by (m+1) local stiffness matrix and the structure ne contains global indices of points on each element. As such, local element is added to the corresponding component of the global matrix which represents assembling the global matrix. This assembling strategy is not fully vectorized but it is good for matrix of moderate number of components. Later, in [section 5.1](#chapter5.xhtml_sec5_1), we consider other approaches to assemble matrices which are efficient for large matrices and allow full vectorization.

Next, we need to take into account BC and calculate matrix *S* and vector **M** which are being added to *A* and **F**, respectively, to form full FEM matrices. Incorporating BC is performed according to the step three of [algorithm 1](#chapter2.xhtml_comp02_1) for BC of the first type (Dirichlet BC), and according to the step three of [algorithm 2](#chapter2.xhtml_comp02_2) for BC of the third type (Robin BC). Recall that BC of the second type (Neumann BC) can be considered as a special case of Robin BC. Code [listing 2.6](#chapter2.xhtml_list2_6) implements logic for including BC where function assemblingBC() inputs boundary condition matrix, bc, stiffness matrix, A, forcing vector, F, and outputs stiffness matrix and forcing vector complemented with BC, [A0,F0]. As discussed in [section 2.2](#chapter2.xhtml_sec2_2), first column of matrix bc encodes type of BC, so lines 6–13 correspond to BC of the third type either for point s0 (lines 6–9) or point s1 (lines 10–13). Then, BC of the first type is considered (lines 15–22). In both cases, the stiffness matrix and forcing vector are modified in some way to include BC. The last step is to form final matrices from the modified one (lines 23–25).

![](images/comp02_11.jpg)

Once the final stiffness matrix, A0, and forcing vector, F0, are created using function assemblingBC(), resulting FEM system can be solved and solution can be composed according to the steps 4 and 5 of [algorithm 1](#chapter2.xhtml_comp02_1). Function solveFEM() in [listing 2.7](#chapter2.xhtml_list2_7) returns the final solution, u. The code lines 12–13 call linear solver (backslash MATLAB operator) and append Dirichlet BC if any (u_s0 and u_s1).

![](images/comp02_12.jpg)

It is convenient to combine previous three functions into the single one which performs solution of a linear BVP. Let us introduce a function solveBVP() which return final solution, u, and mesh points, x_mesh, with given arguments being BC, equation coefficients, finite element nodes, and interpolation along with quadrature nodes on the basis element (see [listing 2.8](#chapter2.xhtml_list2_8)).

![](images/comp02_13.jpg)

We could stop here and decide that the task of coding FEM is done, but one important part of any numerical simulation pipeline is missing. To make sure that we have done all correctly and to validate output results, we need a tool for error analysis. The main approach is to run simulation for a problem with known exact solution and then compare the output with true values in the form of error. To analyse FEM error when exact solution is known, it is worth having a function which calculates the error norm in spaces *L*[2] and *H*¹

$$\begin{array}{l} {e = u - u_{h},\quad\| e\|_{L_{2}}^{2} = \int\limits_{s_{0}}^{s_{1}}e^{2}(x)dx,\quad\| e\|_{H^{1}}^{2} = \int\limits_{s_{0}}^{s_{1}}\left( {e'(x)} \right)^{2}dx.} \end{array}$$

Function errorNorm() which code is given in [listing 2.9](#chapter2.xhtml_list2_9) calculates and outputs these norms. Here, e0 is a value of *L*[2] error norm, e1 is a value of *H*¹ error norm, u and du are exact solution and its derivative, y is an FEM solution, xl is a vector of finite element nodes and d is a vector of interpolation points on the basis element [0,1]. Function errorNorm() uses Gaussian quadrature to calculate the norms, and interpolating and differentiating matrices to find corresponding values of the solution.

![](images/comp02_14.jpg)

Now, we are ready to solve example problem using created library. Let us consider the following BVP

$$\begin{array}{cl} {{(u'\cos(x))}' - 2u'\sin(x) + u\sin(x)} & {= \sin^{2}(x),\quad x \in ( - 1,1),} \\ {\quad u( - 1)} & {= \sin( - 1),\quad u'(1) = \cos(1).} \end{array}$$(2.4)

Here, exact solution to be *u* = sin (*x*) and equation coefficients are the following functions: *c*(*x*) = cos (*x*), *b*(*x*) = −2sin (*x*), *a*(*x*) = sin (*x*), *f*(*x*) = sin²(*x*). Boundary points are *s*[0] = −1 and *s*[1] = 1. At the point *s*[0] we have Dirichlet BC which is a BC of the first type and at the point *s*[1] we have Neumann BC. The FEM library deals with either first or third type of BC, so we need to rewrite BC at the point *s*[1] in the form of BC of the third type, namely, in the form *c*(1)*u*^′(1) + *σ*(1)*u*(1) = *μ*(1). It is easy to see that *σ* = 0 and *μ* = cos²(1).

Having all basic functions for assembling and solving FEM, it is not difficult to write a script (see [listing 2.10](#chapter2.xhtml_list2_10)) which solves example BVP and plots solution along with error norm values.

![](images/comp02_15.jpg)![](images/comp02_15_2.jpg)

Plots generated by this script are shown in [figures 2.1](#chapter2.xhtml_fig2_1), [2.2](#chapter2.xhtml_fig2_2) and [2.3](#chapter2.xhtml_fig2_3) where the finite element nodes are indicated as circles and crosses are quadrature nodes which coincide with interpolation nodes.

![A one line graph representing solution. The line gradually increases, and points indicated as crosses and circles lay on the line.](images/fig2_1.jpg)

[Figure 2.1:](#chapter2.xhtml_b2fig2_1) FEM solution to the problem (2.4).

![A graph shows wavy line representing absolute solution error.](images/fig2_2.jpg)

[Figure 2.2:](#chapter2.xhtml_b2fig2_2) Absolute error of the FEM solution to the problem (2.4).

![A graph shows wavy line with spikes representing absolute solution derivative error. These spikes occur at the points where solution is continuous but not smooth.](images/fig2_3.jpg)

[Figure 2.3:](#chapter2.xhtml_b2fig2_3) Absolute error of the FEM solution derivative corresponding to the problem (2.4).

Estimations of numerical error for the FEM solution are given in [table 2.1](#chapter2.xhtml_tbl2_1). It can be seen that implementation of the FEM algorithm performs numerical calculations with acceptable accuracy.

[Table 2.1:](#chapter2.xhtml_b2tbl2_1) Summary of computational errors for the FEM solution to the problem (2.4).

| ∥*e*∥[*L*[2]] | ∥*e*∥[*H*¹] | ∥*e*∥[∞] | ∥*e*^′∥[∞] |
| 10^(−6) | 10^(−5) | 10^(−6) | 10^(−4) |

Changing equation coefficients and parameters of the FEM algorithm in the main script allows solving various BVP. A reader is encouraged to play around with different parameter settings (m,ne,M) and see how it affects solving time and errors magnitude.

## EXERCISE

*   ▶ Find numerical solution to the problems given below with known exact solutions. Boundary conditions of the first type may be chosen to close BVP. Specify your own values for parameter *ε*. Perform analysis of the solution behaviour when *ε* becomes small. Choose different FEM parameters and make observation regarding changes of the error magnitude.

    $$\begin{array}{ll} 1\. & {\quad - \varepsilon u^{''} + u = 0,\quad x \in (0,1),\quad u = \frac{\exp\left( {- \frac{x}{\sqrt{\varepsilon}}} \right) - \exp\left( \frac{x - 2}{\sqrt{\varepsilon}} \right)}{1 - \exp\left( {- \frac{2}{\sqrt{\varepsilon}}} \right)}.} \\ 2\. & {\quad - \varepsilon u^{''} - bu' + u = (1 + \varepsilon\pi^{2})\cos(\pi x) + b\pi\sin(\pi x),\quad x \in ( - 1,1),} \\ & {\quad b = 2 + \cos(\pi x),\quad u = \cos(\pi x).} \\ 3\. & {\quad - (\varepsilon + x^{2})u^{''} - 4xu' - 2u = 0,\quad x \in ( - 1,1),\quad u = \frac{1}{\varepsilon + x^{2}}.} \\ 4\. & {\quad - \varepsilon u^{''} + u = (1 + \varepsilon\pi^{2})\cos(\pi x),\quad x \in ( - 1,1),} \\ & {\quad u = \cos(\pi x) + \exp\left( \frac{x - 1}{\sqrt{\varepsilon}} \right) + \exp\left( {- \frac{x + 1}{\sqrt{\varepsilon}}} \right).} \end{array}$$

## 2.6 PYTHON IMPLEMENTATION

To give a reader more flexibility in implementing FEM, we turn our attention to the Python programming language and explain how to create FEM computational framework in Python. Basically, we are going to translate MATLAB codes into Python ones with some variations in specific features. We expect that a reader has basic Python programming skills.

For dense matrix operation we use NumPy library which provides broad range of specific functions for matrix manipulation and most of them have MATLAB analogy. Book [[7](#ref01.xhtml_refbib_7)] could be helpful in improving scientific programming skills using NumPy library.

There are some important notes regarding using vectors and matrices in Python. First, it is worth noting that indexing in Python starts with zero (unlike indexing in MATLAB starting with one) and all index values given in previous chapters should be decremented by one to correspond Python indexing.

Second, there is a distinction between different types of array data structure in Python. For example, there is a structure called list, a=[1,2,3], which stores data in array like manner, but it is not a vector in terms of ability to be used in matrix calculations; however if it is declared through NumPy library, a = numpy.array([1, 2, 3]), then it can be used in vectorized calculations, for example, in a dot product calculation of two arrays, numpy.dot(a,b). Conversion between list data structure to the numpy.array structure is supported by the NumPy library. Another note is that unlike in MATLAB where most built in functions support vectorized calculations using any array variable, in Python these vectorized calculations should be performed through explicitly calling NumPy library commands. For example, MATLAB version of square root function call on vector, j=1:n;s=sqrt(j.), in Python would have the form: j=numpy.arange(1,n);s=numpy.sqrt(j).

Also, unlike in many matrix languages, the product operator, *, operates elementwise in NumPy arrays, and matrix product can be performed using the numpy.matmul() or @ operator (in Python version ¿ =3.5). For example, having two matrices A=numpy.array([[1, 0],[0, 1]]) and B=numpy.array([[4, 1],[2, 2]]), result of operation A*B would be array([[4, 0],[0, 2]]), but A@B results in array([[4, 1],[2, 2]]).

Array slicing and indexing works exactly the same way it does for lists except that they can be applied to multiple dimensions as well. For example, given a matrix A, the command A[0,3] accesses a single element of the matrix, and A[:,3] extracts a column. Note that slices of arrays do not copy the internal array data but only produce new views of the original data, so if b=A[0,3] and b=b+1 then element of matrix A would be modified implicitly as well. If a copy is needed, then an explicit copy() command is required. NumPy arrays may be indexed with other arrays or lists. For all cases of index arrays, the copy of original data is returned, not a view. For example A[np.array([0,2,4]),0] or A[np.array([0,2,4])][0] returns elements of the first column with indices 0, 2 and 4.

To operate with sparse matrices in Python we use scipy.sparse library. There are various sparse matrix classes in scipy.sparse library (coo_matrix, csc_matrix, csr_matrix, etc.) to perform matrix manipulations of different types. For example, class coo_matrix is used for constructing a sparse matrix in coordinate format from arrays of indices and values (see [figure 2.1](#chapter2.xhtml_fig2_1) for detailed explanations) but it does not directly support arithmetic operations. Class sparse.lil_matrix is a structure for constructing sparse matrices incrementally which supports flexible slicing. Classes csr_matrix and csc_matrix are for compressed sparse row matrix and compressed sparse column matrix representations, respectively. These matrix formats are suitable for arithmetic operations and row/column slicing but inefficient for changing sparsity structure. Usually, coo_matrix is a fast format for constructing sparse matrices. Once a matrix has been constructed, conversion to csc_matrix or csr_matrix format is performed (explicitly or implicitly) for fast arithmetic and matrix vector operations.

Before start writing Python functions, it is required to import libraries which we will be using across the code. Script in [listing 2.11](#chapter2.xhtml_list2_11) shows how to perform importing. Libraries numpy and scipy.sparse are for working with dense and sparse matrices, spsolve is for solving sparse linear systems, plt is for plotting simulation results and timeit library allows operate with timing counters. We need to run this script only once in the FEM Python library.

![](images/comp02_16.jpg)

Python listings given below contain functions which names and functionality repeat ones written in MATLAB, so notations of arguments and returning values have consistent with MATLAB counterparts meaning. While providing Python implementation of particular function, the focus will be on specific Python language features which differ the code from MATLAB version rather than on describing logic, which already has been discussed in previous sections.

Let us look into Python implementation of Gaussian and Lobatto quadrature rules (see [listings 2.12](#chapter2.xhtml_list2_12) and [2.13](#chapter2.xhtml_list2_13)). By design, arguments s0 and s1 can be omitted, so the code line 2 retrieves the number of actual input arguments and stores it in the variable nargin. This is done through the function locals() which returns a vector of arguments, and the function len() returning vector length.

We can see in the code arithmetic calculation of the form j**2, which implements raising j to the second power. The function numpy.diag(bta,k) constructs a diagonal matrix from a given array, bta, and a diagonal position, k. The function linalg.eig(Q) computes eigenvalues and eigenvectors of the matrix Q. To obtain ordered eigenvalues, function numpy.argsort(L) is used which returns the indices that would sort the array L.

![](images/comp02_17.jpg)

Code lines 18–21 in [listing 2.13](#chapter2.xhtml_list2_13) implement extending arrays of weights, w, and nodes, d, with new values at the boundary. This is coded through the functions numpy.append() to append value to the end of the array, and numpy.insert() to insert the value at the beginning of the array. Overall, calculations follow linear logic of the corresponding algorithms for Gaussian and Lobatto quadrature rules.

![](images/comp02_18.jpg)

Script [listing 2.14](#chapter2.xhtml_list2_14) demonstrates how interpolating and differentiating matrices calculation can be implemented in Python. Note that it is a good practice to declare and initialize variables before using them to make it clear of what data manipulations are allowed to work with. Lines 2–6 introduce main variables which are used across the listing where nx and nd represent lengths of corresponding input arrays, E and D are declared to be zeroth matrices of dimension nd by nx, and b is a one-dimensional array of length nx. Function numpy.zeros((nd,nx)) returns a matrix of zeros with the given shape, (nd,nx), and if the second dimension is omitted, then a vector is returned. Looping with parameter can be coded through either specifying a range using a special function range(nx) (see line 7) which returns iterator spanning values in the range [0,nx), or giving the range explicitly as a vector of predefined values (see line 15). Formulas (2.1)–(2.3) which are coded in [listing 2.14](#chapter2.xhtml_list2_14) include calculation of product of elements which is implemented through function numpy.prod(). Indices over which the product in formulas is taken exclude particular values and this is implemented using numpy.delete() function which returns a new array with deleted sub-arrays (lines 8, 11 and 17).

![](images/comp02_19.jpg)

Along with calculation of interpolating and differentiating matrices, error norms calculations and mesh refinement are another complementary functionalities which simplify manipulating FEM data (see [listings 2.15](#chapter2.xhtml_list2_15) and [2.16](#chapter2.xhtml_list2_16)). Note that matrix multiplication is performed using @ operator.

![](images/comp02_20.jpg)![](images/comp02_21.jpg)

Let us discuss in more details [listing 2.17](#chapter2.xhtml_list2_17) for assembling FEM matrices. Here, we use sparse matrices as a main data structure for stiffness matrix, A, and forcing vector, F, and declare them through sparse.coo_matrix() class. This class allows creating matrices in coordinate form using constructor coo_matrix((data, (i, j)), shape=(m, n)), where (m,n) are the matrix dimensions, data is an array of matrix entries, i is an array of row indices and j is an array of column indices of the matrix entries. If arguments (data, (i, j)) are omitted, then an empty sparse matrix of given shape will be created, as shown in code lines 8 and 9\. Class for sparse matrices in Python does not support advanced indexing, so the best way of assembling stiffness matrix is to use extended local matrix as a summand when accumulating final stiffness matrix (see [definition 1.10](#chapter1.xhtml_defi1_10) and [algorithm 2](#chapter2.xhtml_comp02_2)). Recall that extended local stiffness matrix has all zeros apart from the diagonal block for corresponding final element. Assume that we have a final element with three nodes, so the block would be 3 × 3 = 9 elements and to construct a bock diagonal sparse matrix we need three arrays with nine elements each, namely, indices i=[0,0,0,1,1,1,2,2,2], j=[0,1,2,0,1,2,0,1,2] and data with some data values which are flatten one-dimensional representation of two-dimensional (3 × 3) block. Generating local indices is implemented in lines 10–12, where i_loc is a range of local node indices, i_loc_sp_mat is an array of local row indices and j_loc_sp_mat is an array of local column indices for the sparse matrix constructor. Here, function numpy.repeat(i_loc,m+1) repeats each element of the array i_loc given number of times, m+1, and numpy.tile(i_loc,m+1) construct an array by repeating entire array i_loc the number of times, m+1. After calculating local matrix in dense form (line 19), global row and column indices are calculated (lines 20–21), and extended stiffness matrix is added in the form of sparse matrix (see line 22). This approach illustrates a possible way of manipulating with sparse matrices.

![](images/comp02_22.jpg)

Script for assembling BC (see [listing 2.18](#chapter2.xhtml_list2_18)) follows linear logic of replacing corresponding values in stiffness matrices by the BC values. Some comments are added to make it clear which part of the code responsible for the BC of the first type and which one for the third type. The function returns matrices A0 and F0 which are ready to be used with linear solver.

![](images/comp02_23.jpg)

[Listings 2.19](#chapter2.xhtml_list2_19) and [2.20](#chapter2.xhtml_list2_20) show function implementations for solving FEM and BVP. Note how the sparse linear system is solved using sparse.linalg.spsolve() function.

![](images/comp02_24.jpg)![](images/comp02_25.jpg)

Finally, the main script for testing example problem is given in [listing 2.21](#chapter2.xhtml_list2_21). To specify equation coefficients and exact solution, we use inline function definitions (lines 6–12) with corresponding vectorized numpy functions. Also, built-in function numpy.linalg.norm() is used to calculate various norms, for example, ||⋅∥[∞] norm is printed in lines 37–39.

![](images/comp02_26.jpg)![](images/comp02_26_2.jpg)

# Chapter 3 Finite Element Method for the Two-Dimensional Boundary Value Problem

DOI: [10.1201/9781003265979-3](https://doi.org/10.1201/9781003265979-3)

BY learning how to solve one-dimensional BVP using FEM, we have gained knowledge allowing us to take next step and consider two-dimensional case. Although all steps of the algorithm for the two-dimensional case are similar to the one-dimensional one, their implementations are different and require specific features and coding strategies to be considered.

We begin by formulating a model problem in terms of linear partial differential equation with mixed boundary conditions. Then, an integral formulation of the model problem is given with further finite element discretization. We introduce basis functions and show how the discretized problem can be reduced to solving a linear system. Also, basic concepts of two-dimensional mesh with finite elements having triangular shape are discussed.

Notations introduced in [chapter 1](#chapter1.xhtml) are used across the current chapter along with new ones given below.

## GLOSSARY

***f*(**x**):** a function of multiple variables.

****f**(**x**):** a multivariate function of multiple variables.

**$\frac{\partial f}{\partial x_{1}},\frac{\partial f}{\partial x_{2}},\frac{\partial^{2}f}{\partial x_{1}\partial x_{2}},\ldots$:** partial derivatives of a function *f*(**x**).

**∇:** the nabla operator with definition $\nabla f = \left( {\frac{\partial f}{\partial x_{1}},\frac{\partial f}{\partial x_{2}}} \right)^{T}$.

## 3.1 MODEL PROBLEM

Similar to the one-dimensional case, two-dimensional FEM approach will be based on considering a generic BVP which can be reduced to a specific problem by simplifying particular terms in the BVP formulation. This allows to deduce a FEM algorithm which covers as many application problems as possible.

Consider a BVP of finding a function *u* = *u*(**x**) in two-dimensional region Ω with piecewise smooth boundary *Γ* = *Γ*[*D*] ∪ *Γ*[*R*]

$$\begin{array}{l} {- \nabla \cdot \left( {c(\mathbf{\mathbf{x}})\nabla u} \right) + \mathbf{\mathbf{b}}(\mathbf{\mathbf{x}}) \cdot \nabla u + a(\mathbf{\mathbf{x}})u = f(\mathbf{\mathbf{x}}),\quad\mathbf{\mathbf{x}} = (x_{1},x_{2}) \in \Omega,} \end{array}$$(3.1)

$$\begin{array}{ll} & {u(\mathbf{\mathbf{x}}) = u_{D}(\mathbf{\mathbf{x}}),\,\mathbf{\mathbf{x}} \in \Gamma_{D},} \\ & {c(\mathbf{\mathbf{x}})\nabla u \cdot \mathbf{\mathbf{\nu}}(\mathbf{\mathbf{x}}) + \sigma(\mathbf{\mathbf{x}})u = \mu(\mathbf{\mathbf{x}}),\,\mathbf{\mathbf{x}} \in \Gamma_{R}.} \end{array}$$

Here, *Γ*[*D*] and *Γ*[*R*] are the boundary parts for Dirichlet and Robin boundary conditions, respectively, and either of them could be empty (in this case the corresponding boundary condition is omitted); Γ is supposed to be closed; **ν**(**x**) is the unit outward normal vector at the point **x**. Functions *c*, *a*, *f*, *u*[*D*], *σ*, *μ* and **b**(**x**) = (*b*[1](**x**), *b*[2](**x**))^(*T*) are known and supposed to be piecewise smooth. The model problem (3.1) can be reduced to variety of particular problems with appropriate definition of the coefficients, for example, when *c*(**x**) = 1, **b**(**x**) = *a*(**x**) = 0 we come to a Poisson’s equation.

Let us reformulate the problem (3.1) in terms of integral equations. First, we consider function sets 𝒲 and 𝒲⁰

$$\begin{array}{ll} {\mathcal{W} =} & {\left\{ {w \in H^{1}(\Omega):w(\mathbf{\mathbf{x}}) = u_{D}(\mathbf{\mathbf{x}}),\, x \in \Gamma_{D}} \right\},} \\ {\mathcal{W}^{0} =} & {\left\{ {w \in H^{1}(\Omega):w(\mathbf{\mathbf{x}}) = 0,\, x \in \Gamma_{D}} \right\},} \end{array}$$

where *H*¹(*Ω*) is the Sobolev space. Then, perform a standard sequence of steps to come to the integral formulation of the problem. We follow the logic of the projective method described in [section 1.2](#chapter1.xhtml_sec1_2) which is equally applied to the two-dimensional case. By multiplying equation (3.1) by function *v* ∈ 𝒲⁰, integrating over region Ω, applying Gauss theorem[¹](#chapter3.xhtml_fn3_1) and taking into account boundary conditions we come to the formulation of the problem in the form

$$\begin{array}{r} {\int\limits_{\Omega}{\left( {c\nabla u \cdot \nabla + b \cdot \nabla uv + auv} \right)dx + {\int\limits_{\Gamma_{R}}{\sigma uvdx}}}} \\ {= {\int\limits_{\Omega}{fvdx +}}{\int\limits_{\Gamma_{R}}{\mu vdx.}}} \end{array}$$(3.2)

Now, the problem can be formulated as follows: find a function *u* ∈ 𝒲 so that, for any *v* ∈ 𝒲⁰, the function *u* satisfies equation (3.2). Here, functions *v* are the test functions.

## 3.2 FINITE ELEMENTS DEFINITION

Let us introduce 𝒯[*h*] - partitioning (triangulation) of the domain Ω by finite elements *τ*, and all boundary points Γ are vertices of some elements. A finite element is a triple (*τ*, 𝒫[*τ*], 𝒢[*τ*]), where *τ* is the closed area of a simple form (triangle or polygon), 𝒫[*τ*] are the interpolation points belonging to *τ* and 𝒢[*τ*] are interpolation functions defined on *τ* (maximum diameter of elements in 𝒯[*h*] is denoted by *h*). Then, *Γ*[*D*]^(*h*) and *Γ*[*R*]^(*h*) are partitioning of *Γ*[*D*] and *Γ*[*R*], respectively. We introduce notation: 𝒫[*h*] is a set of all interpolation points (grid points of 𝒯[*h*]), 𝒫[*D*] is a set of points belonging to *Γ*[*D*]^(*h*) and 𝒫[*R*] is a set of points belonging to *Γ*[*R*]^(*h*). Now, we are looking for functions *u*[*h*] and *v*[*h*] defined on grid 𝒫[*h*] so that

$$\begin{array}{cl} {\int\limits_{\mathcal{T}_{h}}{\left( {c\nabla u_{h} \cdot \nabla v_{h} + \mathbf{\mathbf{b}} \cdot \nabla u_{h}v_{h} + au_{h}v_{h}} \right)d\mathbf{\mathbf{x}}}} & {+ {\int\limits_{\Gamma_{R}^{h}}{\sigma u_{h}v_{h}d\mathbf{\mathbf{x}}}}} \\ = & {{\int\limits_{\mathcal{T}_{h}}{fv_{h}d\mathbf{\mathbf{x}}}} + {\int\limits_{\Gamma_{R}^{h}}{\mu v_{h}d\mathbf{\mathbf{x}}}}.} \end{array}$$(3.3)

Function *u*[*h*] represents an approximate solution to the BVP and the FEM is to find this function.

## 3.3 TRIANGULATION EXAMPLES

[Figure 3.1](#chapter3.xhtml_fig3_1)(a) shows example of the domain triangulation with three interpolation points. In this case, the finite element *τ* is a triangle, interpolation points 𝒫[*τ*] are the triangle’s vertices and interpolation functions 𝒢[*τ*] = 𝒢[1] = {*g*[1] + *g*[2]*x*[1] + *g*[3]*x*[2]} are polynomials of the first order. Any two elements share either edge or vertex and each edge contains two interpolation points.

![Two parts image showing rough triangulation of the geometry having square shape. Part (a) shows a square tessellated with triangles. Triangle vertices are interpolation points at the same time. Part (b) shows a square tessellated with triangles. Every triangle side has a middle point, as a result part (b) of the image has many more interpolation points compared to part (a).](images/fig3_1.jpg)

[Figure 3.1:](#chapter3.xhtml_b3fig3_1) Examples of the triangulation with three (a) and six (b) interpolation points over a triangle element.

[Figure 3.1](#chapter3.xhtml_fig3_1)(b) shows triangulation with six interpolation points. Each 𝒢[*τ*] includes vertices and in-between points belonging to the edges. As a result, three points of interpolation are available for each edge and the interpolation function is of the second order, 𝒢[*τ*] = 𝒢[2] = {*g*[1] + *g*[2]*x*[1] + *g*[3]*x*[2] + *g*[4]*x*[1]² + *g*[5]*x*[1]*x*[2] + *g*[6]*x*[2]²}.

## 3.4 LINEAR SYSTEM OF THE FEM

Equation (3.3) reduces to the system of linear equation. Firstly, we need to select basis functions which define interpolation over finite elements *τ*. We define basis functions as follows: Let us enumerate all points 𝒫[*h*] from 1 to *n*[*p*] and assign a basis function *φ*[*i*](**x**) to each point **p**[*i*] ∈ 𝒫[*h*] so that *φ*[*i*](**p**[*j*]) = *δ*[*i**j*], *j* = 1, …, *n*[*p*]. [²](#chapter3.xhtml_fn3_2) Then, any *v*[*h*] can be represented in the form of interpolating polynomial

$$\begin{array}{l} {v_{h}(\mathbf{\mathbf{x}}) = {\sum\limits_{i = 1}^{n_{p}}{v_{i}\varphi_{i}(\mathbf{\mathbf{x}})}},} \end{array}$$

where *v*[*i*] = *v*(**p**[*i*]). Let us divide set of indices ℐ = {1, 2, …, *n*[*p*]} into two subsets: ℐ[*D*] = {*i* ∈ ℐ : **p**[*i*] ∈ 𝒫[*D*]} and ℐ[*U*] = {*i* ∈ *I* : **p**[*i*] ∉ 𝒫[*D*]}. Solution at the points **p**[*i*[*D*]] is known from the boundary condition (*u*[*h*](**p**[*i*[*D*]]) = *u*[*D*[*i*]]). We need to find a solution at the points **p**[*i*[*U*]].

The following expansions are valid in 𝒯[*h*]:

$$\begin{array}{l} {u_{h}(\mathbf{\mathbf{x}}) = {\sum\limits_{i \in i_{U}}{u_{i}\varphi_{i}(\mathbf{\mathbf{x}})}} + {\sum\limits_{i \in i_{D}}{u_{D_{i}}\varphi_{i}(\mathbf{\mathbf{x}})}},\quad v_{h}(\mathbf{\mathbf{x}}) = {\sum\limits_{i \in i_{U}}{v_{i}\varphi_{i}(\mathbf{\mathbf{x}})}}.} \end{array}$$(3.4)

Let us define a matrix *Ã* ∼ (*n*[*p*] × *n*[*p*]) and a vector $\left. \widetilde{\mathbf{\mathbf{F}}} \right.\sim(n_{p} \times 1)$ having components

$$\begin{array}{l} {{\widetilde{A}}_{ij} = {\int\limits_{\mathcal{T}_{h}}{\left( {c\nabla\varphi_{j} \cdot \nabla\varphi_{i} + \mathbf{\mathbf{b}} \cdot \nabla\varphi_{j}\varphi_{i} + a\varphi_{j}\varphi_{i}} \right)d\mathbf{\mathbf{x}}}} + {\int\limits_{\Gamma_{R}^{h}}{\sigma\varphi_{j}\varphi_{i}d\mathbf{\mathbf{x}}}}} \end{array}$$(3.5)

$$\begin{array}{l} {{\widetilde{F}}_{i} = {\int\limits_{\mathcal{T}_{h}}{f(\mathbf{\mathbf{x}})\varphi_{i}d\mathbf{\mathbf{x}}}} + {\int\limits_{\Gamma_{R}^{h}}{\mu(\mathbf{\mathbf{x}})\varphi_{i}d\mathbf{\mathbf{x}}}}} \end{array}$$(3.6)

where *Ã* is called global stiffness matrix and $\widetilde{\mathbf{\mathbf{F}}}$ is the global forcing vector. Then, equation (3.3) can be rewritten in the form of the linear system (see [section 1.3.3](#chapter1.xhtml_sec1_3_3) for details)[³](#chapter3.xhtml_fn3_3)

$$\begin{array}{l} {{\sum\limits_{j \in \mathcal{I}_{U}}{{\widetilde{A}}_{ij}u_{j}}} = q_{i},\quad q_{i} = {\widetilde{F}}_{i} - {\sum\limits_{j \in \mathcal{I}_{D}}{{\widetilde{A}}_{ij}u_{D_{j}}}},\, i \in \mathcal{I}_{U}.} \end{array}$$(3.7)

By solving system (3.7) we define *u*[*j*], *j* ∈ ℐ[*U*], and the approximation solution of the problem (3.2) is found from (3.4). Although matrix and vector elements can be defined from (3.5) and (3.6), these formulas are not usually used for calculation purpose. There exists more convenient and efficient calculation method which we consider below.

## 3.5 STIFFNESS MATRIX AND FORCING VECTOR

Linear system (3.7) implies calculation of matrix *Ã* and vector $\widetilde{\mathbf{\mathbf{F}}}$. In practical application problems, these matrices are usually of large sizes and chosen calculation method affects overall performance of the FEM programming implementation. Here, we consider efficient method of their calculation.

It is followed from (3.5) that matrix *Ã* is a sum of two square matrices of (*n*[*p*] × *n*[*p*]) dimension: *Ã* = *A* + *S*,[⁴](#chapter3.xhtml_fn3_4)

$$\begin{array}{ll} A_{ij} & {= {\int\limits_{\mathcal{T}_{h}}{\left( {c\nabla\varphi_{j} \cdot \nabla\varphi_{i} + \mathbf{\mathbf{b}} \cdot \nabla\varphi_{j}\varphi_{i} + a\varphi_{j}\varphi_{i}} \right)d\mathbf{\mathbf{x}}}},} \\ S_{ij} & {= {\int\limits_{\Gamma_{R}^{h}}{\sigma\varphi_{j}\varphi_{i}d\mathbf{\mathbf{x}}}},\quad i,j = 1,\ldots,n_{p}.} \end{array}$$

Similarly,

$$\begin{array}{l} {\widetilde{\mathbf{\mathbf{F}}} = \mathbf{\mathbf{F}} + \mathbf{\mathbf{M}},\quad F_{i} = {\int\limits_{\mathcal{T}_{h}}{f\varphi_{i}d\mathbf{\mathbf{x}}}},\quad M_{i} = {\int\limits_{\Gamma_{R}^{h}}{\mu\varphi_{i}d\mathbf{\mathbf{x}}}},\quad i = 1,\ldots,n_{p}.} \end{array}$$

Recall that triangulation 𝒯[*h*] is a union of finite elements *τ*, that is $\mathcal{T}_{h} = {\underset{l = 1}{\overset{n_{t}}{\cup}}\tau_{l}}$ where *n*[*t*] is the total number of finite elements. It is assumed that there are *m*[*τ*] number of interpolation points belonging to the element *τ*[*l*] (for the triangular 𝒢[1] element *m*[*τ*] = 3) and these points are ordered (locally numerated): **p**[*i*[1]], **p**[*i*[2]], …, **p**[*i*[*m*[*τ*]]]. Let us specify a connectivity matrix, *t* ∼ (*m*[*τ*] × *n*[*t*]), and place into *l*^(*t**h*) column the indices of the points of the *l*^(*t**h*) element (*i*[1], *i*[2], …, *i*[*m*[*τ*]]) so that *t*[*j**l*] defines index of the *j*^(*t**h*) point (in local order) belonging to the element *τ*[*l*].

**Calculation of *A* and **F****. Represent the integral over triangulation 𝒯[*h*] through the sum of integrals over elements *τ*[*l*]. Using the matrix of indices, *t*[*j**l*], we can introduce a matrix ${\overline{A}}^{l}$ with the components

$$\begin{array}{ll} {{\overline{A}}_{\alpha\beta}^{l} = {\int\limits_{\tau_{l}}\left( {c\nabla\varphi_{t_{\beta l}} \cdot \nabla\varphi_{t_{\alpha l}} + \mathbf{\mathbf{b}} \cdot \nabla\varphi_{t_{\beta l}}\varphi_{t_{\alpha l}} + a\varphi_{t_{\beta l}}\varphi_{t_{\alpha l}}} \right)}} & {d\mathbf{\mathbf{x}},} \\ {\alpha,} & {\beta = 1,\ldots,m_{\tau},} \end{array}$$

which is the local stiffness matrix of the finite element *τ*[*l*]. Now, we can express global matrix in terms of local stiffness matrices by introducing extended local stiffness matrix *A*^(*l*) ∼ (*n*[*p*] × *n*[*p*]) so that matrix *A*^(*l*) contains zeros except of elements with indices *t*[*α**l*] and *t*[*β**l*], and

$$\begin{array}{l} {A_{t_{\alpha l},t_{\beta l}}^{l} = {\overline{A}}_{\alpha\beta}^{l},\quad\alpha,\beta = 1,\ldots,m_{\tau}.} \end{array}$$

For example, matrix *A*^(*l*) for the triangular 𝒢[1] element has *m*[*τ*] × *m*[*τ*] = 3 × 3 = 9 nonzero elements. As a result,

$$\begin{array}{l} {A = {\sum\limits_{l = 1}^{n_{t}}A^{l}}.} \end{array}$$

The latter expression indicates that the global stiffness matrix *A* can be obtained by summation of the extended local stiffness matrices, *A*^(*l*). Since there is no sense to sum up zeros, we come to the algorithm of composing global matrix *A* (see [algorithm 4](#chapter3.xhtml_comp03_1)).

![](images/comp03_1.jpg)

Similarly, the algorithm for calculation of **F** can be obtained (see [algorithm 5](#chapter3.xhtml_comp03_2)). Vector $\mathbf{\overline{F}}^{l}$ is called the local force vector.

![](images/comp03_2.jpg)

**Calculation *S* and **M**.** Matrix *S* and vector **M** contain boundary integrals over *Γ*[*R*]^(*h*), so the calculations are performed only using interpolation points belonging to the boundary. Let us introduce, analogous to matrix of indices *t*, a matrix of indices associated with edges, *e* ∼ (*m*[*e*] × *n*[*e*]), which is called edge matrix. Here *n*[*e*] is the number of edges belonging to the boundary *Γ*[*R*]^(*h*) and *m*[*e*] is the number of interpolation points on the edge. In other words, *e*[*j**k*] defines index of the *j*^(*t**h*) point (in local order) belonging to the *k*^(*t**h*) boundary edge. As a result, for the *k*^(*t**h*) edge, *e*[*k*], we can define a local matrix ${\overline{S}}^{k}$ with elements

$$\begin{array}{l} {{\overline{S}}_{\alpha\beta}^{k} = {\int\limits_{e_{k}}{\sigma(\mathbf{\mathbf{x}})\varphi_{e_{\beta k}}\varphi_{e_{\alpha k}}d\mathbf{\mathbf{x}}}}.} \end{array}$$

By introducing extended matrix *S*^(*k*) (see similar extended matrix *A*^(*l*)) we obtain

$$\begin{array}{l} {S = {\sum\limits_{k = 1}^{n_{e}}S^{k}}.} \end{array}$$

Vector **M** is calculated through introducing a local vector $\mathbf{\overline{M}}^{k}$ for each edge *e*[*k*]

$$\begin{array}{l} {{\overline{M}}_{\alpha}^{k} = {\int\limits_{e_{k}}{\mu(\mathbf{\mathbf{x}})\varphi_{e_{\alpha k}}(\mathbf{\mathbf{x}})d\mathbf{\mathbf{x}}}},} \end{array}$$

and summation of the extended vectors **M**^(*k*) across all edges

$$\begin{array}{l} {\mathbf{\mathbf{M}} = {\sum\limits_{k = 1}^{n_{e}}\mathbf{\mathbf{M}}^{k}}.} \end{array}$$

Algorithm of composing matrix *S* and vector **M** is the same as for matrix *A* and vector **F**.

## 3.6 ALGORITHM OF SOLVING PROBLEM

[Algorithm 6](#chapter3.xhtml_comp03_3) summarizes previous results and describes sequence of steps to find the approximate solution to the problem (3.2).

![](images/comp03_3.jpg)

In the following chapters we will discuss each step of this algorithm and provide implementation codes which form a FEM framework library. Programming framework for the FEM will be obtained in MATLAB as well as in Python programming language. Mathematical formulations obtained above will serve as defining expressions for coding numerical methods. To make the code consistent, the same data structures for the FEM representation across both languages implementations are going to be used.

# Chapter 4 Building Two-Dimensional Meshes

DOI: [10.1201/9781003265979-4](https://doi.org/10.1201/9781003265979-4)

FIRST four steps of the FEM algorithm given in [section 3.6](#chapter3.xhtml_sec3_6) will be covered in this chapter. We will describe how to define geometry of a problem and build two-dimensional triangular mesh using MATLAB and Python tools. Basic data structure for the mesh representation will be considered.

Basically, generating geometry for a domain with simple boundary shape is not a challenge; however things become more complicated when a geometry has subdomains or nontrivial boundary shape. In general, the problem of generating geometry can be viewed as having two tasks: geometry definition through some data structure, and performing triangulation to build finite elements. In this chapter we are focussed on the first task, namely, various approaches of how to create data structures for geometry definition and how to represent mesh in a matrix form. Questions of how to encode boundary and build geometry will be discussed as well.

To perform triangulation itself using predefined geometry definition, we are going to use specific MATLAB and Python tools. Triangulation algorithm implementation is not discussed below and it is beyond the scope of the book, but rather existing implementation as a tool or third-party library is used. Interested reader can find mesh generating algorithms in [[3](#ref01.xhtml_refbib_3)] where some triangulation techniques are discussed.

## 4.1 DEFINING GEOMETRY

Let us start with considering an example geometry to show how it can be represented to use with the FEM solver. [Figure 4.1](#chapter4.xhtml_fig4_1) shows an example of the geometry domain Ω. This domain consists of three labelled subdomains, *Ω*[1], *Ω*[2] and *Ω*[3] so that *Ω* = *Ω*[1] ∪ *Ω*[2] ∪ *Ω*[3]. It is seen that *Ω*[1] and *Ω*[3] are rectangles and *Ω*[2] is a square. A circle of radius 0.25 is removed from *Ω*[1]. Also, it is highlighted that we have internal area of the geometry (coloured in grey) and external one which is called complement of the domain Ω and will be referenced as *Ω*[0]. The geometry is split into subdomains to illustrate the fact that PDE coefficients could be different in these subdomains and we need to take it into account.

![An image shows geometry domain having rectangular shape. It is divided into subdomains and each subdomain is labelled. The rectangle is separated by line into upper part and bottom part. Upper part has a square inside it with label of 2 and the rest area of the upper part is labelled with number 3\. Bottom part of the rectangle is labelled with number 1 and the area with the shape of circle is removed from the bottom part.](images/fig4_1.jpg)

[Figure 4.1:](#chapter4.xhtml_b4fig4_1) Example of the domain with labelled subdomains.

Next, boundaries of the geometry are considered (see [figure 4.2](#chapter4.xhtml_fig4_2)). Boundaries of *Ω*[1], *Ω*[2] and *Ω*[3] are split into segments. Segments are labelled, they cannot intersect and have single common end point. As a result, the square is specified with a minimum of four segments and the circle – with two segments. We define internal and external (boundary) segments. Specific boundary conditions could be specified on each segment. [Figure 4.2](#chapter4.xhtml_fig4_2) shows the boundary consisting of 15 segments including 5 internal ones (labelled as 2, 3, 6, 10 and 11). Each segment line can be described in a parametric form

![An image shows geometry domain with the same structure as shown in figure 4.1 but now each boundary of subdomain is labelled. Every boundary line is shown as arrow showing direction to follow the boundary when boundary parameter increases.](images/fig4_2.jpg)

[Figure 4.2:](#chapter4.xhtml_b4fig4_2) Example domain with labelled boundaries.

$$\begin{array}{l} {x_{1} = x_{1}(s),\mspace{9mu} x_{2} = x_{2}(s),\mspace{9mu} s \in \lbrack s_{0},s_{1}\rbrack.} \end{array}$$

For example, a straight line can be parameterized as follows:

$$\begin{array}{l} {\mathbf{\mathbf{x}}(s) = \mathbf{\mathbf{x}}^{start} + s\left( {\mathbf{\mathbf{x}}^{end} - \mathbf{\mathbf{x}}^{start}} \right),\mspace{9mu} s \in \lbrack 0,1\rbrack,} \end{array}$$(4.1)

where **x**^(*s**t**a**r**t*) = **x**(0) and **x**^(*e**n**d*) = **x**(1) are starting and ending points of a line segment. A circle segment has a parametric form

$$\begin{array}{l} {x_{1}(s) = r\cos(s) + x_{1}^{centre},\mspace{9mu} x_{2}(s) = r\sin(s) + x_{2}^{centre},s \in \lbrack s_{0},s_{1}\rbrack,} \end{array}$$(4.2)

where *r* is a radius and **x**^(*c**e**n**t**r**e*) is a circle centre point.

When following the segment from the starting point having parameter value of *s*[0] to the endpoint with parameter value of *s*[1], there is always one subdomain on the left and one on the right hand side. For example, *Ω*[3] is on the left and *Ω*[0] is on the right when following the indicated direction of segment 5; *Ω*[0] is on the left and *Ω*[3] is on the right when following the direction of the segment 9\. Thus, parameter order is important and it defines the direction of boundary path.

As a result, the geometry shown in [figure 4.2](#chapter4.xhtml_fig4_2) can be uniquely defined by specifying two matrices: matrix of parameter values, *S*[*p**a**r**a**m*], and endpoints coordinates *X*[1]*X*[2]

$$\begin{array}{l} {S_{param} = \left( \begin{array}{lllllllllllllll} 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & \pi & \frac{3\pi}{2} & 0 & \frac{\pi}{2} \\ 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & \frac{3\pi}{2} & {2\pi} & \frac{\pi}{2} & \pi \\ 0 & 3 & 3 & 1 & 3 & 3 & 0 & 0 & 0 & 3 & 3 & 0 & 0 & 0 & 0 \\ 1 & 2 & 2 & 0 & 0 & 2 & 1 & 3 & 3 & 2 & 1 & 1 & 1 & 1 & 1 \end{array} \right)} \end{array}$$

$$\begin{array}{l} {X_{1}X_{2} = \left( \begin{array}{lllllllllll} 2 & 1.25 & 1.25 & 2 & 2 & 0.75 & 0 & 0 & 0 & 0.75 & 0 \\ 0 & 1.25 & 0.75 & 2 & 2 & 1.25 & 0 & 0 & 2 & 0.75 & 2 \\ {- 1} & 0.75 & 0.25 & {- 1} & 0 & 0.75 & {- 1} & 0 & 1 & 0.25 & 0 \\ {- 1} & 0.25 & 0.25 & 0 & 1 & 0.75 & 0 & 1 & 1 & 0.75 & 0 \end{array} \right)} \end{array}$$

Here, matrix *S*[*p**a**r**a**m*] ∼ (4 × 15) has 15 columns with one column per boundary segment. Columns from first to eleventh are for straight line segments and from twelve to fifteen are for circle segments. First and second rows of *S*[*p**a**r**a**m*] contain parameter values for starting and endpoint of the corresponding segment, third and fourth rows contain labels of the left hand and right hand regions correspondingly. Matrix *X*[1]*X*[2] ∼ (4 × 11) encodes coordinates of straight line segments with one column per segment. Here, first two rows are *x*[1] coordinates of starting and endpoints, and the last two rows are *x*[2] coordinates of line segments correspondingly. Having matrices *S*[*p**a**r**a**m*] and *X*[1]*X*[2] along with formulas (4.1) and (4.2) allows calculating coordinates of any point on the boundary given an index of boundary segment. In general, quite complicated geometries (not only lines and circles) can be represented through parametric form and encoded in the similar way.

Here, we introduce a MATLAB function geometryFunction(b_index, s) which returns (*x*[1], *x*[2]) coordinates of a boundary point for any segment with index b_index and parameter value s. Parameter b_index can be either scalar or vector and it is allowed to omit parameters. Function call with a single argument, geometryFunction(b_index), returns corresponding entries of the matrix *S*[*p**a**r**a**m*] with one column for each boundary segment specified in b_index. If the function is called without arguments, geometryFunction(), it returns total number of boundary segments.

![](images/comp04_1.jpg)

After defining geometry boundaries, the next step is to perform triangulation to obtain a mesh for the FEM algorithm. Before looking into specific methods of mesh building, let us first discuss data structures which are used for triangular mesh representation.

## 4.2 REPRESENTING MESHES IN MATRIX FORM FOR LINEAR INTERPOLATION FUNCTIONS

Above, we have discussed data structures to encode geometry with subdomaines definition given in [figure 4.1](#chapter4.xhtml_fig4_1) and boundary segments specification given in [figure 4.2](#chapter4.xhtml_fig4_2). The next logical step would be considering triangulation which is illustrated in [figure 4.3](#chapter4.xhtml_fig4_3) for the example geometry. In this book, only triangular mesh is used leaving other types beyond the scope (for example, mesh with rectangular elements).

![An image shows geometry domain with the same structure as shown in figure 4.1 but now it is tessellated with triangles.](images/fig4_3.jpg)

[Figure 4.3:](#chapter4.xhtml_b4fig4_3) Mesh for example geometry.

In this section, we do not consider methods to build a mesh itself but instead, we are focussed on how the mesh can be represented as a data structure. It is assumed that there exists a triangular mesh and we want to encode it. Linear interpolation functions are considered here (with three interpolation nodes), so triangle vertices are the mesh nodes and interpolation nodes at the same time. Let us call it 𝒢[1] mesh stressing that it is used when solution is approximated by a polynomial of the first order.

In general, the mesh data structure should serve two main purposes. Firstly, it should provide information about triangle vertices to allow performing interpolation on elements. Secondly, it should contain information about element edges which belong to boundary segments to correctly apply BC. As such, the mesh data should encapsulate information about mesh points, their connectivity to form triangles (finite elements) and relation between element edges and boundary segments. One of the most convenient forms of mesh representation which has became an industry standard is a matrix form. Three matrices, *P*,*T* and *E*, store all necessary information which allow apply FEM interpolation algorithms. Below we discuss them individually.

Given enumerated *n*[*p*] mesh points, let us form a matrix *P* ∼ (2 × *n*[*p*]) which stores coordinates of mesh points (triangle vertices) so that for *i*^(*t**h*) point coordinate *x*[1] = *P*[1, *i*] and *x*[2] = *P*[2, *i*]. Matrix *P* can be used to access any mesh points but it does not keep any information about mesh elements formation.

Structure representing how mesh triangles are formed from the set of vertices is called connectivity matrix, *T*. Given a number of triangles, *n*[*t*], matrix *T* ∼ (4 × *n*[*t*]) stores indices of vertices for each triangular element and corresponding subdomain label to which this triangle belongs. Elements *T*[1, *j*], *T*[2, *j*] and *T*[3, *j*] are the indices of vertices of the *j*^(*t**h*) triangle (counted anticlockwise), element *T*[4, *j*] is the subdomain label. Note that the matrix *T* is formed using indices of points from matrix *P*, so the order in which points are arranged in *P* is important.

The last structure is an edge matrix, *E*, which stores information regarding finite element edges belonging to the boundary segments (internal and external). Given a number of edges, *n*[*e*], matrix *E* ∼ (7 × *n*[*e*]) contains the following information. Elements *E*[1, *k*] and *E*[2, *k*] contain indices of vertices belonging to the *k*^(*t**h*) edge (vertex index with respect to matrix *P*), elements *E*[3, *k*] and *E*[4, *k*] are the corresponding parameter values *s*[0] and *s*[1] for parametric representation, element *E*[5, *k*] is the index of boundary segment to which the edge belongs, elements *E*[6, *k*] and *E*[7, *k*] are the subdomain labels from the left and right hand side of the edge according to the parameterization direction.

To better understand mesh encoding, let us consider a simple case of L-shaped geometry given in [figure 4.4](#chapter4.xhtml_fig4_4) with 3 subdomains and 10 boundary segments (8 external and 2 internal segments). Splitting each square (subdomain) into two triangles results in rough mesh with 6 finite elements. In [figure 4.4](#chapter4.xhtml_fig4_4), all points and boundary segments are enumerated.

![An image shows geometry domain composed from three squares. Two squares are placed one next to other and the third one is placed above the second one to form L-shape. Every square is divided into two triangles by its diagonal. Every triangle vertex and square side is labelled with some number.](images/fig4_4.jpg)

[Figure 4.4:](#chapter4.xhtml_b4fig4_4) L-shaped domain with rough triangulation.

Matrices *P*,*T* and *E* for the mesh shown in [figure 4.4](#chapter4.xhtml_fig4_4) have the form

$$\begin{array}{l} {P = \left( \begin{array}{lllllllll} {- 1} & {- 1} & 0 & 1 & 0 & 1 & 1 & 0 & \\ 0 & {- 1} & 1 & 1 & {- 1} & {- 1} & 0 & 0 & \end{array} \right),} \end{array}$$

$$\begin{array}{l} {T = \left( \begin{array}{llllll} 1 & 4 & 7 & 2 & 5 & 6 \\ 2 & 3 & 4 & 5 & 6 & 7 \\ 8 & 8 & 8 & 8 & 8 & 8 \\ 2 & 1 & 1 & 2 & 3 & 3 \end{array} \right),} \end{array}$$

$$\begin{array}{l} {E = \left( \begin{array}{llllllllll} 1 & 3 & 2 & 5 & 6 & 7 & 1 & 8 & 5 & 8 \\ 2 & 4 & 5 & 6 & 7 & 4 & 8 & 7 & 8 & 3 \\ 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 \\ 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 \\ 1 & 2 & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 \\ 2 & 0 & 2 & 3 & 3 & 1 & 0 & 1 & 2 & 0 \\ 0 & 1 & 0 & 0 & 0 & 0 & 2 & 3 & 3 & 1 \end{array} \right).} \end{array}$$

A reader is encouraged to examine matching entries of these matrices to the mesh element labels in [figure 4.4](#chapter4.xhtml_fig4_4).

## 4.3 COMPLEMENTARY MESH

Representation of the mesh through matrices (*P*, *T*, *E*) suffices for the FEM algorithms; however, sometimes the information stored in these matrices is not enough to answer the following questions:

1.  Which elements contain a given mesh point (node)?

2.  Which elements share the common edge?

3.  If the element’s edge is a boundary one?

To answer these question matrices (*P*, *T*, *E*) should be extended by including additional information.

*Let us consider 1^(*s**t*) question*. Connectivity matrix *T* can be considered as a compact representation of the extended Boolean matrix *T*[*e**x**t*] ∼ (*n*[*p*] × *n*[*t*]). Each *j*^(*t**h*) column of the matrix *T*[*e**x**t*] has three nonzero (unity) elements located at positions *T*[1, *j*], *T*[2, *j*] and *T*[3, *j*]. It is not difficult to see that *i*^(*t**h*) row of the matrix *T*[*e**x**t*] has unity on the positions corresponding to the elements having node *i* as a vertex. Consequently, if we obtain a sparse representation of the matrix *T*[*e**x**t*] (which can be done by introducing vectors of indices *i*[*t*] and *p*[*t*]) then we are able to resolve 1^(*s**t*) question. This logic is coded through MATLAB function in [listing 4.2](#chapter4.xhtml_list4_2) which returns sparse format of extended transposed connectivity matrix.

![](images/comp04_2.jpg)

Matrix *T*[*e**x**t*] for the mesh given in [figure 4.4](#chapter4.xhtml_fig4_4) takes the form

$$\begin{array}{l} {T_{ext} = \left( \begin{array}{llllll} 1 & 0 & 0 & 0 & 0 & 0 \\ 1 & 0 & 0 & 1 & 0 & 0 \\ 0 & 1 & 0 & 0 & 0 & 0 \\ 0 & 1 & 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 1 & 1 & 0 \\ 0 & 0 & 0 & 0 & 1 & 1 \\ 0 & 0 & 1 & 0 & 0 & 1 \\ 1 & 1 & 1 & 1 & 1 & 1 \end{array} \right),} \end{array}$$

and the following piece of code

![](images/comp04_3.jpg)

results in displaying mesh point index and corresponding triangles having this point as a vertex.

![](images/comp04_4.jpg)

It can be seen that *i*^(*t**h*) mesh node is the vertex of triangles with indices it(pt(i):pt(i+1)-1).

*Resolving 2^(*n**d*) and 3^(*r**d*) questions*. Let us introduce two complementary matrices *E*^(*c*) and *T*^(*c*) as follows:

*   Matrix *E*^(*c*) ∼ (7 × *n*[*k*]) contains information not only about element’s edges belonging to boundary segments (like matrix *E*), but information about edges of all elements. Here, *n*[*k*] is the number of edges of all finite elements. Components *E*[1, *k*]^(*c*) and *E*[2, *k*]^(*c*) are the indices of mesh points belonging to *k*^(*t**h*) edge, *E*[3, *k*]^(*c*) and *E*[4, *k*]^(*c*) are the values of parameter *s* for the *k*^(*t**h*) edge provided it belongs to boundary segments and *E*[3, *k*]^(*c*) = *E*[4, *k*]^(*c*) = 0 otherwise, *E*[5, *k*]^(*c*) is the segment index, or *E*[5, *k*]^(*c*) = 0 if the *k*^(*t**h*) edge does not belong to a boundary segment, *E*[6, *k*]^(*c*) and *E*[7, *k*]^(*c*) are the indices of triangles (elements) from left and right hand sides of the *k*^(*t**h*) edge.

*   Matrix *T*^(*c*) ∼ (4 × *n*[*t*]) contains information regarding indices of edges and subdomain labels. Components *T*[1, *j*]^(*c*), *T*[2, *j*]^(*c*) and *T*[3, *j*]^(*c*) are the indices of edges of the *j*^(*t**h*) element, *T*[4, *j*]^(*c*) is the subdomain label to which the *j*^(*t**h*) element belongs.

Three matrices (*P*, *T*^(*c*), *E*^(*c*)) are complementary to (*P*, *T*, *E*) and contain full information regarding the mesh (we further call them complementary 𝒢[1] mesh). Complementary 𝒢[1] mesh is convenient when elements are treated independently. Following MATLAB function complMeshG1() calculates matrices *E*^(*c*) and *T*^(*c*)

![](images/comp04_5.jpg)![](images/comp04_5_2.jpg)

Complementary matrices and extended connectivity matrix considered here give more flexibility in manipulating mesh and allow extracting more rich information regarding mesh elements which could be helpful for building refined FEM algorithms.

## 4.4 BUILDING MESHES IN MATLAB^®

Building triangulation in MATLAB for the two-dimensional domain Ω can be performed using function initmesh() which is part of the pde toolbox extension of the MATLAB. For example,

![](images/comp04_6.jpg)

Here, function initmesh() builds a mesh defined in the geometry file ’geometry’ and command pdemesh() plots the resulting mesh. Parameter ’Hmax’ defines the maximum edge value of the mesh triangles. Function initmesh() returns mesh representation in terms of points, edges and connectivity matrices, (p,e,t), described above.

There are two possibilities to define a geometry for the function initmesh():

*   using custom-build function;

*   using a matrix (when all segments are lines or ellipse segments).

In order a custom-build function defining geometry to be passed to the function initmesh() as a parameter, it should have option to return specific values depending on provided arguments. The function geometryFunction() for geometry encoding discussed in [section 4.1](#chapter4.xhtml_sec4_1) (see [listing 4.1](#chapter4.xhtml_list4_1)) can be passed to the function initmesh() as an argument and it meets interface requirements to be processed as a function argument. For instance, following script generates and plots the mesh shown in [figure 4.3](#chapter4.xhtml_fig4_3) where the geometry is defined by geometryFunction()

![](images/comp04_7.jpg)

Another option of geometry definition which can be used by initmesh() function is a matrix where each row must have specific meaning. As an illustration, the geometry shown in [figure 4.2](#chapter4.xhtml_fig4_2) can be encoded through the following matrix definition

![](images/comp04_8.jpg)

The matrix in [listing 4.4](#chapter4.xhtml_list4_4) contains 15 columns (number of segments) and each column defines one segment. First element in the column defines type of the segment (2 is a straight line, 4 is an ellipse); 2^(*t**h*) and 3^(*t**h*) (4^(*t**h*) and 5^(*t**h*)) elements define *x*[1] (*x*[2]) coordinates of starting points and endpoints, respectively; 6^(*t**h*) and 7^(*t**h*) elements specify labels of left and right subdomains. Elements from 8 to 12 are for ellipse specification and can be omitted for straight lines. Elements 8 and 9 define *x*[1] and *x*[2] coordinates of the ellipse centre; elements 10 and 11 are ellipse’s semi-axes; 12^(*t**h*) element specifies ellipse’s rotation angle (anticlockwise in radian).[¹](#chapter4.xhtml_fn4_1) Following piece of code builds the example mesh shown in [figure 4.3](#chapter4.xhtml_fig4_3) using geometryMatrix geometry definition.

![](images/comp04_9.jpg)

For better mesh visualization, it is sometimes helpful to display not only mesh as a set of triangles, but labels for individual triangle vertices and edges as well. This would improve mesh illustration and facilitate debugging process for matrix encoding, (p,e,t). [Listing 4.5](#chapter4.xhtml_list4_5) introduces a function plotG1mesh() which uses matrices p, e and t to plot labelled triangulation. Function plotG1mesh() has the following parameters: p,e,t are the matrices defining the mesh, opt is a Boolean vector for option specification (opt(1)==1 – outputs point labels, opt(2)==1 – outputs boundary edge labels, opt(3)==1 – outputs triangle labels), and fs is a font size.

![](images/comp04_10.jpg)

The L-shaped labelled geometry shown in [figure 4.4](#chapter4.xhtml_fig4_4) is generated through the script

![](images/comp04_11.jpg)

File lshapeg.m for this geometry is provided in the MATLAB pde toolbox (parameter inf indicates building rough mesh). [Figure 4.4](#chapter4.xhtml_fig4_4) shows triangulation with given labels of triangles, edges and vertices and function plotG1mesh() plots this triangulation.

Similarly, complementary mesh discussed in [section 4.3](#chapter4.xhtml_sec4_3) can also be labelled with corresponding indices using following script

![](images/comp04_12.jpg)

where the function plotComplMeshG1() plots complementary mesh and has a form given in [listing 4.6](#chapter4.xhtml_list4_6)

![](images/comp04_13.jpg)

As a result, we obtain [figure 4.5](#chapter4.xhtml_fig4_5) with given indices for mesh points, triangle elements and edges. Boundary edges are marked with two numbers: index of the edge and index of the boundary segment.

![An image shows geometry domain with the same structure as shown in figure 4.4 but it has more additional labels.](images/fig4_5.jpg)

[Figure 4.5:](#chapter4.xhtml_b4fig4_5) Complementary mesh.

## 4.5 BUILDING MESHES IN PYTHON

Above, we have considered how to define a domain geometry and build a mesh using MATLAB tools. Now, we explain how to perform mesh building in Python. Again, the approach is to use third-party library for mesh processing rather than discussing particular mesh building algorithm. There is a powerful mesh generation tool, named Gmsh, having its own scripting language allowing creating complex geometries. The library PyGmsh provides a Python interface for the Gmsh scripting language so one can create geometry and generate meshes more easily with excess to Python’s features. After installing PyGmsh, the default Gmsh kernel with basic geometry construction functions can be used.

Module PyGmsh has a class Geometry to represent a geometry in the following way: first, it is to be defined points (using the method add_point), then lines (using add_line, add_circle,add_circle_arc, add_line_loop, etc.), and finally surfaces (using add_plane_surface method). These geometrical entities are assigned identification numbers when they are created. Groups of geometrical entities can be defined (using add_physical_line or add_physical_surface methods) and are called physical entities with unique identification numbers. The purpose of these physical entities is to assemble geometrical entities into larger groups so that they can be referred to by the mesh module as single entities. In terms of domain geometry definitions, physical entities can be viewed as labelled boundaries or subdomains on which boundary conditions or coefficients are defined. As an example, script in [listing 4.7](#chapter4.xhtml_list4_7) defines geometry illustrated in [figures 4.2](#chapter4.xhtml_fig4_2) and [4.3](#chapter4.xhtml_fig4_3). Function geometry() has a parameter h – mesh triangular size, and returns two structures: geometry object, geom, and labels of geometry elements, geom_labels.

![](images/comp04_14.jpg)![](images/comp04_14_2.jpg)![](images/comp04_14_3.jpg)

Let us make some comments regarding defining labels for the geometry elements. Subdomains are labelled by numbers, but for labelling a boundary (see lines 65 –94) we use group of colon-separated three labels: a number, letter L with a number and letter R with a number. Here, first number is the boundary label and subsequent numbers are subdomain labels from left (letter L) and right (letter R) hand sides of the boundary. These labels are assigned to physical groups of the geometry and kept in the dictionary geom_labels which maps identification number of each physical group to the specified label. Group identification numbers are generated automatically and kept in the list _TAKEN_PHYSICALGROUP_IDS of the class Geometry.

The next step is to generate a mesh and retrieve triangulation data for p,t,e matrices (see [section 4.2](#chapter4.xhtml_sec4_2) for detailed explanation of data structure p,t,e). Function generateMesh() in [listing 4.8](#chapter4.xhtml_list4_8) creates matrices of point coordinates, p, connectivity, t and edges e which have same structure as described in [section 4.2](#chapter4.xhtml_sec4_2). It has two parameters: geom – geometry object defining geometry structure, and geom_labels – a structure containing labels for geometry elements (these structures are created by geometry() function), and returns matrices (p,t,e).

![](images/comp04_15.jpg)

It is worth noting that as we will see later, elements of the edge matrix, e, corresponding to geometry parameter values generated by the MATLAB initmesh() function are not in use in FEM framework, as such, to be consistent, in [listing 4.8](#chapter4.xhtml_list4_8), we keep the same number of rows in matrix e but not filling those for parameter values of edges.

As a result, the mesh illustrated in [figure 4.3](#chapter4.xhtml_fig4_3) can be generated through running the script

![](images/comp04_16.jpg)

# Chapter 5 Programming Two-Dimensional Finite Element Method

DOI: [10.1201/9781003265979-5](https://doi.org/10.1201/9781003265979-5)

IN this chapter we will consider five different methods of assembling global stiffness matrix and global force vector with evaluation of computational cost, efficiency and performance of each method in details. First, we will be focussed on matrices assembling technique, not on calculating matrices elements, and assuming generic local stiffness matrix to be a unity matrix. Further, we will consider methods for calculating elements of local stiffness matrices and local forcing vectors. Also, it will be shown how to incorporate boundary conditions into FEM. Description given in this chapter will involve some mathematical analysis which is important to understand computational techniques. Numerical methods for calculating integrals, function transformations and operating with basis functions will be used to deduce algorithms for calculating local FEM matrices.

## 5.1 ASSEMBLING GLOBAL STIFFNESS MATRIX

Let us consider assembling global stiffness matrix for 𝒢[1] triangular mesh corresponding to a square domain. Triangulation is represented in terms of matrices (p,e,t). It is important to mention that t(1:3,it) stores global node indices for the element having index it. Local stiffness matrices could be assembled into the global one through the following five methods.

1^(*s**t*) *algorithm (inefficient)*. This algorithm is based on the definition of global stiffness matrix and assembles the stiffness matrix element by element, but it is computationally inefficient and not recommended for practical use in MATLAB.

![](images/comp05_1.jpg)

2^(*n**d*) *algorithm (partly optimized)*. This is a vectorized version of the previous algorithm and it is suitable for meshes with small number of elements.

![](images/comp05_2.jpg)

3^(*d*) *algorithm (optimized)*. This algorithm is based on assembling the stiffness matrix in the coordinate form.

![](images/comp05_3.jpg)

Some comments are to be mentioned here. For any matrix B, indexing like B(:) transforms the matrix into a column of the length numel(B). Element Al(i,j) should be added to the corresponding positions of matrix A. As such, instructions i(m)=il(:); j(m)=jl(:); v(m)=Al(:) transform matrices il, jl and Al into columns and assign them to the corresponding elements of the vectors i, j and v.

4^(*t**h*) *algorithm (most efficient)*. This algorithm is based on fully vectorized form of assembling global stiffness matrix

![](images/comp05_4.jpg)

Function stiffnessAssemb_4() is loop free and operates only with vectors. For the symmetric matrix A the algorithm could be more memory efficient (in this case some of aij can be replaced by a single vector and A=A+A.’). We can avoid vectorization of the local stiffness matrices in function stiffnessAssemb_4() and save some memory. For example, the following version of assembling algorithm is comparable in terms of computational cost with the previous one

![](images/comp05_5.jpg)

Let us compare computational efficiency of all assembling algorithms with the help of the function testAssembStiffness() in [listing 5.6](#chapter5.xhtml_list5_6).

![](images/comp05_6.jpg)

[Table 5.1](#chapter5.xhtml_tbl5_1) summarizes results of the computational efficiency test. We can conclude that the CPU time for the first and second versions of the function stiffnessAssemb() is proportional to the square of nodes number while CPU time for the third, fourth and fifth versions of the assembling algorithm are practically proportion to the number of mesh nodes. Algorithms of ver_4 and ver_5 are faster than ver_3 since they do not contain loops. As a result, it is recommended to use vectorized form of the global matrix assembling algorithm.

[Table 5.1:](#chapter5.xhtml_b5tbl5_1) Summary of the computational efficiency test. Last five columns contain CPU time for corresponding version of the stiffness matrix assembling algorithm.

| np | nt | ver_1 | ver_2 | ver_3 | ver_4 | ver_5 |
| --- | --- | --- | --- | --- | --- | --- |
| 121 | 200 | 0.04883 | 0.00586 | 0.05566 | 0.0 | 0.0 |
| 2601 | 5000 | 1.85449 | 0.66308 | 1.36817 | 0.00293 | 0.00293 |
| 10201 | 20000 | 17.21289 | 8.50488 | 5.65820 | 0.01270 | 0.01367 |

For arbitrary finite elements (not necessarily triangle) we recommend using generic function shown in [listing 5.7](#chapter5.xhtml_list5_7) for assembling global stiffness matrix (provided there is a function calcLocalStiffness() to compute a local stiffness matrix). Here, p is a matrix of points, t is a matrix of elements, and ntep is a number of element’s points.

![](images/comp05_7.jpg)

## 5.2 ASSEMBLING GLOBAL FORCING VECTOR

Assembling global forcing vector, *F*, is performed in a similar to global stiffness matrix way. Three methods of assembling could be used depending on the possibility to vectorize calculations. Functions below implement these methods.

![](images/comp05_8.jpg)![](images/comp05_9.jpg)![](images/comp05_10.jpg)

To test performance let us run the following script

![](images/comp05_11.jpg)

which results in [table 5.2](#chapter5.xhtml_tbl5_2). It follows from [table 5.2](#chapter5.xhtml_tbl5_2) that computational cost for the third method five times higher compared with first or second method.

[Table 5.2:](#chapter5.xhtml_b5tbl5_2) Summary of the computational efficiency test for the algorithm of assembling global forcing vector. Last three columns contain CPU time for the corresponding version of the algorithm.

| np | nt | ver_1 | ver_2 | ver_3 |
| --- | --- | --- | --- | --- |
| 121 | 200 | 0.0 | 0.00098 | 0.00879 |
| 2601 | 5000 | 0.00098 | 0.00098 | 0.13281 |
| 10201 | 20000 | 0.00293 | 0.00195 | 0.52637 |

## 5.3 CALCULATING LOCAL STIFFNESS MATRICES

Let us consider calculating local stiffness matrix corresponding to a triangular element *τ* (here we drop the index *l* implying that *τ* could be any element from *τ*[*l*] defined above). Components of the local matrix ${\overline{A}}_{\alpha\beta}$ with indices *α*, *β* = 1, 2, 3 are defined as

$$\begin{array}{l} {{\overline{A}}_{\alpha\beta} = {\int\limits_{\tau}{\left( {c\nabla\varphi_{i_{\beta}} \cdot \nabla\varphi_{i_{\alpha}} + \mathbf{\mathbf{b}} \cdot \nabla\varphi_{i_{\beta}}\varphi_{i_{\alpha}} + a\varphi_{i_{\beta}}\varphi_{i_{\alpha}}} \right)d\mathbf{\mathbf{x}}}}.} \end{array}$$(5.1)

Here, *i*[1], *i*[2] and *i*[3] are the vertices indices of the element *τ*, and *φ*[*i*[1]], *φ*[*i*[2]] and *φ*[*i*[3]] are the corresponding basis functions (note that (*i*[1], *i*[2], *i*[3]) is a column of matrix t). [Figure 5.1](#chapter5.xhtml_fig5_1) shows the element *τ* with notation. To compute integral (5.1) we need expressions for the basis functions and their gradients along with numerical method for integral calculation.

![An image shows two triangles in three-dimensional space having one common side and placed one above the other. Vertices not belonging to the common side are connected with line so that it forms a perpendicular to the bottom triangle.](images/fig5_1.jpg)

[Figure 5.1:](#chapter5.xhtml_b5fig5_1) Triangular element *τ* and basis function *φ*[*i*[1]].

We consider two possible methods of calculating integral (5.1). First method is based on the assumption that coefficients *c*(**x**), *b*(**x**) and *a*(**x**) are constant over the element *τ* and equal to the values computed at the element’s centre of mass, **p**[*τ*] = (**p**[*i*[1]] + **p**[*i*[2]] + **p**[*i*[3]])/3. In this case the integral is computed analytically (provided expressions for the basis functions are known) through the formula

$$\begin{array}{l} {{\overline{A}}_{\alpha\beta} = {\int\limits_{\tau}{\left( {c(\mathbf{\mathbf{p}}_{\tau})\nabla\varphi_{i_{\beta}} \cdot \nabla\varphi_{i_{\alpha}} + \mathbf{\mathbf{b}}(\mathbf{\mathbf{p}}_{\tau}) \cdot \nabla\varphi_{i_{\beta}}\varphi_{i_{\alpha}} + a(\mathbf{\mathbf{p}}_{\tau})\varphi_{i_{\beta}}\varphi_{i_{\alpha}}} \right)d\mathbf{\mathbf{x}}}}.} \end{array}$$(5.2)

Second method makes use of the quadrature formula with one node which is faithful representation for linear polynomial integrand

$$\begin{array}{l} \left. {\overline{A}}_{\alpha\beta} = \middle| \tau \middle| \left( {c\nabla\varphi_{i_{\beta}} \cdot \nabla\varphi_{i_{\alpha}} + \mathbf{\mathbf{b}} \cdot \nabla\varphi_{i_{\beta}}\varphi_{i_{\alpha}} + a\varphi_{i_{\beta}}\varphi_{i_{\alpha}}} \right)(\mathbf{\mathbf{p}}_{\tau}), \right. \end{array}$$(5.3)

where |*τ*| is the area of the element *τ*.

Next, we consider representation of the basis functions on the element *τ*. To obtain expressions for the basis functions we use an approach which is equally applicable to any type of triangular elements with straight line edges (for example, triangular elements with six nodes or 𝒢[2] elements). The main idea is to consider a canonical element *τ̂* in the coordinate system $\hat{\mathbf{\mathbf{x}}} = ({\hat{x}}_{1},{\hat{x}}_{2})$ on which basis functions take simple known form. Then the basis functions for the element *τ* are derived through coordinate transformation. To illustrate this approach, let us consider two elements shown in [figure 5.2](#chapter5.xhtml_fig5_2), where the canonical element has vertices coordinates $\hat{\mathbf{\mathbf{p}}_{1}} = (0,0),\,\hat{\mathbf{\mathbf{p}}_{2}} = (1,0),\,\hat{\mathbf{\mathbf{p}}_{3}} = (0,1)$ and an arbitrary three-nodes element *τ* has vertices **p**[1], **p**[2] and **p**[3]. In this case, the following functions

$$\begin{array}{l} {{\hat{\varphi}}_{1}(\hat{\mathbf{\mathbf{x}}}) = 1 - {\hat{x}}_{1} - {\hat{x}}_{2},\quad{\hat{\varphi}}_{2}(\hat{\mathbf{\mathbf{x}}}) = {\hat{x}}_{1},\quad{\hat{\varphi}}_{3}(\hat{\mathbf{\mathbf{x}}}) = {\hat{x}}_{2}} \end{array}$$

![An image shows two triangles, one on the left which is a canonical triangle and one on the right-hand side of the image center. Canonical triangle is an equilateral right triangle and from the right-hand side is an ordinary triangle without any specific property.](images/fig5_2.jpg)

[Figure 5.2:](#chapter5.xhtml_b5fig5_2) Canonical element *τ̂* and original 𝒢[1] mesh element *τ*.

represent basis functions on element *τ̂*, and it is clear that ${\hat{\varphi}}_{i}(\hat{\mathbf{\mathbf{p}}_{j}}) = \delta_{ij}$. Transformation from *τ̂* to *τ* is given by

$$\begin{array}{l} {\mathbf{\mathbf{x}} = \mathbf{\mathbf{p}}_{1}{\hat{\varphi}}_{1} + \mathbf{\mathbf{p}}_{2}{\hat{\varphi}}_{1} + \mathbf{\mathbf{p}}_{3}{\hat{\varphi}}_{1} = \mathbf{\mathbf{p}}_{1} + {\hat{x}}_{1}(\mathbf{\mathbf{p}}_{2} - \mathbf{\mathbf{p}}_{1}) + {\hat{x}}_{2}(\mathbf{\mathbf{p}}_{3} - \mathbf{\mathbf{p}}_{1}).} \end{array}$$(5.4)

Indeed, this is an affine transformation which maps vertices of *τ̂* to the vertices of *τ* with preserving orientation of the canonical element and (0, 0) → **p**[1], (1, 0) → **p**[2], (0, 1) → **p**[3]. After introducing notation

$$\begin{array}{l} {B_{\tau} = \left( \begin{array}{ll} {(\mathbf{\mathbf{p}}_{2} - \mathbf{\mathbf{p}}_{1})}_{1} & {(\mathbf{\mathbf{p}}_{3} - \mathbf{\mathbf{p}}_{1})}_{1} \\ {(\mathbf{\mathbf{p}}_{2} - \mathbf{\mathbf{p}}_{1})}_{2} & {(\mathbf{\mathbf{p}}_{3} - \mathbf{\mathbf{p}}_{1})}_{2} \end{array} \right),} \end{array}$$(5.5)

transformation can be rewritten in matrix form

$$\begin{array}{l} \left. \mathbf{\mathbf{x}} = B_{\tau}\hat{\mathbf{\mathbf{x}}} + \mathbf{\mathbf{p}}_{1}\quad:\quad\hat{\tau}\rightarrow\tau \right. \end{array}$$(5.6)

with Jacobian determinant *J*[*τ*] = det *B*[*τ*] > 0. As a result, the area of element *τ* is defined as

$$\begin{array}{l} \left| \tau \middle| = {\int\limits_{\tau}{d\mathbf{\mathbf{x}}}} = {\int\limits_{\tau}{\det B_{\tau}d\hat{\mathbf{\mathbf{x}}}}} = \middle| \hat{\tau} \middle| \det B_{\tau} = \frac{1}{2}J_{\tau}. \right. \end{array}$$

Inverse transformation has a form of $\hat{\mathbf{\mathbf{x}}} = B_{\tau}^{- 1}(\mathbf{\mathbf{x}} - \mathbf{\mathbf{p}}_{1})$ with

$$\begin{array}{l} {B_{\tau}^{- 1} = \frac{1}{\det B_{\tau}}\left( \begin{array}{ll} {(\mathbf{\mathbf{p}}_{3} - \mathbf{\mathbf{p}}_{1})}_{2} & {- {(\mathbf{\mathbf{p}}_{3} - \mathbf{\mathbf{p}}_{1})}_{1}} \\ {- {(\mathbf{\mathbf{p}}_{2} - \mathbf{\mathbf{p}}_{1})}_{2}} & {(\mathbf{\mathbf{p}}_{2} - \mathbf{\mathbf{p}}_{1})}_{1} \end{array} \right) = \left( \begin{array}{ll} \widetilde{d} & {- \widetilde{b}} \\ {- \widetilde{c}} & \widetilde{a} \end{array} \right).} \end{array}$$

Consequently,

$$\begin{array}{ll} {\hat{x}}_{1} & {= \widetilde{d}\left( {x_{1} - {(\mathbf{\mathbf{p}}_{1})}_{1}} \right) - \widetilde{b}\left( {x_{2} - {(\mathbf{\mathbf{p}}_{1})}_{2}} \right),} \\ {\hat{x}}_{2} & {= - \widetilde{c}\left( {x_{1} - {(\mathbf{\mathbf{p}}_{1})}_{1}} \right) + \widetilde{a}\left( {x_{2} - {(\mathbf{\mathbf{p}}_{1})}_{2}} \right).} \end{array}$$

Basis functions *φ*[*i*](**x**) on the element *τ* are obtained from the basis functions on the element *τ̂* through the transformation *φ*[*i*](**x**) = *φ̂*[*i*](*B*[*τ*]^(−1)(**x** − **p**[1])). As a result,

$$\begin{array}{ll} {\varphi_{1}(\mathbf{\mathbf{x}})} & {= 1 - \varphi_{2}(\mathbf{\mathbf{x}}) - \varphi_{3}(\mathbf{\mathbf{x}}),} \\ {\varphi_{2}(\mathbf{\mathbf{x}})} & {= \widetilde{d}\left( {x_{1} - {(\mathbf{\mathbf{p}}_{1})}_{1}} \right) - \widetilde{b}\left( {x_{2} - {(\mathbf{\mathbf{p}}_{1})}_{2}} \right),} \\ {\varphi_{3}(\mathbf{\mathbf{x}})} & {= - \widetilde{c}\left( {x_{1} - {(\mathbf{\mathbf{p}}_{1})}_{1}} \right) + \widetilde{a}\left( {x_{2} - {(\mathbf{\mathbf{p}}_{1})}_{2}} \right).} \end{array}$$

Respectively, gradients of the basis functions have the form

$$\begin{array}{l} {\nabla\varphi_{1} = \left( \begin{array}{l} {\widetilde{c} - \widetilde{d}} \\ {\widetilde{b} - \widetilde{a}} \end{array} \right),\quad\nabla\varphi_{2} = \left( \begin{array}{l} \widetilde{d} \\ {- \widetilde{b}} \end{array} \right),\quad\nabla\varphi_{3} = \left( \begin{array}{l} {- \widetilde{c}} \\ \widetilde{a} \end{array} \right).} \end{array}$$

It is worth noting that *φ*[*i*](**p**[*τ*]) = 1/3, *i* = 1, 2, 3, and for gradients we have

$$\begin{array}{l} {\nabla\varphi_{i}(\mathbf{\mathbf{x}}) = B_{\tau}^{- 1}{}^{T}\hat{\nabla}\hat{\varphi_{i}}(\hat{\mathbf{\mathbf{x}}}).} \end{array}$$

Also, the following expressions are valid for the elements *τ* of any type

$$\begin{array}{l} {{\sum\limits_{i = 1}^{m_{\tau}}{\varphi_{i}(\mathbf{\mathbf{x}})}} = 1,\quad{\sum\limits_{i = 1}^{m_{\tau}}{\nabla\varphi_{i}(\mathbf{\mathbf{x}})}} = {(0,0)}^{T},\quad\mathbf{\mathbf{x}} \in \tau,} \end{array}$$

where *m*[*τ*] is the number of interpolation nodes belonging to the element *τ*.

By this point, we have obtained all expressions to calculate elements of the local stiffness matrix. Now, let us consider methods for calculation of the integral (5.1) mentioned above. Since the basis *φ*[*i*[*α*]] are linear functions, then ∇*φ*[*i*[*α*]] are constants and (5.1) can be rewritten as

$$\begin{array}{ll} {{\overline{A}}_{\alpha\beta} = c(\mathbf{\mathbf{p}}_{\tau})} & {\nabla\varphi_{i_{\beta}} \cdot \nabla\varphi_{i_{\alpha}}{\int\limits_{\tau}{d\mathbf{\mathbf{x}}}} + \mathbf{\mathbf{b}}(\mathbf{\mathbf{p}}_{\tau}) \cdot \nabla\varphi_{i_{\beta}}{\int\limits_{\tau}{\varphi_{i_{\alpha}}d\mathbf{\mathbf{x}}}}} \\ & \left. + a(\mathbf{\mathbf{p}}_{\tau}){\int\limits_{\tau}{\varphi_{i_{\beta}}\varphi_{i_{\alpha}}d\mathbf{\mathbf{x}}}} = \middle| \tau \middle| c(\mathbf{\mathbf{p}}_{\tau})\nabla\varphi_{i_{\beta}} \cdot \nabla\varphi_{i_{\alpha}} \right. \\ & {+ \mathbf{\mathbf{b}}(\mathbf{\mathbf{p}}_{\tau}) \cdot \nabla\varphi_{i_{\beta}}J_{\tau}{\int\limits_{\hat{\tau}}{{\hat{\varphi}}_{i_{\alpha}}d\hat{\mathbf{\mathbf{x}}}}} + a(\mathbf{\mathbf{p}}_{\tau})J_{\tau}{\int\limits_{\hat{\tau}}{{\hat{\varphi}}_{i_{\beta}}{\hat{\varphi}}_{i_{\alpha}}d\hat{\mathbf{\mathbf{x}}}}}.} \end{array}$$(5.7)

First integral on the right hand side of the expression (5.7) being calculated either analytically or numerically using quadrature formula with one node results in the value of 1/6, and we come to the expression

$$\begin{array}{l} \left. {\overline{A}}_{\alpha\beta} = \middle| \tau \middle| \left( {c(\mathbf{\mathbf{p}}_{\tau})\nabla\varphi_{i_{\beta}} \cdot \nabla\varphi_{i_{\alpha}} + \frac{1}{3}\mathbf{\mathbf{b}}(\mathbf{\mathbf{p}}_{\tau}) \cdot \nabla\varphi_{i_{\beta}}} \right) + a(\mathbf{\mathbf{p}}_{\tau})J_{\tau}{\int\limits_{\hat{\tau}}{{\hat{\varphi}}_{i_{\beta}}{\hat{\varphi}}_{i_{\alpha}}d\hat{\mathbf{\mathbf{x}}}}}. \right. \end{array}$$

The last integral results in different answers depending on the applied calculation methods. When using quadrature formula the answer is

$$\begin{array}{l} {{\int\limits_{\hat{\tau}}{{\hat{\varphi}}_{i_{\beta}}{\hat{\varphi}}_{i_{\alpha}}d\hat{\mathbf{\mathbf{x}}}}} = {\hat{\varphi}}_{i_{\beta}}\left( \hat{\mathbf{\mathbf{p}}_{\tau}} \right){\hat{\varphi}}_{i_{\alpha}}\left( \hat{\mathbf{\mathbf{p}}_{\tau}} \right){\int\limits_{\hat{\tau}}{d\hat{\mathbf{\mathbf{x}}}}} = \left( \begin{array}{ll} \frac{1}{18} & \frac{1}{18} \\ \frac{1}{18} & \frac{1}{18} \end{array} \right),} \end{array}$$

but applying analytical integration gives

$$\begin{array}{l} {{\int\limits_{\hat{\tau}}{{\hat{\varphi}}_{i_{\beta}}{\hat{\varphi}}_{i_{\alpha}}d\hat{\mathbf{\mathbf{x}}}}} = \left( \begin{array}{ll} \frac{1}{12} & \frac{1}{24} \\ \frac{1}{24} & \frac{1}{12} \end{array} \right).} \end{array}$$

Next, we consider calculation of the local forcing vector on the element *τ*

$$\begin{array}{l} {{\overline{F}}_{\alpha} = {\int\limits_{\tau}{f(\mathbf{\mathbf{x}})\varphi_{i_{\alpha}}(\mathbf{\mathbf{x}})d\mathbf{\mathbf{x}}}}.} \end{array}$$

Both, analytical integration and quadrature method, lead to the same result, namely

$$\begin{array}{l} {{\overline{F}}_{\alpha} = \frac{1}{6}J_{\tau}f(\mathbf{\mathbf{p}}_{\tau}),\quad\alpha = 1,2,3.} \end{array}$$

Regarding calculation boundary integrals

$$\begin{array}{l} {{\overline{S}}_{\alpha\beta} = {\int\limits_{e}{\sigma(\mathbf{\mathbf{x}})\varphi_{i_{\alpha}}\varphi_{i_{\beta}}d\mathbf{\mathbf{x}}}},\quad{\overline{M}}_{\alpha} = {\int\limits_{e}{\mu(\mathbf{\mathbf{x}})\varphi_{i_{\alpha}}(\mathbf{\mathbf{x}})d\mathbf{\mathbf{x}}}},} \end{array}$$(5.8)

which are associated with the boundary conditions on the edge *e* having the vertex indices *i*[1] and *i*[2], we can apply both approaches mentioned above. For the components of the vector **M** we come to the same expression regardless of the integration method, $\left. {\overline{M}}_{\alpha} = \middle| e \middle| /2\mu(\mathbf{\mathbf{p}}_{e}),\,\alpha = 1,2 \right.$, where |*e*| is the length of the edge *e* and **p**[*e*] is the midpoint of the edge. For the matrix $\overline{S}$ we obtain two results depending on the calculation method. In case of analytical integration we have

$$\begin{array}{l} \left. {\overline{S}}_{\alpha\beta} = \middle| e \middle| \mu(\mathbf{\mathbf{p}}_{e})\left( \begin{array}{ll} \frac{1}{3} & \frac{1}{6} \\ \frac{1}{6} & \frac{1}{3} \end{array} \right). \right. \end{array}$$

Integration using quadrature formula gives $\left. {\overline{S}}_{\alpha\beta} = ( \middle| e \middle| /4)\mu(\mathbf{\mathbf{p}}_{e}) \right.$, where the fact *φ*[*i*[*α*]](**p**[*e*]) = 1/2 is taken into account.

## 5.4 CALCULATING EQUATION COEFFICIENTS

Stiffness matrices depend on the coefficients of the partial differential equation (*c*, **b**, *a*, *f*) and we need to decide how to incorporate calculation of these coefficients into FEM. Note that the equation coefficients could be piecewise functions on subdomains. Recall that the domain Ω where the solution is sought could consist of subdomains. Each subdomain is supposed to have unique label, sdl, and this label can be retrieved from the connectivity matrix t so that sdl=t(4,:). As such, each element ’knows’ about subdomain to which it belongs. We can construct a function which takes as an input subdomain label sdl and performs calculation of the coefficient, for example, if we have three subdomains *Ω*[1], *Ω*[2], *Ω*[3], and coefficient *c* is defined as

$$\begin{array}{l} {c(\mathbf{\mathbf{p}}) = \left\{ \begin{array}{ll} {1,} & {\mathbf{\mathbf{p}} \in \Omega_{1},} \\ {x_{1}^{2} + x_{2},} & {\mathbf{\mathbf{p}} \in \Omega_{2},} \\ {\sin(x_{1} + x_{2}),} & {\mathbf{\mathbf{p}} \in \Omega_{3},} \end{array}~ \right.} \end{array}$$

then the function in [listing 5.11](#chapter5.xhtml_list5_11) calculates the coefficient *c*.

![](images/comp05_12.jpg)

This function can be called at any time when coefficient values need to be calculated. It is worth noting that this is a vectorized function which allows to calculate coefficients over all subdomain points.

## 5.5 CALCULATING GLOBAL STIFFNESS MATRIX AND FORCING VECTOR

In [section 5.3](#chapter5.xhtml_sec5_3) we obtained expression for calculating local stiffness matrices and local force vectors for the 𝒢[1] mesh. Now, let us incorporate this information into the algorithms provided in [sections 5.1](#chapter5.xhtml_sec5_1) and [5.2](#chapter5.xhtml_sec5_2). We provide two versions of the algorithm: vectorized and non-vectorized. Let us start with non-vectorized version given in [listing 5.12](#chapter5.xhtml_list5_12).

![](images/comp05_13.jpg)![](images/comp05_13_2.jpg)

Analysis of the function assemblingAF_nv() shows that in order to vectorize it we need to avoid using loop and assemble local stiffness matrices on place once they have been calculated. As a result, we come to the vectorized version of the algorithm (see [listing 5.13](#chapter5.xhtml_list5_13)).

![](images/comp05_14.jpg)![](images/comp05_14_2.jpg)

Let us compare computational costs of these two functions. We take a domain having three subdomains with geometry defined by matrix geometryMatrix (see [figure 4.1](#chapter4.xhtml_fig4_1)) and specify coefficients of the PDE as follows:

![](images/comp05_15.jpg)![](images/comp05_16.jpg)![](images/comp05_17.jpg)![](images/comp05_18.jpg)![](images/comp05_19.jpg)

Then, we run the script shown in [listing 5.19](#chapter5.xhtml_list5_19) to measure CPU time for three meshes with different number of nodes.

![](images/comp05_20.jpg)

As a result, we come to [table 5.3](#chapter5.xhtml_tbl5_3) which shows that vectorized version outperforms non-vectorized one, that is predictable due to more efficient memory management of the vectorized calculations in MATLAB.

[Table 5.3:](#chapter5.xhtml_b5tbl5_3) Summary of the computational efficiency test for assembling global stiffness matrix and forcing vector. Last two columns contain CPU time for the corresponding algorithm version.

| np | nt | assemblingAF | assemblingAF_nv |
| --- | --- | --- | --- |
| 704 | 1312 | 0.00391 | 1.08008 |
| 2670 | 5148 | 0.00781 | 3.73047 |
| 16473 | 32466 | 0.05566 | 23.62988 |

Python implementation of the function assemblingAF() can be found in [Appendix E.1](#appE.xhtml_appE) where corresponding explanations are provided.

## 5.6 CALCULATING BOUNDARY CONDITIONS

Below, we describe one of the possible methods of calculating boundary conditions. Later, we make use of this approach to incorporate boundary conditions into final FEM matrix.

Recall that the boundary Γ of the problem domain Ω is supposed to be split into two parts, *Γ*[*D*] and *Γ*[*R*], on which different boundary conditions could be defined (see [section 3.1](#chapter3.xhtml_sec3_1)). Boundary parts *Γ*[*D*] and *Γ*[*R*], in turn, are union of the corresponding boundary segments defined in geometry matrix. We associate each segment with either function *u*[*D*] (for the Dirichlet boundary *Γ*[*D*]) or with pair of functions (*σ*, *μ*) (for the Robin boundary *Γ*[*R*]). Thereby, we define conditions on *Γ*[*D*] and *Γ*[*R*] separately.

Suppose that *Γ*[*D*] is non-empty and consists of the boundary segments with indices (*i*[1], *i*[2], …, *i*[*d*]) and function *u*[*D*] could be different for each segment. We define a function uD(x1,x2,sdl) in the way described in [section 5.4](#chapter5.xhtml_sec5_4). As a result, Dirichlet boundary conditions are defined by the list of boundary segment indices bsD=[i1, i2, %, id ] and by corresponding function (likewise in [section 5.4](#chapter5.xhtml_sec5_4)). Note that we need to bear in mind that sdl parameter in a function has now meaning of the local index. For instance, supposing we have three Dirichlet boundary segments with indices 5, 2 and 7, then bsD = [5 2 7]. If *u*[*D*] = 1 for the fifth and seventh segments, *u*[*D*] = *x*[1] + *x*[2] for the second segment, then we can define the function uD as shown in [listing 5.20](#chapter5.xhtml_list5_20).

![](images/comp05_21.jpg)

If there is no Dirichlet boundary conditions, then bcD=[] and uD=[]; if *Γ*[*D*] = *Γ* then bsD=inf.

Likewise, we define boundary conditions on *Γ*[*R*] through the list of indices bsR and corresponding functions sg and mu for (*σ*, *μ*). In this case, if *σ* = *μ* = 0 then this segment is not indicated in the list; if *Γ*[*R*] = *Γ* then bsR=inf. Finally, if *Γ*[*D*] = ⌀, *Γ*[*R*] = *Γ* and *σ* = *μ* = 0 then bsN=inf, sg=[], mu=[].

For convenience, we pack data (bsD,uD,bsR,sg,mu) into structure bc with corresponding fields.

## 5.7 ASSEMBLING BOUNDARY CONDITIONS

Now, we gather all the necessary data to form the FEM system defined by (3.7)

$$\begin{array}{l} {{\sum\limits_{j \in \mathcal{I}_{U}}{{\widetilde{A}}_{ij}u_{j}}} = q_{i},\quad q_{i} = {\widetilde{F}}_{i} - {\sum\limits_{j \in \mathcal{I}_{D}}{{\widetilde{A}}_{ij}u_{D_{j}}}},\, i \in \mathcal{I}_{U},} \end{array}$$

where the matrix *Ã* = {*Ã*[*i**j*]}[*i*, *j* = 1]^(*n*[*p*]) = *A* + *S*, **F̃** = {*F̃*[*i*]}[*i* = 1]^(*n*[*p*]) = **F** + **M**, ℐ[*D*] are the indices of the points with Dirichlet boundary conditions, and ℐ[*U*] are the rest points.

Function assemblingAF() (see [section 5.5](#chapter5.xhtml_sec5_5)) calculates matrix *A* and vector **F** and we need a similar function to calculate *S* and **M**. In addition, this function would enable us calculating vector **U**[*D*] with *n*[*p*] elements such that all its elements are equal to zero apart from elements with indices *j* ∈ ℐ[*D*] having value of *u*[*D*[*j*]].

Matrix *Ã*[ℐ[*U*]] = {*Ã*}[*i*, *j* ∈ ℐ[*U*]] is obtained from the matrix *Ã* by deleting rows and columns with indices belonging to the set ℐ[*D*]. To perform this operation we introduce a matrix *N* ∼ (*n*[*p*] × *m*) where *m* is the number of elements in the set ℐ[*U*] and

$$\begin{array}{l} {N^{T} \cdot {(u_{1},u_{2},\cdots,u_{n_{p}})}^{T} = {(u_{i_{1}},u_{i_{2}},\cdots,u_{i_{U}})}^{T}.} \end{array}$$

Matrix *N* can be defined as N=sparse([i1,i2,%,in],1:m,1,np,m). Consequently, if *S*, **M**, *N*, and **u**[*D*] are calculated, then matrix *Ã* and vector **q** are defined through the following expressions

$$\begin{array}{l} {{\widetilde{A}}_{\mathcal{I}_{U}} = N^{T}(A + S)N,\quad\mathbf{\mathbf{q}} = N^{T}((\mathbf{\mathbf{F}} + \mathbf{\mathbf{M}}) - (A + S)\mathbf{\mathbf{U}}_{D}).} \end{array}$$

Note that after solving the system *Ã*[ℐ[*U*]]**u** = **q** the final vector of solution at the node points can be obtained as **U** = *N***u** + **U**[*D*] (complementing vector **u** by the boundary values **U**[*D*]). As a result, we come to the function assemblingBC() in [listing 5.21](#chapter5.xhtml_list5_21) which calculates contributions from the boundary elements.

![](images/comp05_22.jpg)![](images/comp05_22_2.jpg)

For clarification, MATLAB function t=ismember(a,b) returns Boolean vector such that t(k)=1 if a(k) ∈ b and t(k)=0 if a(k) ∉ b.

Functions described above allow us forming and solving FEM system. As a final step, we provide a function assemblingPDE() in [listing 5.22](#chapter5.xhtml_list5_22) which assembles a PDE problem and solves it using FEM. Depending on the number of output arguments, it returns either FEM matrices or a final solution vector.

![](images/comp05_23.jpg)

Functions assemblingAF() and assemblingPDE() translated into Python programming language can be found in [Appendix E.2](#appE.xhtml_appE).

## 5.8 SOLVING EXAMPLE PROBLEM

Let us apply function assemblingPDE() to solve an example problem. We consider PDE of the form

$$\begin{array}{l} {- \nabla \cdot \left( {c(\mathbf{\mathbf{x}})\nabla u} \right) + \mathbf{\mathbf{b}}(\mathbf{\mathbf{x}}) \cdot \nabla u + a(\mathbf{\mathbf{x}})u = f(\mathbf{\mathbf{x}}),\quad\mathbf{\mathbf{x}} = (x_{1},x_{2}) \in \Omega,} \end{array}$$

with boundary conditions

$$\begin{array}{ll} & {u(\mathbf{\mathbf{x}}) = u_{D}(\mathbf{\mathbf{x}}),\,\mathbf{\mathbf{x}} \in \Gamma_{D};} \\ & {c(\mathbf{\mathbf{x}})\nabla u \cdot \mathbf{\mathbf{\nu}}(\mathbf{\mathbf{x}}) + \sigma(\mathbf{\mathbf{x}})u = \mu(\mathbf{\mathbf{x}}),\,\mathbf{\mathbf{x}} \in \Gamma_{R},} \end{array}$$

where Ω is a circle of the unity radius. [Figure 5.3](#chapter5.xhtml_fig5_3) shows boundaries of the circle having four segments, where *Γ*[*D*] comprises segments 1 and 3, and *Γ*[*R*] comprises segments 2 and 4.

![An image shows a geometry having shape of circle with unity radius. A boundary of the circle is split into four parts and every part is shown as directed arch with label.](images/fig5_3.jpg)

[Figure 5.3:](#chapter5.xhtml_b5fig5_3) Geometry for the example problem.

We define coefficients

$$\begin{array}{ll} c & {= 2 + x_{1} + x_{2},} \\ a & {= x_{1} + x_{2},} \\ \mathbf{\mathbf{b}} & {= (x_{1},x_{2}),} \\ f & {= - 8 - 6(x_{1} + x_{2}) + (2 + x_{1} + x_{2})(x_{1}^{2} + x_{2}^{2}),} \end{array}$$

and boundary conditions

$$\begin{array}{ll} u_{D} & {= x_{1}^{2} + x_{2}^{2},} \\ \sigma & {= \left\{ \begin{array}{ll} {0,} & {\text{on~}2^{nd}\text{~segment},} \\ {2,} & {\text{on~}4^{th}\text{~segment~},} \end{array}~ \right.} \\ \mu & {= \left\{ \begin{array}{ll} {2(2 + x_{1} + x_{2})u_{D},} & {\text{~on~}2^{nd}\text{~segment},} \\ {2(2 + x_{1} + x_{2} + 1)u_{D},} & {\text{on~}4^{th}\text{~segment}\text{.}} \end{array}~ \right.} \end{array}$$

Boundary conditions *σ* and *μ* can be coded through the functions

![](images/comp05_24.jpg)![](images/comp05_25.jpg)![](images/comp05_26.jpg)

It is easy to see that solution to this problem is given by function *u* = *x*[1]² + *x*[2]². We utilize function assemblingPDE() to solve this problem numerically on the meshes with h = [0.5 0.1 0.05 0.02]. Since the exact solution is known we can find an absolute error

$$\begin{array}{l} \left. err = \max\limits_{x \in \mathcal{T}_{h}} \middle| u(x) - u_{h}(x) \middle| , \right. \end{array}$$

and relative error, *e**r**r*[*h*] = *e**r**r*/*h*². Function testPDE in [listing 5.26](#chapter5.xhtml_list5_26) solves this problem and calculates FEM solution errors.

![](images/comp05_27.jpg)

As a result we obtain [tables 5.4](#chapter5.xhtml_tbl5_4) and [5.5](#chapter5.xhtml_tbl5_5) summarizing testing data.

[Table 5.4:](#chapter5.xhtml_b5tbl5_4) Summary of the solving test problem. Last three columns contain CPU time for the corresponding functions.

| np | assemblingAF | assemblingBC | solving |
| --- | --- | --- | --- |
| 33 | 0.00195 | 0.00586 | 0.00293 |
| 544 | 0.00195 | 0.00195 | 0.00683 |
| 2169 | 0.00586 | 0.00195 | 0.02344 |
| 13525 | 0.05859 | 0.00683 | 0.31348 |

[Table 5.5:](#chapter5.xhtml_b5tbl5_5) Errors when solving the test problem numerically.

| np | 33 | 544 | 2169 | 13525 |
| --- | --- | --- | --- | --- |
| err | 0.07266 | 0.00252 | 0.00093 | 0.00013 |
| errh2 | 0.29066 | 0.25173 | 0.37120 | 0.32498 |

Data for error magnitudes in [table 5.5](#chapter5.xhtml_tbl5_5) indicate that the problem has been solved successfully. Absolute error decreases with mesh resolution refining while relative error remains stable with slight fluctuation.

Python version of the code for solving example problem can be found in [Appendix E.3](#appE.xhtml_appE).

# Chapter 6 Nonlinear Basis Functions

DOI: [10.1201/9781003265979-6](https://doi.org/10.1201/9781003265979-6)

HERE we consider 𝒢[2] mesh and obtain expressions for calculation of basis functions for mesh triangular elements with straight as well as curvilinear edges. Analysis of how to deduce expression for calculating elements of stiffness matrix is given here. We provide mathematical formulations and expressions without giving MATLAB implementations codes. Based on the content of this chapter, coding functions can be easily composed. Basically, we outline techniques to extend existing FEM framework for 𝒢[1] mesh to FEM with 𝒢[2] mesh.

## 6.1 QUADRATIC BASIS FUNCTIONS FOR LINEAR TRIANGULAR ELEMENTS

Methodology to obtain basis functions for the 𝒢[2] triangles with straight edges is similar to one of 𝒢[1] meshes with the difference in number of interpolation nodes.

Let us consider a canonical triangle element *τ̂* in the coordinate system $\hat{\mathbf{\mathbf{x}}} = ({\hat{x}}_{1},{\hat{x}}_{2})$ having six interpolation nodes $\hat{\mathbf{\mathbf{p}}_{i}},\, i = 1,\ldots,6$ (here $\hat{\mathbf{\mathbf{p}}_{4}},\hat{\mathbf{\mathbf{p}}_{5}}$, and $\hat{\mathbf{\mathbf{p}}_{6}}$ are midpoints). Then 𝒢[2] are all polynomials of the second order on the element *τ̂* (see [figure 6.1](#chapter6.xhtml_fig6_1) with original triangle element and corresponding basis element).

![An image shows two triangles of the same form as shown in figure 5.2 but with additional midpoint for every triangle side.](images/fig6_1.jpg)

[Figure 6.1:](#chapter6.xhtml_b6fig6_1) Canonical element *τ̂* and original 𝒢[2] mesh element *τ*.

If *x̂*[3] = 1 − *x̂*[1] − *x̂*[2], then basis in ${\hat{\mathcal{G}}}_{2}$ is defined by the following functions

$$\begin{array}{ll} {\hat{\varphi}}_{1} & {= {\hat{x}}_{3}(2{\hat{x}}_{3} - 1),\quad{\hat{\varphi}}_{2} = {\hat{x}}_{1}(2{\hat{x}}_{1} - 1),\quad{\hat{\varphi}}_{3} = {\hat{x}}_{2}\left( {2{\hat{x}}_{2} - \frac{1}{2}} \right),} \\ {\hat{\varphi}}_{4} & {= 4{\hat{x}}_{1}{\hat{x}}_{3},\quad{\hat{\varphi}}_{5} = 4{\hat{x}}_{1}{\hat{x}}_{2},\quad{\hat{\varphi}}_{6} = 4{\hat{x}}_{2}{\hat{x}}_{3},} \end{array}$$(6.1)

and for arbitrary function $\hat{z} \in {\hat{\mathcal{G}}}_{2}$ is valid

$$\begin{array}{l} {\hat{z}(\hat{\mathbf{\mathbf{x}}}) = {\sum\limits_{i = 1}^{6}{\hat{z}(\hat{\mathbf{\mathbf{p}}_{i}}){\hat{\varphi}}_{i}(\hat{\mathbf{\mathbf{x}}})}},\quad\hat{\mathbf{\mathbf{x}}} \in \hat{\tau}.} \end{array}$$

Coordinate transformation *τ̂* → *τ* is defined by (see (5.4) – (5.6))

$$\begin{array}{l} {\mathbf{\mathbf{x}} = B_{\tau}\hat{\mathbf{\mathbf{x}}} + \mathbf{\mathbf{p}}_{1},} \end{array}$$(6.2)

and, in addition, points $\hat{\mathbf{\mathbf{p}}_{i}}$ are transformed into points **p**[*i*], *i* = 1, …, 6. Inverse transformation is defined by $\hat{\mathbf{\mathbf{x}}} = B_{\tau}^{- 1}(\mathbf{\mathbf{x}} - \mathbf{\mathbf{p}}_{1})$ and functions *φ*[*i*](**x**) = *φ̂*[*i*](*B*[*τ*]^(−1)(**x** − **p**[1])) represent a basis in 𝒢[2]. As a result, $\hat{z}(\hat{\mathbf{\mathbf{x}}})$ transforms into *z*(**x**) such that

$$\begin{array}{l} {z(\mathbf{\mathbf{x}}) = {\sum\limits_{i = 1}^{6}{z(\mathbf{\mathbf{p}}_{i})\varphi_{i}(\mathbf{\mathbf{x}})}},\quad\mathbf{\mathbf{x}} \in \tau.} \end{array}$$(6.3)

It is worth noting here that unlike 𝒢[1] mesh, basis functions for 𝒢[2] mesh are nonlinear functions, namely, of the second order. This fact results in slightly more complicated calculations of its gradients.

## 6.2 QUADRATIC BASIS FUNCTIONS FOR CURVILINEAR TRIANGULAR ELEMENTS

Usually, curvilinear elements are used as mesh elements adjoining the boundary to approximate curvilinear geometry in most precise way. [Figure 6.2](#chapter6.xhtml_fig6_2) shows 𝒢[2] canonical element *τ̂* (basis functions for *τ̂* are defined by (6.1)) and corresponding curvilinear element *τ*. Points **p**[*i*], *i* = 1, …, 6 form the element so that each three points define a parabolic curve. For example, it is possible to plot a unique parabola through nodes **p**[2], **p**[3] and **p**[5]. As a result, the element *τ* can be expressed through the functions of second order, or, in other words, through basis functions (6.1). We come to the transformation

![An image shows two triangles with midpoints of the same placement as shown in figure 6.1 but the right-hand side triangle has curvilinear sides.](images/fig6_2.jpg)

[Figure 6.2:](#chapter6.xhtml_b6fig6_2) Canonical element *τ̂* and original curvilinear 𝒢[2] mesh element *τ*.

$$\begin{array}{l} {\mathbf{\mathbf{x}} = {\sum\limits_{i = 1}^{6}{\mathbf{\mathbf{p}}_{i}{\hat{\varphi}}_{i}(\hat{\mathbf{\mathbf{x}}})}},\quad\hat{\mathbf{\mathbf{x}}} \in \hat{\tau}} \end{array}$$(6.4)

which transforms *τ̂* into *τ*, and points $\hat{\mathbf{\mathbf{p}}_{i}}$ are transformed into **p**[*i*]. Note that if nodes of the element *τ* lie on the straight line, then transformation (6.4) reduces to linear form (6.2). As such, the difference between linear and curvilinear triangle elements is the way of transformation from *τ̂* to *τ*.

Likewise linear 𝒢[2] elements, to represent any function defined on curvilinear element *τ* through the basis function we utilize the expression (6.3) where basis functions now are not polynomials of the second order but function of the **x** being itself second-order polynomial.

## 6.3 STIFFNESS MATRIX WITH QUADRATIC BASIS FUNCTIONS

Let us consider calculation of the local stiffness matrix defined on the 𝒢[2] mesh elements (see (5.1))

$$\begin{array}{l} {{\overline{A}}_{\alpha\beta} = \int\limits_{\tau}\left( {c\nabla\varphi_{\beta} \cdot \nabla\varphi_{\alpha} + \mathbf{\mathbf{b}} \cdot \nabla\varphi_{\beta}\varphi_{\alpha} + a\varphi_{\beta}\varphi_{\alpha}} \right)d\mathbf{\mathbf{x}}.} \end{array}$$(6.5)

Method of calculation of the integral (6.5) considered below is applicable to both, curvilinear and linear, 𝒢[2] elements.

First, we define Jacobian matrix *J*(**x**) with $\mathbf{\mathbf{x}} = \mathbf{\mathbf{x}}(\hat{\mathbf{\mathbf{x}}}) = {(x_{1}(\hat{\mathbf{\mathbf{x}}}),x_{2}(\hat{\mathbf{\mathbf{x}}}))}^{T}$,

$$\begin{array}{l} {J(\hat{\mathbf{\mathbf{x}}}) = \left( \begin{array}{ll} \frac{\partial x_{1}}{\partial{\hat{x}}_{1}} & \frac{\partial x_{2}}{\partial{\hat{x}}_{1}} \\ \frac{\partial x_{1}}{\partial{\hat{x}}_{2}} & \frac{\partial x_{2}}{\partial{\hat{x}}_{2}} \end{array} \right)(\hat{\mathbf{\mathbf{x}}}).} \end{array}$$

Next, we substitute element *τ* by *τ̂* in the expression (6.5). By doing this we have

$$\begin{array}{l} \left. c(\mathbf{\mathbf{x}})\rightarrow\hat{c}(\hat{\mathbf{\mathbf{x}}}) = c(\mathbf{\mathbf{x}}(\hat{\mathbf{\mathbf{x}}})),\quad\varphi_{\alpha}(\mathbf{\mathbf{x}})\rightarrow{\hat{\varphi}}_{\alpha}(\hat{\mathbf{\mathbf{x}}}) \right. \end{array}$$

$$\begin{array}{l} \left. \nabla\rightarrow J^{- 1}(\hat{\mathbf{\mathbf{x}}})\hat{\nabla},\quad\hat{\nabla} = \left( {\partial/\partial{\hat{x}}_{1},\partial/\partial{\hat{x}}_{2}} \right)^{T},\quad d\mathbf{\mathbf{x}} = \middle| J(\hat{\mathbf{\mathbf{x}}}) \middle| d\hat{\mathbf{\mathbf{x}}}, \right. \end{array}$$

where basis functions ${\hat{\varphi}}_{\alpha}(\hat{\mathbf{\mathbf{x}}})$ are defined by (6.1), and

$$\begin{array}{ll} {{\overline{A}}_{\alpha\beta} = \int\limits_{\hat{\tau}}} & \left( {\hat{c}(\hat{\mathbf{\mathbf{x}}})J^{- 1}(\hat{\mathbf{\mathbf{x}}})\hat{\nabla}{\hat{\varphi}}_{\beta} \cdot J^{- 1}(\hat{\mathbf{\mathbf{x}}})\hat{\nabla}{\hat{\varphi}}_{\alpha}}~ \right. \\ & \left. \text{\quad\quad}\left. ~{+ \hat{\mathbf{\mathbf{b}}}(\hat{\mathbf{\mathbf{x}}}) \cdot J^{- 1}(\hat{\mathbf{\mathbf{x}}})\hat{\nabla}{\hat{\varphi}}_{\beta}{\hat{\varphi}}_{\alpha} + \hat{a}(\hat{\mathbf{\mathbf{x}}}){\hat{\varphi}}_{\beta}{\hat{\varphi}}_{\alpha}} \right) \middle| J(\hat{\mathbf{\mathbf{x}}}) \middle| d\hat{\mathbf{\mathbf{x}}}. \right. \end{array}$$(6.6)

To compute integral (6.6) we apply quadrature rule. Let us denote the integrand as $\hat{z}(\hat{\mathbf{\mathbf{x}}})$, then

$$\begin{array}{l} {{\overline{A}}_{\alpha\beta} = \int\limits_{\hat{\tau}}\hat{z}(\hat{\mathbf{\mathbf{x}}})d\hat{\mathbf{\mathbf{x}}} \approx {\sum\limits_{i = 1}^{q}{{\hat{\gamma}}_{i}\hat{z}(\hat{\mathbf{\mathbf{d}}_{i}})}},} \end{array}$$

where coefficients *γ̂*[*i*] and nodes $\hat{\mathbf{\mathbf{d}}_{i}}$, *i* = 1, …, *q* depend on particular chosen quadrature rule. Using quadrature with polynomials of the second order suffice for 𝒢[2] mesh.

When calculating integral (6.6) we make use of some properties of the 𝒢[2] mesh. Firstly, when computing ${\overline{A}}_{\alpha\beta}$ over triangle with straight edges, matrix *J*^(−1) = *B*^(−*T*) does not depend on $\hat{\mathbf{\mathbf{x}}}$ and ${\overline{A}}_{\alpha\beta}$ can be computed only once. However, in case of curvilinear triangular elements, Jacobian $J^{- 1}(\hat{\mathbf{\mathbf{x}}})$ needs to be calculated *q* times. Secondly, we can facilitate calculation of (6.6) by introducing matrices $\hat{D}(\hat{\mathbf{\mathbf{d}}_{i}}) \sim (2 \times 6)$

$$\begin{array}{l} {\hat{D}(\hat{\mathbf{\mathbf{d}}_{i}}) = \left\{ {\hat{\nabla}{\hat{\varphi}}_{\beta}(\hat{\mathbf{\mathbf{d}}_{i}})} \right\}_{\beta = 1}^{6},\quad D(\hat{\mathbf{\mathbf{d}}_{i}}) = J^{- 1}(\hat{\mathbf{\mathbf{d}}_{i}})\hat{D}(\hat{\mathbf{\mathbf{d}}_{i}}),} \end{array}$$

column-vectors

$$\begin{array}{l} {\hat{\mathbf{\mathbf{\varphi}}}(\hat{\mathbf{\mathbf{d}}_{i}}) = \left\{ {{\hat{\varphi}}_{\beta}(\hat{\mathbf{\mathbf{d}}_{i}})} \right\}_{\beta = 1}^{6},} \end{array}$$

and coefficients $\left. \gamma(\hat{\mathbf{\mathbf{d}}_{i}}) = {\hat{\gamma}}_{i} \middle| J(\hat{\mathbf{\mathbf{d}}_{i}}) \right|$ such that

$$\begin{array}{ll} {{\overline{A}}_{\alpha\beta} = {\sum\limits_{i = 1}^{q}{{\hat{\gamma}}_{i}\hat{z}(\hat{\mathbf{\mathbf{d}}_{i}})}}} & {= {\sum\limits_{i = 1}^{q}\gamma}(\hat{\mathbf{\mathbf{d}}_{i}})\left( {\hat{c}(\hat{\mathbf{\mathbf{d}}_{i}})\mathbf{\mathbf{D}}_{\beta}(\hat{\mathbf{\mathbf{d}}_{i}}) \cdot \mathbf{\mathbf{D}}_{\alpha}(\hat{\mathbf{\mathbf{d}}_{i}})}~ \right.} \\ & {\text{\quad\quad}\left. ~{+ \left( {\hat{\mathbf{\mathbf{b}}}(\hat{\mathbf{\mathbf{d}}_{i}}) \cdot \mathbf{\mathbf{D}}_{\beta}(\hat{\mathbf{\mathbf{d}}_{i}}) + \hat{a}(\hat{\mathbf{\mathbf{d}}_{i}}){\hat{\varphi}}_{\beta}(\hat{\mathbf{\mathbf{d}}_{i}})} \right){\hat{\varphi}}_{\alpha}(\hat{\mathbf{\mathbf{d}}_{i}})} \right),} \end{array}$$

where $\mathbf{\mathbf{D}}_{\alpha}(\hat{\mathbf{\mathbf{d}}_{i}})$ is the column of $D(\hat{\mathbf{\mathbf{d}}_{i}})$ with index *α*. Since **x** ⋅ **y** = **x**^(*T*)**y**, **x****y**^(*T*) = {*x*[*i*]*y*[*j*]}[*i*, *j* = 1]^(*n*), **x**, **y** ∈ **R**^(*n*), then local stiffness matrix can be expressed as

$$\begin{array}{ll} {\overline{A} = {\sum\limits_{i = 1}^{q}\gamma}(\hat{\mathbf{\mathbf{d}}_{i}})} & \left( {\hat{c}(\hat{\mathbf{\mathbf{d}}_{i}})D^{T}(\hat{\mathbf{\mathbf{d}}_{i}})D(\hat{\mathbf{\mathbf{d}}_{i}})}~ \right. \\ & {\text{\quad\quad}\text{\quad\quad}\text{\quad\quad}\left. ~{+ \hat{\mathbf{\mathbf{\varphi}}}(\hat{\mathbf{\mathbf{d}}_{i}})\left( {\hat{\mathbf{\mathbf{b}}}(\hat{\mathbf{\mathbf{d}}_{i}})D(\hat{\mathbf{\mathbf{d}}_{i}}) + \hat{a}(\hat{\mathbf{\mathbf{d}}_{i}}){\hat{\mathbf{\mathbf{\varphi}}}}^{T}(\hat{\mathbf{\mathbf{d}}_{i}})} \right)} \right).} \end{array}$$

The local forcing vector is calculated analogously, namely,

$$\begin{array}{l} {\overline{\mathbf{\mathbf{F}}} = {\sum\limits_{i = 1}^{q}{\gamma(\hat{\mathbf{\mathbf{d}}_{i}})\hat{f}(\hat{\mathbf{\mathbf{d}}_{i}})\hat{\mathbf{\mathbf{\varphi}}}(\hat{\mathbf{\mathbf{d}}_{i}})}}.} \end{array}$$

It is worth noting that the following is valid for the curvilinear triangular element (see 6.4)

$$\begin{array}{l} {\hat{f}(\hat{\mathbf{\mathbf{d}}_{i}}) = f(X\hat{\mathbf{\mathbf{\varphi}}}(\hat{\mathbf{\mathbf{d}}_{i}})),\quad J(\hat{\mathbf{\mathbf{d}}_{i}}) = \hat{D}(\hat{\mathbf{\mathbf{d}}_{i}})X^{T},\quad X_{2 \times 6} = (\mathbf{\mathbf{p}}_{1},\ldots,\mathbf{\mathbf{p}}_{6}),} \end{array}$$

where *X* is the matrix with interpolation nodes of the finite element *τ*.

Let us provide numerical values of coefficients $\gamma(\hat{\mathbf{\mathbf{d}}_{i}})$ for two particular quadrature rules. First one contains three nodes (*q* = 3), it interpolates exactly polynomials of the second order (𝒢[2] mesh) and has the following nodes and coefficients:

$$\begin{array}{l} {\hat{d} = \left( \begin{array}{lll} 0.5 & 0.5 & 0 \\ 0 & 0.5 & 0.5 \end{array} \right),\quad\hat{\gamma} = \frac{1}{6}\left( \begin{array}{lll} 1 & 1 & 1 \end{array} \right).} \end{array}$$

Second one contains six points and interpolates exactly polynomials of the fourth order. Its nodes and coefficients are given by

$$\begin{array}{ll} & {a_{1} = 0.09157621350977073,\quad a_{2} = 0.09157621350977073,} \\ & {b_{1} = 0.4459484909159649,\quad b_{2} = 0.4459484909159649,} \\ & {a_{3} = 1 - a_{1} - a_{2},\quad b_{3} = 1 - b_{1} - b_{2},} \\ & {\hat{d} = \left( \begin{array}{llllll} a_{1} & a_{1} & a_{3} & b_{1} & b_{1} & {b3} \\ a_{2} & a_{3} & a_{2} & b_{2} & b_{3} & {b2} \end{array} \right),} \\ & {\gamma_{1} = 0.1099517436553218,\quad\gamma_{2} = 0.2233815896780115,} \\ & {\hat{\gamma} = \frac{1}{2}\left( \begin{array}{llllll} \gamma_{1} & \gamma_{1} & \gamma_{1} & \gamma_{2} & \gamma_{2} & \gamma_{2} \end{array} \right).} \end{array}$$

Now, we consider calculation of the boundary matrix $\overline{S} = \left\{ {\overline{S}}_{\alpha\beta} \right\}$ and boundary vector $\overline{\mathbf{\mathbf{M}}} = \left\{ {\overline{M}}_{\alpha} \right\}$ (see expression 5.8). Let *e* be the boundary edge with endpoints **p**[1], **p**[2] and midpoint **p**[3], and *ê* = {*θ̂* ∈ [0, 1]} is a basis edge having endpoints $\hat{\mathbf{\mathbf{p}}_{1}} = 0$, $\hat{\mathbf{\mathbf{p}}_{2}} = 1$ and midpoint $\hat{\mathbf{\mathbf{p}}_{3}} = 0.5$. Then, basis functions defined on the edge can be expressed as

$$\begin{array}{l} {{\hat{\varphi}}_{1}(\hat{\theta}) = (1 - 2\hat{\theta})(1 - \hat{\theta}),\quad{\hat{\varphi}}_{2}(\hat{\theta}) = \hat{\theta}(2\hat{\theta} - 1),\quad{\hat{\varphi}}_{3}(\hat{\theta}) = 4\hat{\theta}(1 - \hat{\theta}).} \end{array}$$

Expression

$$\begin{array}{l} {\mathbf{\mathbf{x}} = \mathbf{\mathbf{x}}_{e}(\hat{\theta}) = \mathbf{\mathbf{p}}_{1}{\hat{\varphi}}_{1}(\hat{\theta}) + \mathbf{\mathbf{p}}_{2}{\hat{\varphi}}_{2}(\hat{\theta}) + \mathbf{\mathbf{p}}_{3}{\hat{\varphi}}_{3}(\hat{\theta})} \end{array}$$

defines transformation $\left. \hat{e}\rightarrow e\,(\hat{\mathbf{\mathbf{p}}_{k}}\rightarrow\mathbf{\mathbf{p}}_{k},\, k = 1,2,3) \right.$ and parametric representation of the edge as well. It is easy to see, that in case of straight line edge the midpoint **p**[3] = (**p**[1] + **p**[2])/2 and **x**[*e*](*θ̂*) = **p**[1](1 − *θ̂*) + **p**[2]*θ̂*. Boundary integrals (5.8) for calculation of ${\overline{S}}_{\alpha\beta}$ and ${\overline{M}}_{\alpha}$ rewritten in terms of *θ̂* over the basis edge *ê* have the form of one-dimensional integrals

$$\begin{array}{ll} {\overline{S}}_{\alpha\beta} & {= \int\limits_{0}^{1}\sigma(\mathbf{\mathbf{x}}_{e}(\hat{\theta})){\hat{\varphi}}_{\alpha}(\hat{\theta}){\hat{\varphi}}_{\beta}(\hat{\theta})l(\hat{\theta})d\hat{\theta},} \\ {\overline{M}}_{\alpha} & {= \int\limits_{0}^{1}\mu(\mathbf{\mathbf{x}}_{e}(\hat{\theta})){\hat{\varphi}}_{\alpha}(\hat{\theta})l(\hat{\theta})d\hat{\theta},} \end{array}$$(6.7)

where $l(\hat{\theta}) = \sqrt{{(x_{1}'(\hat{\theta}))}^{2} + {(x_{2}'(\hat{\theta}))}^{2}}$. For the straight line edge, *l*(*θ̂*) = |**p**[2] − **p**[1]|, and *l* is the length of edge.

To calculate one-dimensional integral, let us utilize quadrature rule

$$\begin{array}{l} {\int\limits_{0}^{1}\hat{z}(\hat{\theta})d\hat{\theta} \approx {\sum\limits_{i = 1}^{q}{{\hat{\gamma}}_{i}\hat{z}({\hat{d}}_{i})}}.} \end{array}$$

Likewise calculation of two-dimensional integral (6.6), we introduce column-vectors $\hat{\mathbf{\mathbf{\varphi}}}({\hat{d}}_{i}) = \left\{ {{\hat{\varphi}}_{\beta}({\hat{d}}_{i})} \right\}_{\beta = 1}^{3}$, $d\hat{\mathbf{\mathbf{\varphi}}}({\hat{d}}_{i}) = \left\{ {{\hat{\varphi}}_{\beta}'({\hat{d}}_{i})} \right\}_{\beta = 1}^{3}$ and matrix of nodes coordinates *X*[2 × 3] = (**p**[1], **p**[2], **p**[3]). Then, $x'({\hat{d}}_{i}) = Xd\hat{\mathbf{\mathbf{\varphi}}}({\hat{d}}_{i})$ and $\left. l({\hat{d}}_{i}) = \middle| Xd\hat{\mathbf{\mathbf{\varphi}}}({\hat{d}}_{i}) \right|$ is the length of the vector $Xd\hat{\mathbf{\mathbf{\varphi}}}({\hat{d}}_{i})$. Having introduced this, we come to the expressions for the matrix *S* and vector **M**

$$\begin{array}{ll} S & {= {\sum\limits_{i = 1}^{q}{\gamma({\hat{d}}_{i})\sigma(X\hat{\mathbf{\mathbf{\varphi}}}({\hat{d}}_{i}))\hat{\mathbf{\mathbf{\varphi}}}({\hat{d}}_{i}){\hat{\mathbf{\mathbf{\varphi}}}}^{T}({\hat{d}}_{i})}},} \\ \overline{\mathbf{\mathbf{M}}} & {= {\sum\limits_{i = 1}^{q}{\gamma({\hat{d}}_{i})\mu(X\hat{\mathbf{\mathbf{\varphi}}}({\hat{d}}_{i}))\hat{\mathbf{\mathbf{\varphi}}}({\hat{d}}_{i})}},} \end{array}$$(6.8)

where $\left. \gamma({\hat{d}}_{i}) = {\hat{\gamma}}_{i} \middle| Xd\hat{\mathbf{\mathbf{\varphi}}}({\hat{d}}_{i}) \right|$.

In conclusion, we provide coefficients for two particular quadrature rules defined on *[*0,1*]* which interpolates exactly polynomials of the third order. The first one is Gauss quadrature:

$$\begin{array}{ll} & {{\hat{\gamma}}_{1} = {\hat{\gamma}}_{2} = 0.5,\quad{\hat{d}}_{1} = 0.5\left( {1 - \sqrt{1/3}} \right),} \\ & {{\hat{d}}_{2} = 0.5\left( {1 + \sqrt{1/3}} \right),\quad q = 2.} \end{array}$$(6.9)

The second one is Simpson quadrature

$$\begin{array}{ll} & {{\hat{\gamma}}_{1} = {\hat{\gamma}}_{3} = 1/6,\quad{\hat{\gamma}}_{2} = 4/6,\quad{\hat{d}}_{1} = 0,} \\ & {{\hat{d}}_{2} = 0.5,\quad{\hat{d}}_{3} = 1,\quad q = 3.} \end{array}$$(6.10)

Using either (6.9) or (6.10) allows calculating boundary integrals (6.7) numerically and obtaining corresponding matrices (6.8).

# Conclusion

IN this book we have considered creating computational framework for the linear finite element method (FEM) with application to solving ordinary and partial differential equations having mixed boundary conditions. Each step of the FEM algorithm is described in detail and programming codes in MATLAB and Python are composed. Although there exists various software packages implementing FEM, understanding the basics of the FEM algorithm is important to utilize these packages. Explanations of the FEM algorithm and computational framework given in this book not only help to understand basics of the method but to provide guidance of how to build customized code for solving a problem using FEM. The latter is important since it allows to develop coding skills and to become more flexible with solving any nonstandard problem where standard FEM packages could fail to solve (or simply these packages are not available). Apart from this, coding functions from this book can be extended or modified to build improved FEM framework with some specific features if required.

Of course, we have only considered simple case of linear FEM, but it could be starting point to build more sophisticated algorithms. For example, solving nonlinear PDE results in FEM system which requires applying numerical methods to solve nonlinear systems. Creating FEM programming codes for three-dimensional case could be the next step a reader starts to look at.

# Appendix A Variational Formulation of a Boundary Value Problem

DOI: [10.1201/9781003265979-A](https://doi.org/10.1201/9781003265979-A)

HERE we discuss variational approach to solve BVP. Variational methods are used in many applications where a problem can be expressed in terms of so-called variational principles. In accordance with one of these principles, function *u*(*x*) being a solution to a BVP at the same time must be a stationary point of a variational functional

$$\begin{array}{l} {J(u) = {\int\limits_{s_{0}}^{s_{1}}{F(x,u,u')dx}},} \end{array}$$

where *s*[0] and *s*[1] are constants, *u*(*x*) is a twice continuously differentiable function and function *F* is twice continuously differentiable with respect to its arguments. A stationary point is a function *u*^*(*x*) which makes *J*(*u*) stationary, or when the first-order change in *J*(*u*) with respect to the function *u*(*x*) vanishes. Usually, variational functional has a certain meaning, for example, it could be a potential energy and a stationary point is a function that minimizes the energy. It is known from variational calculus that a stationary point is solution to the Euler-Lagrange equation

$$\begin{array}{l} {- \frac{d}{dx}\frac{\partial F}{\partial u'} + \frac{\partial F}{\partial u} = 0.} \end{array}$$(A.1)

If equation (A.1) is complemented with some boundary conditions

$$\begin{array}{l} {u(s_{0}) = u_{s_{0}},\quad u(s_{1}) = u_{s_{1}},} \end{array}$$(A.2)

then we see that finding a stationary point of *J*(*u*) is equivalent to solving BVP (A.1) – (A.2).

As an example, let us consider the functional

$$\begin{array}{l} {J(u) = \frac{1}{2}{\int\limits_{s_{0}}^{s_{1}}{c(x)\left( {u'(x)} \right)^{2} + a(x)u^{2}(x) - f(x)u(x)dx}},} \end{array}$$(A.3)

where *c*(*x*), *a*(*x*) and *f*(*x*) are piecewise continuous functions and *c*(*x*) > 0, *b*(*x*) > 0. A variational problem is to find a function *u*(*x*) which minimizes *J*(*u*).

$$\begin{array}{l} \left. J(u)\rightarrow\min,\quad u(s_{0}) = u_{s_{0}},\quad u(s_{1}) = u_{s_{1}}. \right. \end{array}$$(A.4)

Then, the Euler-Lagrange equation takes the form

$$\begin{array}{l} {- \left( {c(x)u'(x)} \right)' + a(x)u(x) = f(x).} \end{array}$$(A.5)

It can be shown that stationary point in this case is a function which minimizes (A.3). As a result, solving (A.3) – (A.4) is equivalent to solving BVP (A.5) – (A.2).

In practice, the BVP (A.5) – (A.2) is replaced by the integral expression (A.3) for which a minimization problem is considered with some approximation of unknown function. In the context of FEM, the unknown function *u* is represented through linear combination of some known functions, *φ*[*i*](*x*), and coefficients, *α*[*i*], as follows:

$$\begin{array}{l} {u(x) = {\sum\limits_{i = 1}^{N}{\alpha_{i}\varphi_{i}(x)}}.} \end{array}$$(A.6)

By substituting (A.6) into (A.3) we come to the problem of minimization of multivariate function *J*(*α*[*i*]*φ*[*i*](*x*)) with respect to variables *α*[*i*]. According to the first-order necessary condition for a minimum, variables *α*[*i*] can be found from equations

$$\begin{array}{l} {\frac{\partial}{\partial\alpha_{i}}J\left( {\sum\limits_{i = 1}^{N}{\alpha_{i}\varphi_{i}}} \right) = 0.} \end{array}$$

By adding to these equations conditions (A.2) we come to a system of equations for finding coefficients *α*[*i*] which defines solution (A.6).

One limitation of the variational approach to solve BVP is that it is applicable only in case when a given differential equation represents Euler-Lagrange equation which is not always achievable. For example, BVP (1.1) is not allowing variational formulation. Instead, projective method can be used which is considered throughout this book.

# Appendix B Discussion of Global Interpolating Polynomial

DOI: [10.1201/9781003265979-B](https://doi.org/10.1201/9781003265979-B)

LET us consider a global approximating polynomial, *P*[*m*](*x*), of the order *m* defined on the interval [*s*[0], *s*[1]] which interpolates a function *f*(*x*). Set of interpolation nodes forms a sequence

$$\begin{array}{l} {s_{0} = x_{1} < x_{2} < \cdots < x_{m + 1} = s_{1}.} \end{array}$$

We want to analyse what happens when number of nodes increases (for example, to improve function approximation accuracy). Below, various types of approximation errors are considered, and it is shown how increasing number of interpolation nodes (and accordingly the degree of polynomial *P*[*m*]) leads to accumulation of these errors.

**Convergence with increasing number of nodes**. Suppose that we have chosen some strategy of increasing polynomial degree, *m*, by introducing new nodes according to some rule. The question arises, whether it is always true that such polynomials converge to the source function, or

$$\begin{array}{l} \left. \Delta(P_{m}) = \max\limits_{\lbrack s_{0},s_{1}\rbrack} \middle| f(x) - P_{m}(x) \middle| \underset{m\rightarrow\infty}{\overset{}{\rightarrow}}0\. \right. \end{array}$$

The short answer is not. To illustrate this, let us consider the Runge function[¹](#appB.xhtml_fn2_1) *f*(*x*) = 1/(1 + 25*x*²), *x* ∈ [−1, 1], and a simple strategy which consists of having uniformly distributed nodes with the step *h* = 2/*m*, that is *x*[*i*] = −1 + (*i* − 1)*h*, *i* = 1, …, *m* + 1. The polynomial degree increases with increasing *m* and the result of applying this strategy with *m* = {6, 10, 14} is shown in [figure B.1](#appB.xhtml_figB_1). It can be seen that when *m* increases, approximation in the central part of the interval shows perfect result; however, polynomials diverge in the end regions, 0.73 ≲ |*x*| ≤ 1.

![Four parts image illustrating approximation divergence with increasing polynomial degree. Part (a) shows two lines: one has bell-like shape which is source function and the other one has arch shape which is approximation with three nodes. The lines are significantly different and does not coincide. Part (b) shows two lines: one has bell-like shape which is source function and the other one has wavy shape which is approximation with six nodes. The lines are close but not coincide in the middle part of the graph. Part (c) shows two lines: one has bell-like shape which is source function and the other one has wavy shape which is approximation with ten nodes. The lines are coincided mostly in the middle part of the graph but significantly diverge at the corners. Part (d) shows two lines: one has bell-like shape which is source function and the other one has bell-like shape in the middle and wavy shape close to corners which is approximation with fourteen nodes. The lines are coincided exactly in the middle part of the graph but significantly diverge at the corners.](images/fig8_1.jpg)

[Figure B.1:](#appB.xhtml_bfigB_1) Example of approximation divergence with increasing polynomial degree, *m*, for uniformly distributed interpolation nodes when (a) *m* = 3; (b) *m* = 6; (c) *m* = 10; (d) *m* = 14. Here, the source function is *f*(*x*) = 1/(1 + 25*x*²) (solid line), and approximation is performed using Lagrange basis functions (dashed line).

![Two parts image illustrating Influence of the interpolation node distribution on the approximation error. Part (a) shows three lines: first has bell-like shape which is source function; second line is an approximation with Chebyshev nodes, and it is close to the first one but a bit wavy at the corners; the third one is an approximation with uniformly distributed nodes, and it has significant deviation from the source function at the corner regions. Part (b) shows two lines corresponding to approximation error. First line represents error for the approximation with Chebyshev nodes which oscillates with values close to zero and the second line represents the approximation with uniformly distributed nodes, and it has mush larger oscillation compared with the first line.](images/fig8_2.jpg)

[Figure B.2:](#appB.xhtml_bfigB_2) Influence of the interpolation node distribution on the approximation error. Plot (a) shows the source function *f*(*x*) = 1/(1 + 25*x*²) (solid line), approximating polynomial of degree *m* = 10 having uniform node distribution (dashed line) and the polynomial which nodes are roots of the Chebyshev polynomial of the second kind (dotted line). Plot (b) illustrates dependence of the error function, *ω*[*m* + 1], on the node distribution. Here, the solid line corresponds to the uniform distribution and the dashed line corresponds to the nodes being the Chebyshev polynomial roots.

We conclude that uniform distribution of nodes could potentially lead to approximation divergence. To understand why the node distribution is of importance, let us consider the approximation error, *Δ*(*P*[*m*]), which can be estimated as

$$\begin{array}{l} \left. \Delta(P_{m}) \leq \frac{\left| f^{(m + 1)}(\xi) \right|}{(m + 1)!}\max\limits_{\lbrack s_{0},s_{1}\rbrack} \middle| \omega_{m + 1}(x) \middle| , \right. \end{array}$$

where

$$\begin{array}{l} {\omega_{m + 1}(x) = (x - x_{1})(x - x_{2})\cdots(x - x_{m + 1}),} \end{array}$$

and *ξ* ∈ [*s*[0], *s*[1]]. It can be seen that the error depends on function *ω*[*m* + 1] which, in turn, depends on the relative nodes location. The problem of divergence can be resolved by choosing nodes to be roots of an orthogonal polynomial, for example, taking nodes to be *x*[*i*] = −cos (*π*(*i* − 1)/*m*), 1 ≤ *i* ≤ *m* + 1 improves convergence (see [figure B.2](#appB.xhtml_figB_2)).[²](#appB.xhtml_fn2_2)

Although taking orthogonal polynomial roots as interpolation nodes is a good strategy, practically it could be inapplicable in some cases, for example, when interpolation nodes are prescribed through a table of function values which leaves no freedom of changing the nodes distribution.

**Error of input data and approximation accuracy**. Another source of polynomial approximation error arises from the fact that the function values at the interpolation nodes, *f*[*i*] = *f*(*x*[*i*]), are specified or calculated with some errors, *ϵ*[*i*], that is *f*[*i*]^* = *f*[*i*] + *ϵ*[*i*]. As a result, polynomial *P*[*m*]^*(*x*) constructed from the nodes *f*[*i*]^* inevitably contains errors as well

$$\begin{array}{l} {P_{m}(x) - P_{m}^{*}(x) = {\sum\limits_{j = 1}^{m + 1}\epsilon_{j}}\varphi_{j}(x),} \end{array}$$

where *φ*[*j*](*x*) is a Lagrange basis function. If *ϵ*^* = max {*ϵ*[*i*]}, then the following estimation takes place

$$\begin{array}{l} \left. \max\limits_{\lbrack s_{0},s_{1}\rbrack} \middle| P_{m}(x) - P_{m}^{*}(x) \middle| \leq \Lambda_{m}\epsilon^{*},\quad\Lambda_{m} = \max\limits_{\lbrack s_{0},s_{1}\rbrack}\left. \sum\limits_{j = 1}^{m + 1} \right|\varphi_{j}(x) \middle| . \right. \end{array}$$

Here, *Λ*[*m*] is called the Lebesgue constant. It can be seen that the constant *Λ*[*m*] represents the factor by which approximation error increases when the input data error is introduced. Sensitivity of the approximation method to the errors of input data is characterized by a conditional number which can be defined by the Lebesgue constant. The value of *Λ*[*m*] depends only on nodes distribution but not on the interval length. Asymptotic estimation shows that the Lebesgue constant grows logarithmically with *m* → ∞ if Chebyshev nodes are used. On the other hand, it grows exponentially in the case of equidistant nodes. The former fact leads to conclusion, that it is recommended to avoid using high order global interpolation polynomials having equidistant nodes distribution. Alternative approach is to use a piecewise local interpolation when the interval [*s*[0], *s*[1]] is split into subintervals and function *f* is approximated by interpolating polynomial of low order on each subinterval.

# Appendix C Interpolatory Quadrature Formulas

DOI: [10.1201/9781003265979-C](https://doi.org/10.1201/9781003265979-C)

QUADRATURE formulas are used to approximate integrals of functions which are not computed exactly. The most common quadrature formulas look like

$$\begin{array}{l} {{\int\limits_{s_{0}}^{s_{1}}{fdx}} \approx {\sum\limits_{i = 1}^{n}{\gamma_{i}f(x_{i})}}.} \end{array}$$

Here *x*[*i*] are called nodes of the formula and *γ*[*i*] are called weights.

In other words, if *φ*[*i*](*x*) are basis functions, then

$$\begin{array}{l} {{\int\limits_{s_{0}}^{s_{1}}{fdx}} \approx {\int\limits_{s_{0}}^{s_{1}}{\sum\limits_{i = 1}^{n}{f(x_{i})\varphi_{i}(x)}}} = {\sum\limits_{i = 1}^{n}{f(x_{i})}}\underset{\gamma_{i}}{\underset{︸}{\int\limits_{s_{0}}^{s_{1}}{\varphi_{i}(x)dx}}} = {\sum\limits_{i = 1}^{n}{\gamma_{i}f(x_{i})}}.} \end{array}$$

Obviously, if basis functions are integrated exactly then the order of precision of an interpolatory formula will be at least *n* − 1. Well-known rectangle formula, trapezoidal rule and Simpson rule are interpolatory quadrature rules corresponding to the polynomials of the zeroth, first and second orders, respectively.

It is seen from the above formula that the precision of quadrature formula can be increased by increasing number of interpolating nodes (degree of interpolating polynomial). However, if there is a freedom in choosing distribution of nodes then the precision could be increased through particular choice of nodes location with fixed number *n*. This can be illustrated as follows: Suppose we have a function *f* defined on the interval which is approximated by a linear polynomial with two nodes, *x*[1] and *x*[2] (see [figure C.1](#appC.xhtml_figC_1)). Then the trapezoid quadrature rule gives a value of the integral equalling the area *ABCD* and this rule has the first order of precision. On the other hand, if we consider a rectangle formula with a freedom of choice of interpolation node, *x*[1]^*, we can find location of *x*[1]^* so that the area *AEFD* (result of rectangle formula) would be equal to the area *ABCD*. In this situation, the rectangle formula results not in the zeroth order of precision but in the first order. This is achieved through the particular choice of node location.

![An image shows three lines plotted in the coordinate system. First line has an arch form, and this is a source function. Second line connects corner points of the source function with straight line and it is labelled with letters BC. The third line is a straight line which goes through the middle point of the second one and indicated with letters EF. There are two perpendiculars to the horizontal axis coming from the points B and C which are labelled as BA and CD.](images/fig9_1.jpg)

[Figure C.1:](#appC.xhtml_bfigC_1) Illustration of rectangle and trapezoid quadrature rules.

There are several algorithms for computing the nodes *x*[*i*] and weights *w*[*i*] of Gaussian quadrature rule and one of them is given below. We start by considering a quadrature for the interval [−1, 1] with *n* nodes[¹](#appC.xhtml_fnC_1)

$$\begin{array}{l} {{\int\limits_{- 1}^{1}{fdx}} \approx {\sum\limits_{i = 1}^{n}{\gamma_{i}f(x_{i})}}.} \end{array}$$

Note that this formula is exact for the polynomial of some degree *N* if and only if it is exact for the set of functions *f* = 1, *x*, *x*², …, *x*^(*N*). This is equivalent to the fact that nodes and weights must satisfy the following system of nonlinear equations

$$\begin{array}{l} {{\sum\limits_{i = 1}^{n}{\gamma_{i}x_{i}^{k}}} = {\int\limits_{- 1}^{1}{x^{k}dx}} = \frac{1 - {( - 1)}^{k + 1}}{k + 1},\quad k = 0,\ldots,N.} \end{array}$$

It can be shown that the system has unique solution if the number of unknowns is equal to the number of equations, so *N* = 2*n* − 1. For example, Gaussian quadrature with two nodes corresponds to *n* = 1 and *N* = 3. Weights and nodes are found from the system

$$\begin{array}{ll} {\gamma_{1} + \gamma_{2}} & {= {\int\limits_{- 1}^{1}{dx}} = 2,} \\ {\gamma_{1}x_{1} + \gamma_{2}x_{2}} & {= {\int\limits_{- 1}^{1}{xdx}} = 0,} \\ {\gamma_{1}x_{1}^{2} + \gamma_{1}x_{2}^{2}} & {= {\int\limits_{- 1}^{1}{x^{2}dx}} = \frac{2}{3},} \\ {\gamma_{1}x_{1}^{3} + \gamma_{1}x_{2}^{3}} & {= {\int\limits_{- 1}^{1}{x^{3}dx}} = 0.} \end{array}$$

By solving it, we find the values: *γ*[1] = *γ*[2] = 1, $x_{1} = - 1/\sqrt{3},x_{2} = 1/\sqrt{3}$. As a result we obtain Gaussian quadrature with two nodes being exact for polynomials of the third order

$$\begin{array}{l} {{\int\limits_{- 1}^{1}{fdx}} \approx f\left( {- \frac{1}{\sqrt{3}}} \right) + f\left( \frac{1}{\sqrt{3}} \right).} \end{array}$$

Nodes and weights for larger values of *m* can be found tabulated in many numerical analysis books.

**Conditional number of interpolatory quadrature formulas**. When computing integrals, an integrand is often known approximately with some error (for example, it could be computed with some rounding error or measured with error). As a result, instead of exact value of the integrand, *f*, approximated value is available, *f*^* = *f* + *ϵ*, having some error *ϵ*. Let us estimate sensitivity of interpolatory quadrature with respect to input data, or equivalently, defined a quadrature conditional number, *ν*. If we assume that |*f*(*x*) − *f*^*(*x*)| < *ϵ*^* ∀*x* ∈ [*s*[0], *s*[1]], then

$$\begin{array}{l} {\left| {{\sum\limits_{i = 1}^{n}{\gamma_{i}f(x_{i})}} - {\sum\limits_{i = 1}^{n}{\gamma_{i}f^{*}(x_{i})}}} \right| \leq \epsilon^{*}{\sum\limits_{i = 1}^{n}\left| \gamma_{i} \right|} = \nu\epsilon^{*},\quad\nu = {\sum\limits_{i = 1}^{n}\left| \gamma_{i} \right|}.} \end{array}$$

As such, perturbing input data lead to increasing quadrature error by factor *ν* which is a conditional number. One important observation regarding the conditional number is that

$$\begin{array}{l} {\nu = {\sum\limits_{i = 1}^{n}\left| \gamma_{i} \right|} \geq {\sum\limits_{i = 1}^{n}\gamma_{i}},} \end{array}$$

which means that if all weights are positive we obtain the smallest conditional number; otherwise, we come to an ill-conditional quadrature. All weights of Gaussian quadrature are positive which guarantees stability with respect to input data errors.

# Appendix D Quadrature Rules and Orthogonal Polynomials

DOI: [10.1201/9781003265979-D](https://doi.org/10.1201/9781003265979-D)

IN general case, Gaussian quadrature rule for integral numerical calculation can be derived using property of orthogonal polynomials. Here, we provide some basics of the orthogonal polynomials theory and give generic formulas to calculate quadrature nodes and weights. Let us start with a definition.

It is easy to see that orthogonal polynomials are defined up to constant multipliers. Choice of multiplier values can be dictated by some normalization, for example, they can be chosen so that to obtain unity leading polynomial coefficient. An overview of the most important properties of the orthogonal polynomials is given below.

1.  The polynomial *P*[*n*](*t*) has *n* real distinctive roots which are within the interval of orthogonality.

2.  The sequence of orthogonal polynomials satisfies a recurrence relation of the form

    $$\begin{array}{l} {P_{k + 1}(x) = (a_{k}x - b_{k})P_{k}(x) - c_{k}P_{k - 1}(x),\quad k \geq 0,\quad P_{- 1}(x) = 0.} \end{array}$$

3.  Polynomial roots, {*x*[*k*]}[*k* = 1]^(*m*), are the eigenvalues of the following tridiagonal matrix

    $$\begin{array}{l} {A_{n} = \left( \begin{array}{lllll} \alpha_{0} & \sqrt{\beta_{1}} & & & \\ & & & & \\ \sqrt{\beta_{1}} & \alpha_{1} & \sqrt{\beta_{2}} & & \\ & & & & \\ & {\ddots \ddots} & \ddots & & \\ \, & & \sqrt{\beta_{n - 2}} & \alpha_{n - 2} & \sqrt{\beta_{n - 1}} \\ & & & \sqrt{\beta_{n - 1}} & \alpha_{n - 1} \end{array} \right),} \end{array}$$(D.1)

    where

    $$\begin{array}{l} {\alpha_{k} = \frac{b_{k}}{a_{k}},\quad k \geq 0,\quad\beta_{k} = \frac{c_{k}}{a_{k - 1}a_{k}},\quad k \geq 1.} \end{array}$$(D.2)

4.  Polynomial roots, {*x*[*k*]}[*k* = 1]^(*n*), are the nodes of Gauss Jacobi quadrature

    $$\begin{array}{l} {{\int\limits_{s_{0}}^{s_{1}}{f(x)\omega(x)dx}} \approx {\sum\limits_{k = 1}^{n}{\gamma_{k}f(x_{k})}},} \end{array}$$(D.3)

    where all *γ*[*k*] > 0 and the quadrature is exact if *f* is a polynomial of order 2*n* − 1. Vector of quadrature weights, **γ** = {*γ*[*k*]}[*k* = 1]^(*m*), is found from the expression

    $$\begin{array}{l} {\gamma_{k} = U_{1k}^{2}m_{0},\quad m_{0} = {\int\limits_{s_{0}}^{s_{1}}{\omega(x)dx}},} \end{array}$$(D.4)

    where *U*[1*k*] is the first row of the matrix *U*, columns of which are normalized eigenvectors (i.e., eigenvectors with unity Euclidean norm) of the matrix *A*[*n*], and *A*[*n*] = *U**Λ**U*^(−1), *Λ* =  diag (*x*[1], …, *x*[*n*]).

An important family of orthogonal polynomials are Jacobi polynomials determined by the weight function of the form

$$\begin{array}{l} {\omega(x) = {(1 - x)}^{\alpha}{(1 + x)}^{\beta},\quad(s_{0},s_{1}) = ( - 1,1),\quad\alpha,\beta > - 1.} \end{array}$$

In this case, orthogonal polynomials depend on parameters {*α*, *β*} and first two polynomials can be expressed as

$$\begin{array}{l} {P_{0}^{(\alpha,\beta)}(x) = 1,\quad P_{1}^{(\alpha,\beta)}(x) = \frac{1}{2}\left( {\left( {\alpha + \beta + 2} \right)x + \alpha - \beta} \right).} \end{array}$$

Coefficients of recurrent formula are found through

$$\begin{array}{ll} a_{k} & {= \frac{(2k + \alpha + \beta + 1)(2k + \alpha + \beta + 2)}{2(k + 1)(k + \alpha + \beta + 1)},} \\ b_{k} & {= \frac{(\beta^{2} - \alpha^{2})(2k + \alpha + \beta + 1)}{2(k + 1)(k + \alpha + \beta + 1)(2k + \alpha + \beta)},} \\ c_{k} & {= \frac{(k + \alpha)(k + \beta)(2k + \alpha + \beta + 2)}{(k + 1)(k + \alpha + \beta + 1)(2k + \alpha + \beta)}.} \end{array}$$(D.5)

Integral in (D.4) can be found as follows:

$$\begin{array}{l} {m_{0} = 2^{\alpha + \beta + 1}\frac{\Gamma(\alpha + 1)\Gamma(\beta + 1)}{\Gamma(\alpha + \beta + 2)},} \end{array}$$(D.6)

where *Γ*(*x*) is a gamma function which is defined as *Γ*(*x*) = (*x* − 1)! for any positive integer *x*. Derivatives of polynomials can be determined through the expression

$$\begin{array}{l} {\frac{d}{dx}P_{n}^{(\alpha,\beta)} = \frac{1}{2}(m + \alpha + \beta + 1)P_{n - 1}^{(\alpha + 1,\beta + 1)}(x).} \end{array}$$(D.7)

Let us indicate some particular cases. When *α* = *β* = −1/2 we obtain Chebyshev polynomials of the first type, *T*[*n*]. Parameters *α* = *β* = 0 correspond to Legendre polynomials, *L*[*n*] = *P*[*n*]^((0, 0)), which represent an important class of polynomials for obtaining quadrature rules. It is worth indicating that when considering Legendre polynomials, we have *ω*(*x*) = 1 and the quadrature (D.3) transforms into Gaussian quadrature rule over the interval [−1, 1]

$$\begin{array}{l} {{\int\limits_{- 1}^{1}{f(x)dx}} \approx {\sum\limits_{k = 1}^{n}{\gamma_{k}f(x_{k})}},} \end{array}$$

By substituting *α* = 0 and *β* = 0 into (D.5) and (D.6) we find the matrix coefficients (D.2) to be *α*[*k*] = 0, *β*[*k*] = *k*²/(4*k*² − 1), and the integral *m*[0] = 2. As a result, quadrature weights to be *γ*[*k*] = 2*U*[1*k*]² and corresponding quadrature nodes are the eigenvalues of matrix *A*[*n*].

The nodes of the Gaussian quadrature, being the zeros of Legendre polynomials, do not encompass the boundaries −1 and 1 of the interval [−1, 1]. In some circumstance, it is desirable to include these points in the boundaries. This is possible at the price of reducing by 2 units the degree of exactness of the Gaussian quadrature which results in Lobatto quadrature

$$\begin{array}{l} {{\int\limits_{- 1}^{1}{f(x)dx}} \approx \frac{2}{n(n - 1)}f( - 1) + {\sum\limits_{k = 2}^{n - 1}{\gamma_{k}f(x_{k})}} + \frac{2}{n(n - 1)}f(1).} \end{array}$$

Similar to the Gaussian quadrature problem stated previously, in Lobatto quadrature we constrain *x*[1] = −1 and *x*[*n*] = 1, which means we now have less degree of freedom and the Lobatto quadrature is exact for polynomials of order 2*m* − 3. In this case, quadrature nodes are roots of the polynomial (1 − *x*²)*L*[*n* − 1]^′(*x*). Indeed, *x*[1] and *x*[*n*] are the roots of (1 − *x*²), and nodes *x*[2], …, *x*[*n* − 1], are the *n* − 2 zeros of the polynomial *L*[*n* − 1]^′, or equivalently the points where the polynomial *L*[*n* − 1] is extremal. From (D.7) we see that roots of *L*[*n* − 1]^′ are roots of *P*[*n* − 2]^((1, 1)), and by substituting *α* = 1 and *β* = 1 into (D.5) and (D.6) we find the matrix coefficients (D.2) to be *α*[*k*] = 0, *β*[*k*] = *k*(*k* + 1)/((2*k* + 1)(2*k* + 3)), and the integral *m*[0] = 4/3. Once quadrature weights, *γ̃*[*k*], for *L*[*n* − 1]^′ are found, corresponding weights for (1 − *x*²)*L*[*n* − 1]^′ are defined as *γ*[*k*] = *γ̃*[*k*]/(1 − *x*[*k*]²).

# Appendix E Computational Framework in Python

DOI: [10.1201/9781003265979-E](https://doi.org/10.1201/9781003265979-E)

## E.1 ASSEMBLING MATRICES

How to calculate and assemble FEM matrices is explained in [sections 5.3](#chapter5.xhtml_sec5_3)–[5.5](#chapter5.xhtml_sec5_5) where MATLAB function assemba() for the vectorized version of the assembling algorithm is given. It is straightforward to translate this function into Python with some minor changes.

Below we provide Python code for matrix calculating and assembling algorithm utilizing sparse matrices. It follows the structure of the MATLAB code given in [section 5.5](#chapter5.xhtml_sec5_5).

![](images/compE_1.jpg)![](images/compE_1_2.jpg)

## E.2 ASSEMBLING BOUNDARY CONDITIONS

Implementation of boundary condition calculation in Python is based on the approach described in [section 5.6](#chapter5.xhtml_sec5_6). We use dictionary structure containing list of boundary segments and corresponding function names defined on these segments. For example, by defining the function uD(x1,x2,sdl)

![](images/compE_2.jpg)

we can specify Dirichlet boundary conditions on the first and third segments as

![](images/compE_3.jpg)

Python implementation of the function assemblingBC() given below performs assembling boundary conditions and repeat the logic of the corresponding MATLAB function.

![](images/compE_4.jpg)![](images/compE_4_2.jpg)![](images/compE_4_3.jpg)

Here, we need to explain how to implement in Python some MATLAB functions. For instance, MATLAB function find(a) which finds indices and values of nonzero elements of the array a can be represented in Python as function numpy.nonzero(a) which returns a tuple of arrays, one for each dimension of a, containing the indices of the nonzero elements in that dimension. To group the indices by element, rather than dimension, we can use numpy.transpose(numpy.nonzero(a)) which results in two-dimensional array of indices with a row for each nonzero element. Logical operations over Boolean arrays can be performed through special functions of the numpy package, for example, function numpy.logical_or(x1,x2) applies logical OR to the elements of x1 and x2. MATLAB function ismember(x1,x2) corresponds to Python function numpy.isin(x1,x2) which returns a Boolean array of the same shape as array x1 that is True where an element of x1 is in x2 and False otherwise. [Listing E.4](#appE.xhtml_listE_4) shows a function assemblingPDE() code for solving a PDE problem. Function spsolve() is used here to solve linear system of sparse matrices.

![](images/compE_5.jpg)

## E.3 SOLVING EXAMPLE PROBLEM

As a final step, let us create a Python code for solving the example problem formulated in [section 5.8](#chapter5.xhtml_sec5_8). The code is self-documented and easy to read.

![](images/compE_6.jpg)![](images/compE_6_2.jpg)![](images/compE_6_3.jpg)

Here, geometry is defined in function disk() and BC are specified in functions uD(), sigma() and mu(). Function testPDE() when called calculates solution values and prints solution error in various norms.

# Bibliography

*   [[1]](#fm-chapter2.xhtml_b2refbib_1) G. Dhatt, G. Touzot, and E. Lefrancois. Finite Element Method. London, UK: ISTE Ltd, 2012.
*   [[2]](#fm-chapter2.xhtml_b2refbib_2) A.J.M. Ferreira. MATLAB Codes for Finite Element Analysis. Vol. 157. Solid Mechanics and Its Applications. Springer, 2009.
*   [[3]](#fm-chapter2.xhtml_b2refbib_3) Mark S. Gockenbach. Understanding and Implementing the Finite Element Method. Society for Industrial and Applied Mathematics, 2006.
*   [[4]](#fm-chapter2.xhtml_b2refbib_4) E. Jones, T. Oliphant, P. Peterson, et al. *SciPy: Open Source Scientific Tools for Python.* 2001\. url: [http://www.scipy.org/](http://www.scipy.org).
*   [[5]](#fm-chapter2.xhtml_b2refbib_5) Gang Li. Introduction to the Finite Element Method and Implementation with MATLAB. Cambridge University Press, 2020.
*   [[6]](#fm-chapter2.xhtml_b2refbib_6) *MATLAB and Partial Differential Equation Toolbox Release* *2019a*. Natick, Massachusetts, USA, 2019\. url: [http://www.mathworks.com/](http://www.mathworks.com).
*   [[7]](#fm-chapter2.xhtml_b2refbib_7) Travis E. Oliphant. A Guide to NumPy. USA: Trelgol Publishing, 2006.

# Index

*   Approximate solution [14](#chapter1.xhtml_p14), [71](#chapter3.xhtml_p71)
*   Assembling boundary conditions [51](#chapter2.xhtml_p51), [121](#chapter5.xhtml_p121)
*   Assembling global matrices [29](#chapter1.xhtml_p29), [75](#chapter3.xhtml_p75), [101](#chapter5.xhtml_p101)

*   Barycentric formula [10](#chapter1.xhtml_p10)
*   Basis functions [9](#chapter1.xhtml_p9), [10](#chapter1.xhtml_p10), [15](#chapter1.xhtml_p15), [30](#chapter1.xhtml_p30), [72](#chapter3.xhtml_p72)
*   Boundary value problem [3](#chapter1.xhtml_p3), [70](#chapter3.xhtml_p70)

*   Canonical element [30](#chapter1.xhtml_p30), [109](#chapter5.xhtml_p109)
*   Chebyshev polynomials [151](#appD.xhtml_p151)
*   Classical solution [4](#chapter1.xhtml_p4)
*   Connectivity matrix [74](#chapter3.xhtml_p74), [85](#chapter4.xhtml_p85)

*   Differentiating matrix [32](#chapter1.xhtml_p32)
*   Dirichlet boundary condition [3](#chapter1.xhtml_p3), [70](#chapter3.xhtml_p70)

*   Edge matrix [75](#chapter3.xhtml_p75), [85](#chapter4.xhtml_p85)
*   Extended local forcing vector [29](#chapter1.xhtml_p29), [75](#chapter3.xhtml_p75)
*   Extended local stiffness matrix [28](#chapter1.xhtml_p28), [75](#chapter3.xhtml_p75)

*   Finite element method [xiii](#fm-chapter2.xhtml_pxiii), [8](#chapter1.xhtml_p8), [14](#chapter1.xhtml_p14)
*   Finite elements [13](#chapter1.xhtml_p13), [71](#chapter3.xhtml_p71), [72](#chapter3.xhtml_p72)

*   Gaussian quadrature [34](#chapter1.xhtml_p34), [146](#appC.xhtml_p146), [151](#appD.xhtml_p151)
*   Global forcing vector [17](#chapter1.xhtml_p17), [28](#chapter1.xhtml_p28), [73](#chapter3.xhtml_p73), [74](#chapter3.xhtml_p74)
*   Global stiffness matrix [17](#chapter1.xhtml_p17), [27](#chapter1.xhtml_p27), [73](#chapter3.xhtml_p73), [74](#chapter3.xhtml_p74)

*   Integral equation [7](#chapter1.xhtml_p7), [71](#chapter3.xhtml_p71)
*   Interpolating matrix [32](#chapter1.xhtml_p32)
*   Interpolating polynomial [9](#chapter1.xhtml_p9), [73](#chapter3.xhtml_p73)
*   Interpolation condition [9](#chapter1.xhtml_p9)
*   Interpolation nodes [9](#chapter1.xhtml_p9)
*   Interpolatory quadrature [145](#appC.xhtml_p145)

*   Lagrange spline [13](#chapter1.xhtml_p13)
*   Lobatto quadrature [35](#chapter1.xhtml_p35), [152](#appD.xhtml_p152)
*   Local forcing vector [28](#chapter1.xhtml_p28), [75](#chapter3.xhtml_p75), [112](#chapter5.xhtml_p112)
*   Local stiffness matrix [28](#chapter1.xhtml_p28), [75](#chapter3.xhtml_p75), [108](#chapter5.xhtml_p108)

*   Neumann boundary condition [3](#chapter1.xhtml_p3)

*   Orthogonal polynomials [149](#appD.xhtml_p149)
*   Orthogonal projection [5](#chapter1.xhtml_p5)

*   Point coordinates matrix [85](#chapter4.xhtml_p85)
*   Projective method [5](#chapter1.xhtml_p5)

*   Quadrature precision order [145](#appC.xhtml_p145)
*   Quadrature rule [31](#chapter1.xhtml_p31), [34](#chapter1.xhtml_p34)

*   Robin boundary condition [3](#chapter1.xhtml_p3), [70](#chapter3.xhtml_p70)

*   Sparse matrix [42](#chapter2.xhtml_p42)

*   Weak solution [7](#chapter1.xhtml_p7)