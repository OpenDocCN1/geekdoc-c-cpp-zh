
## DE GRUYTER

*Petričă C. Pop*

## GENERALIZED NETWORK DESIGN PROBLEMS

## MODELING AND OPTIMIZATION

## DE GRUYTER SERIES IN DISCRETE MATHEMATICS AND APPLICATIONS

![](img/8ee31706d554c7b9e05caa9ab83aec83_0_0.png)

![](img/8ee31706d554c7b9e05caa9ab83aec83_0_1.png)

## De Gruyter Series in Discrete Mathematics and Applications 1

*Editor*

Colva M. Roney-Dougal, St Andrews, United Kingdom

## Petričă C. Pop

## Generalized Network Design Problems

## Modeling and Optimization

De Gruyter

Mathematics Subject Classification 2010: Primary: 90B10, 90C27, 90C10; Secondary: 68M10, 68T20, 90C11, 78M32, 90C10.

Acknowledgement: This work was supported by a grant of the Romanian National Authority for Scientific Research, CNCS - UEFISCDI, project number PN-II-RU-TE-2011-3-0113.

ISBN 978-3-11-026758-7
e-ISBN 978-3-11-026768-6

Library of Congress Cataloging-in-Publication Data
A CIP catalog record for this book has been applied for at the Library of Congress.

Bibliographic information published by the Deutsche Nationalbibliothek
The Deutsche Nationalbibliothek lists this publication in the Deutsche Nationalbibliografie; detailed bibliographic data are available in the internet at http://dnb.dnb.de.

© 2012 Walter de Gruyter GmbH, Berlin/Boston

Translation: Peter V. Malyshev, Kiev
Typesetting: Da-TeX Gerd Blumenstein, Leipzig, www.da-tex.de
Printing and binding: Hubert & Co. GmbH & Co. KG, Göttingen
© Printed on acid-free paper
Printed in Germany
www.degruyter.com

## Preface

Combinatorial optimization is a fascinating topic. Combinatorial optimization problems arise in a wide variety of important fields such as transportation, telecommunications, computer networking, location, planning, distribution problems, etc. Over the last few decades, important and significant results have been obtained on theory, algorithms and applications.

In combinatorial optimization, many network design problems can be generalized in a natural way by considering a related problem on a clustered graph, where the original problem’s feasibility constraints are expressed in terms of the clusters, i.e. node sets instead of individual nodes. This class of problems is usually referred to as generalized network design problems (GNDPs) or generalized combinatorial optimization problems.

The express purpose of this book is to describe, in a unified manner, a series of mathematical models, methods, propositions and algorithms arising from generalized network design problems, developed in the last years. The book consists of seven chapters. In addition to an introductory chapter, the following generalized network design problems are formulated and examined:

- generalized minimum spanning tree problem;
- generalized traveling salesman problem;
- railway traveling salesman problem;
- generalized vehicle routing problem;
- generalized fixed-charge network design problem;
- generalized minimum vertex-biconnected network problem.

While these topics will be described in the framework of generalized combinatorial optimization problems, my intention was to make each chapter relatively self-contained, so that each can be read separately.

This book will be useful for researchers, practitioners, and graduate students in the fields of operations research, optimization, applied mathematics and computer science. Due to the substantial practical importance of some presented problems, researchers in other areas will also find this book useful.

I am indebted to Georg Still, Gunther Raidl, Walter Kern, Andrei Horbat Marc and to many other colleagues, including my co-authors of the articles cited herein.

Finally, I am especially grateful to my wife Corina and our daughter Ana Maria, for their support throughout the writing of this monograph.

Baia Mare, September 2011

Petričă C. Pop

## Contents

- Preface .................................................................... v
- 1 Introduction ............................................................ 1
- 1.1 Combinatorial optimization and integer programming ............ 1
- 1.2 Complexity theory .................................................... 3
- 1.3 Heuristic and relaxation methods ................................ 5
- 1.4 Generalized network design problems ............................. 7
- 2 The Generalized Minimum Spanning Tree Problem (GMSTP) ........... 9
- 2.1 Definition and complexity of the GMSTP ......................... 10
- 2.2 An exact algorithm for the GMSTP ............................... 12
- 2.3 Mathematical models of the GMSTP ............................... 14
- 2.3.1 Formulations based on tree properties ...................... 14
- 2.3.2 Formulations based on arborescence properties ............ 17
- 2.3.3 Flow based formulations .................................... 19
- 2.3.4 A model based on Steiner tree properties ................. 23
- 2.3.5 Local-global formulation of the GMSTP .................... 24
- 2.4 Approximation results for the GMSTP ............................ 28
- 2.4.1 Introduction ................................................. 29
- 2.4.2 Positive results: the design of the approximation algorithms . 30
- 2.4.3 A negative result for the GMSTP .......................... 32
- 2.4.4 An approximation algorithm for the GMSTP with bounded cluster size .................................... 34
- 2.5 Solving the GMSTP .................................................. 41
- 2.5.1 A branch-and-cut algorithm for solving the GMSTP ......... 42
- 2.5.2 A heuristic algorithm for solving the GMSTP .............. 44
- 2.5.3 Rooting procedure for solving the GMSTP .................. 46
- 2.5.4 Solving the GMSTP with Simulated Annealing ............... 48
- 2.6 Notes ................................................................ 59
- 3 The Generalized Traveling Salesman Problem (GTSP) ................. 60
- 3.1 Definition and complexity of the GTSP .......................... 61
- 3.2 An efficient transformation of the GTSP into the TSP ........... 61
- 3.3 An exact algorithm for the Generalized Traveling Salesman Problem . 63
- 3.4 Integer programming formulations of the GTSP ... 65
- 3.4.1 Formulations based on the properties of Hamiltonian tours ... 65
- 3.4.2 Flow based formulations ... 66
- 3.4.3 A local-global formulation ... 69
- 3.5 Solving the Generalized Traveling Salesman Problem ... 71
- 3.5.1 Reinforcing ant colony system for solving the GTSP ... 72
- 3.5.2 Computational results ... 75
- 3.5.3 A hybrid heuristic approach for solving the GTSP ... 78
- 3.5.4 Computational results ... 88
- 3.6 The drilling problem ... 92
- 3.6.1 Stigmergy and autonomous robots ... 93
- 3.6.2 Sensitive robots ... 94
- 3.6.3 Sensitive robot metaheuristic for solving the drilling problem ... 94
- 3.6.4 Numerical experiments ... 97
- 3.7 Notes ... 99
- 4 The Railway Traveling Salesman Problem (RTSP) ... 100
- 4.1 Definition of the RTSP ... 100
- 4.2 Preliminaries ... 101
- 4.3 Methods for solving the RTSP ... 103
- 4.3.1 The size reduction method through shortest paths ... 103
- 4.3.2 A cutting plane approach for the RTSP ... 111
- 4.3.3 Solving the RTSP via a transformation into the classical TSP ... 114
- 4.3.4 An ant-based heuristic for solving the RTSP ... 119
- 4.4 Dynamic Railway Traveling Salesman Problem ... 121
- 4.4.1 Ant colony approach to the Dynamic RTSP ... 122
- 4.4.2 Implementation details and computational results ... 124
- 4.5 Notes ... 126
- 5 The Generalized Vehicle Routing Problem (GVRP) ... 128
- 5.1 Definition and complexity of the GVRP ... 129
- 5.2 An efficient transformation of the GVRP into a capacitated arc routing problem ... 130
- 5.3 Integer linear programming formulations of the GVRP ... 132
- 5.3.1 A general formulation ... 132
- 5.3.2 A node based formulation ... 135
- 5.3.3 Flow based formulations ... 137
- 5.4 A numerical example ... 139
- 5.5 Special cases of the proposed formulations .................... 141
- 5.5.1 The Generalized multiple Traveling Salesman Problem ....... 141
- 5.5.2 The Generalized Traveling Salesman Problem ............... 143
- 5.5.3 The Clustered Generalized Vehicle Routing Problem ....... 144
- 5.6 Solving the Generalized Vehicle Routing Problem ............ 147
- 5.6.1 An improved hybrid algorithm for Solving the GVRP ....... 147
- 5.6.2 An efficient memetic algorithm for solving the GVRP ..... 154
- 5.6.3 Computational experiments ................................ 159
- 5.7 Notes ........................................................ 165
- 6 The Generalized Fixed-Charge Network Design Problem (GFCNDP) ......... 167
- 6.1 Definition of the GFCNDP ................................... 168
- 6.2 Integer programming formulations of the GFCNDP ............. 169
- 6.3 Solving the GFCNDP ......................................... 173
- 6.4 Computational results ...................................... 175
- 6.5 Notes ........................................................ 177
- 7 The Generalized Minimum Edge-Biconnected Network Problem (GMEBCNP) ...... 178
- 7.1 Definition and complexity of the GMEBCNP ................... 178
- 7.2 A mixed integer programming model of the GMEBCNP ........... 179
- 7.3 Solving the GMEBCNP ........................................ 181
- 7.3.1 Simple Node Optimization Neighborhood (SNON) ............. 181
- 7.3.2 Node Re-Arrangement Neighborhood (NRAN) .................. 182
- 7.3.3 Edge Augmentation Neighborhood ........................... 182
- 7.3.4 Node Exchange Neighborhood ............................... 183
- 7.3.5 Variable Neighborhood Descent ............................ 183
- 7.4 Computational results ...................................... 185
- 7.5 Notes ........................................................ 185
- Bibliography ..................................................... 188
- Index ............................................................ 202
