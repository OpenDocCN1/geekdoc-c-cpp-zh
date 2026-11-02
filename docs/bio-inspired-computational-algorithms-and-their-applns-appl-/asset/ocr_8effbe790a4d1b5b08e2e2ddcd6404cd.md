Limitations of the genetic programming revealed at the solution of the problem of suitable mathematical equation search, have led to creation of the network operator.

In this work we introduce a new data structure which we called a network operator. Network operator is a directed graph that contains operations, arguments and all information for calculations of mathematical equation.

Network operator method was used for the problems of control synthesis (Diveyev & Sofronova, 2008; Diveev, 2009; Diveev & Sofronova, 2009a,b).

# 2. Program notations of mathematical equations

Mathematical equations consist of variables, parameters, unary and binary operations that form four constructive sets.

Set of variables

X = (x1,...,xN), xi ∈ R^i, i = 1,N. (1)

Set of parameters

Q = (q1,...,qp), qi ∈ R^i, i = 1,P. (2)

Unary operations set

O1 = (ρ1(z)=z, ρ2(z),...,ρW(z)). (3)

Binary operations set

O2 = {χ0(z',z''),...,χV-1(z',z'')}. (4)

Unary operations set must have an identity operation

ρi(z) = z. (5)

Binary operations must be commutative

χi(z',z'') = χi(z'',z'), i = 0,V-1, (6)

associative

χi((z',z''),z''') = χi(z',(z'',z''')), i = 0,V-1, (7)

and have a unit element

∃e_i ⇒ χi(e_i,z) = z, i = 0,V-1. (8)

A program notation of mathematical equation is a notation of equation with the help of constructive sets (1) – (4).