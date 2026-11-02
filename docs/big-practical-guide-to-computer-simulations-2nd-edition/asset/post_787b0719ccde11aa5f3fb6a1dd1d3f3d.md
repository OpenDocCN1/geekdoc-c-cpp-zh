
## BIG PRACTICAL GUIDE TO Computer Simulations
### Second Edition

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_0_0.png)

Alexander K. Hartmann
University of Oldenburg, Germany
World Scientific

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_2_0.png)

Published by
World Scientific Publishing Co. Pte. Ltd.
5 Toh Tuck Link, Singapore 596224
USA office: 27 Warren Street, Suite 401-402, Hackensack, NJ 07601
UK office: 57 Shelton Street, Covent Garden, London WC2H 9HE

British Library Cataloguing-in-Publication Data

A catalogue record for this book is available from the British Library.

BIG PRACTICAL GUIDE TO COMPUTER SIMULATIONS
2nd Edition
Copyright © 2015 by World Scientific Publishing Co. Pte. Ltd.

All rights reserved. This book, or parts thereof, may not be reproduced in any form or by any means, electronic or mechanical, including photocopying, recording or any information storage and retrieval system now known or to be invented, without written permission from the publisher.

For photocopying of material in this volume, please pay a copying fee through the Copyright Clearance Center, Inc., 222 Rosewood Drive, Danvers, MA 01923, USA. In this case permission to photocopy is not required from the publisher.

ISBN 978-981-4571-76-0
ISBN 978-981-4571-77-7 (pbk)

To my family

## Preface to the 2nd edition

After the first edition of this book was published, I received a lot of supporting comments from various people. Nevertheless, many readers recommended some further subjects to be included in the book, in particular related to new developments or tools. Furthermore, several misprints and little mistakes were reported by them. Also, for some paragraphs, I decided to rewrite them a bit or expand them by including more examples. Hence, I did not hesitate for long, when World Scientific asked me to write a second edition. You are holding the result of this effort in your hands.

The main extensions of the second edition are as follows:

- An introduction to the programming language *Python* has been added, see Sec. 2.3. This language is half-way between a script language (since it is interpreted) and a full high-level programming language (it offers, e.g. complex data structures, object-oriented elements and many libraries for various purposes). Thus, when using *Python*, on the one hand it is easy to write scripts for various tasks like data analysis. On the other hand, small to medium size simulation project can be implemented rapidly.
- Since simulation and analysis of *networks and graphs* has become more and more important in various fields of science, the Sec. 6.8 on graphs has been extended by a subsection (6.8.4) on the calculation of the *connected component*. This is one of the most-often performed analyses for graphs and the basis of many complex algorithms, e.g. to obtain shortest paths, diameters, or centrality measures.
- The Sec. 8.1.1 on how to *draw random numbers* for discrete random variables now includes the fastest available algorithm. It allows one to draw each random number according to the given distribution in constant time O(1). This is much faster compared to the standard approach which takes O(log N), where N is the number of the possible outcomes.
- The Sec. 8.2.4 covers the *rejection method*, which allows one to draw random numbers according to a given probability density, usually applied for non-invertible distribution functions. The section has been extended by the general approach to bound the target distribution by arbitrary probability density functions. This enlarges strongly the range of distributions which can be realized by this approach.

    Furthermore, as an example for generating random points in higher dimensions, drawing points uniformly on the surface of *d-dimensional hypersphere* is included now.
- In Chap. 8 on data analysis, in the Sec. 8.5 on hypothesis test and measuring correlations in data sets, a subsection on the *Receiver operating characteristic* (ROC) has been included. The ROC is an advanced yet widespread approach which allows for the determination of optimal parameters for hypothesis tests.
- Furthermore a subsection (8.5.5) on the *principal-component analysis* has been added. This is the simplest approach to search for the most important “directions” in high-dimensional data.
- *Data clustering methods* are an important tool in the analysis of big data sets, since they allow for looking for structure in overwhelming amounts of data. This is a very sophisticated way of data analysis, much beyond the level of averages, histograms and curve fitting. Several approaches, ranging from the most-simple *k-means* method to the advanced hierarchical clustering algorithms are now explained extensively in Sec. 8.5.6.
- The Sec. 8.6.2 on *fitting data* using *gnuplot* has been extended by how to restrict ranges of fitting parameters (which is not possible by default) and how to fit functions to multiple sets of data simultaneously.
- In the first edition, *gnuplot* was only used to generate “quick and dirty” plots of data. In Sec. 9.2.1 it is now shown how one can generate publication-quality plots using *gnuplot*.
- The Sec. 9.2.4 on the ray tracer *POV-Ray* has been extended by some paragraphs which explain how this ray tracer can be used to generate three-dimensional pictures of simulation snapshots.

    By using sequences of such figures, small movies can be generated easily.
- In the first edition, the Sec. 9.3.1 on LaTeX, a standard typesetting tool to generate high-quality documents as large as complete books (like this one), was a rather short introduction giving few examples. For the second edition this section has been expanded substantially, such that it now serves as a complete introduction to LaTeX, presenting the most-frequently used LaTeX elements in scientific publications, such that all necessary knowledge to generate standard to advanced manuscripts (from the typesetting point of view) is covered.

These new sections include and discuss, following the hands-on approach of the first edition, all necessary source codes that the reader can apply the new knowledge to her or his ease as quickly as possible. Thus, I hope that this new edition will allow you to learn all technical aspects of scientific computer simulations as fast as possible, ranging from the initial idea over the implementation, performing the simulations, doing the data analysis, up to the publication of your results. Thus, using this book will save you a lot of time which you can use to concentrate on the actual scientific problem you want to solve. Finally, since the new edition comprises almost all non-problem specific knowledge you need in computational science, I decided to rename the book to “Big Practical Guide to Computer Simulations”.

This new edition would not have been possible without the help of many people. I am grateful to the following persons for communicating mistakes, making useful suggestions and providing extensions of the book: Pia Backmann, Jan Christoph Bernack, Gunnar Claussen, Timo Dewenter, Florian Effenberg, Pascal Fieth, Nikolai Gagunashvili, Hendrike Heidemann, Ivo Inicki, Simon Knowles, Karsten Looschen, Markus Manssen, Andreas Mohrs, Zacharias Njam Mokom, Oliver Melchert, Marc Mézard, Tudor Mitran, Christoph Norrenbrock, Tom Seren, Hendrik Schawe, Sagar Sinha, Verena Sterr, Sebastian von Ohr, and A. Peter Young. Furthermore, Oliver Melchert provided a Python script for data resampling which is included in the new edition.

Alexander K. Hartmann
Oldenburg, July 2014

## Preface to the 1st edition

You have decided to become an expert in computer simulations, congratulations! This is a good decision, because computational and simulation methods become more and more important in all areas of science, humanities, economics, engineering and mathematics. This book will help you a great deal in learning the most important basics which you need during all phases of a simulation research project, from the phases of program design, implementation, and debugging, through running the simulations, organizing the data and analyzing the results, to the final phase where you want to present and publish your results.

Note that nowadays thousands of different problems exist which are being investigated by computer simulations. One studies, for example, the diffusion of chemicals in soils, the folding of proteins in cells, the communication of neurons in the brain, the deformation of cars in accidents, the behavior of brokers working at the stock market, the evolution of the weather during the next days or weeks, the turbulent behavior of flowing water in a turbine, the movement of electrons in semiconductors, the patterns of words in languages, or the traffic of pedestrians in crowded shopping malls, to name only a few. Consequently, there are many algorithms to treat the variety of problems, for example, finite differences, finite elements, integration methods, matrix inversion, eigenvalue determination, equation solvers, molecular dynamics simulations, Monte Carlo methods, density functional approaches, graph algorithms, optimization methods, and so on. Which methods are suitable for your problems depends heavily on the problems you want to solve. Since there are way too many algorithms available for all these different problems, and because everybody needs usually a different
