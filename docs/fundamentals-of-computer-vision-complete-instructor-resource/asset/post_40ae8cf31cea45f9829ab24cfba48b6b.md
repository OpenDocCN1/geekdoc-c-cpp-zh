
- C.3 Some Useful IFS Functions 363
- C.4 Common Problems 364
- C.5 Example Programs 364
- Author Index 369
- Subject Index 373

## Preface

This book introduces the fundamental principles of Computer Vision to the advanced undergraduate or first-year graduate student in mathematics, computer science, or engineering.

The book is deliberately informal. The authors attempt to keep the student interested and motivated to continue reading. The student is often addressed directly, as if the student and the authors were in a classroom together. The style is somewhat casual, the authors use the first person frequently, the passive voice is seldom used, and the occasional joke may appear.

The foundations described in the title of this book take two forms: mathematical principles and algorithmic concepts. The principles and concepts are taught together, by describing a computer vision problem, e.g., segmentation, describing an algorithm that could solve that problem, and explaining the mathematical principles underlying the algorithm.

These mathematical principles include

- Linear Operators Taught through a variety of applications, including:
  - Basis Functions Taught through edge detectors
  - Gaussian Convolution Taught through development of Gaussian edge kernels
  - Constrained Optimization Taught through finding optimal edge detection kernels and through principal components
  - The Pseudoinverse Taught through explaining photometric stereo
  - Scale Taught through development of Gaussian edge kernels.
- Nonlinear Operators Taught through mathematical morphology.
- Effects of Sampling Taught by illustrating the use of small kernels for determining orientation.
- Use of Optimization Taught through development of noise removal algorithms, adaptive contours for segmentation and graph cuts.
- Use of Consistency Taught through Hough-like algorithms, through shape matching, and projection onto a manifold.
- Projective Geometry Taught through shape from motion and shape from X algorithms.

These are organized in a progression of levels, moving from pixel-level operations such as noise removal, through edge detection, segmentation, and shape description, and finally to recognition. At each level in the progression, the student learns what specific terminology means, what a good application of the concept to an image does, and one or more approaches to solving the application problem.

Almost all the images used as examples in the book are available for download. When one of these figures is used, the figure caption gives the name of the image.

### What is not included in this book:

The disciplines of statistical pattern recognition and artificial neural networks [0.1] receive only passing mention in this book. This is because both of those disciplines are sufficiently important and sufficiently broad to justify entire courses in themselves.

Also not included are some topics that are of current active research interest. Deep Learning [0.3], for example, is turning out to be of great importance to the eventual success of Computer Vision systems, but such topics are better suited to an advanced topics course, after the students have been introduced to Computer Vision using this book.

We recommend that prior to this book, students have adequate knowledge of image processing [0.2], such that they learn what a pixel is, what the difference is between enhancement and restoration, how to process a color or multi-spectral image, and how to do image processing, preferably in both the spatial domain and the frequency domain, as well as the different filtering approaches.

The student using this book will receive a broad introduction to the field of Computer Vision, which includes reinforcement of many of the requisite mathematical principles.

The book is in four parts:

- **Part I, Preliminaries** touches on biological vision, math, and implementation of algorithms in software.
- **Part II, Preprocessing** discusses the need to “clean up” images before we start the Computer Vision algorithms by removing corruptions due to noise and blur. The need for local area operations such as convolution are included.
- **Part III, Image Understanding** covers segmentation of an image into meaningful regions and representing those regions. Matching of both regions and scenes is included in this part.
- **Part IV, The 2D Image in a 3D World** describes how images of objects may be related to those objects in the observed world.

### Bibliography

- [0.1] R. O. Duda, P. E. Hart, and D. G. Stork. *Pattern Classification*. Wiley Interscience, 2nd edition, 2000.
- [0.2] R. Gonzalez, R. Woods, and L. Eddins. *Digital Image Processing Using MATLAB*. McGraw-Hill, 2nd edition, 2016.
- [0.3] Y. LeCun, Y. Bengio, and G. Hinton. Deep learning. *Nature*, 521(7553), 2015.

## For the Instructor

This is a first course in Computer Vision. It is intended for seniors or first-level graduate students in math-intensive curricula, such as electrical engineering, computer engineering, math, physics, or computer science.

While this book provides a “foundation” in computer vision, a foundation in university-level mathematics is required for this book. We suggest that all students have the usual three-semester course in differential calculus, at least one course in differential equations, and one or two courses in concepts of matrices and linear algebra.

The authors feel strongly that a student in Computer Vision should have a reasonably good grasp of what the computer is actually doing – and that means programming. While MATLAB is a fantastic research tool, and provides wonderful rendering tools, using MATLAB may prevent the student from gaining this insight into the basic operations (unless, of course, the student actually writes MATLAB code and doesn’t use a toolbox). We prefer the student learn and use C or C++.

We have a software package available with which we have had considerable success, described in Appendix C. It can be downloaded for free for MacOSX64, Linux64, and most versions of Windows, along with a lot of images, from www.cambridge.org/9781107184886. This package is, however, not required to use the book. The instructor may choose any software platform, including MATLAB.

One style of teaching this course, the one we usually follow, is to have a number of small projects, roughly a week or two in duration, instead of a single end-of-class project.

In teaching this course, the principal problems we have encountered are with students who don’t know the difference between a compiler and a fishing rod, and students who think an eigenvalue is made with sugar and served with syrup. The emphasis on knowing linear algebra is very important.

We also recommend that prior to taking this course, students take a class in image processing, in which they learn what a pixel is, what restoration does, and the difference between enhancement and filtering.

Our teaching style in this book is deliberately informal. We try to instill in the student the feeling that s/he is in a personal conversation with the book. For that reason, we often use the word “we” rather than the passive voice. We also include the occasional joke or silliness. The occasional smile hopefully will motivate the student to read on.

The authors of this book also wrote an earlier book on computer vision, published by Cambridge University Press in 2004. This text does contain a very small amount of material taken directly from that book.

## Part I

### Preliminaries

In this part of the book, we start getting ready to do Computer Vision (CV). First, we briefly introduce biological vision and the biological motivation of Computer Vision. This is followed by a chapter describing how to write computer programs to process images. We then provide a chapter of math. The emphasis in that chapter is linear algebra, as that is the mathematical discipline most used in CV. We also touch briefly on probability and function minimization.

After we have the human prepared by taking the prerequisites and reviewing the math, we need for that human to know what an image actually is. It turns out that the word “image” has a number of different meanings in different contexts, and Chapter 4 discusses them.
