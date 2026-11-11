
- 15.6.5 Rasterizing Shadows ...... 428
- 15.6.6 Beyond the Bounding Box ...... 429
- **15.7 Rendering with a Rasterization API** ...... 432
  - 15.7.1 The Graphics Pipeline ...... 432
  - 15.7.2 Interface ...... 434
- **15.8 Performance and Optimization** ...... 444
  - 15.8.1 Abstraction Considerations ...... 444
  - 15.8.2 Architectural Considerations ...... 444
  - 15.8.3 Early-Depth-Test Example ...... 445
  - 15.8.4 When Early Optimization Is Good ...... 446
  - 15.8.5 Improving the Asymptotic Bound ...... 447
- **15.9 Discussion** ...... 447
- **15.10 Exercises** ...... 449

## 16 Survey of Real-Time 3D Graphics Platforms ...... 451

There is great diversity in the feature sets and design goals among 3D graphics platforms. Some are thin layers that bring the application as close to the hardware as possible for optimum performance and control; others provide a thick layer of data structures for the storage and manipulation of complex scenes; and at the top of the power scale are the game-development environments that additionally provide advanced features like physics and joint/skin simulation. Platforms supporting games render with the highest possible speed to ensure interactivity, while those used by the special effects industry sacrifice speed for the utmost in image quality. We present a broad overview of modern 3D platforms with an emphasis on the design goals behind the variations.

- **16.1 Introduction** ...... 451
  - 16.1.1 Evolution from Fixed-Function to Programmable Rendering Pipeline ...... 452
- **16.2 The Programmer's Model: OpenGL Compatibility (Fixed-Function) Profile** ...... 454
  - 16.2.1 OpenGL Program Structure ...... 455
  - 16.2.2 Initialization and the Main Loop ...... 456
  - 16.2.3 Lighting and Materials ...... 458
  - 16.2.4 Geometry Processing ...... 458
  - 16.2.5 Camera Setup ...... 460
  - 16.2.6 Drawing Primitives ...... 461
  - 16.2.7 Putting It All Together—Part 1: Static Frame ...... 462
  - 16.2.8 Putting It All Together—Part 2: Dynamics ...... 463
  - 16.2.9 Hierarchical Modeling ...... 463
  - 16.2.10 Pick Correlation ...... 464
- **16.3 The Programmer's Model: OpenGL Programmable Pipeline** ...... 464
  - 16.3.1 Abstract View of a Programmable Pipeline ...... 464
  - 16.3.2 The Nature of the Core API ...... 466
- **16.4 Architectures of Graphics Applications** ...... 466
  - 16.4.1 The Application Model ...... 466
  - 16.4.2 The Application-Model-to-IM-Platform Pipeline (AMIP) ...... 468
  - 16.4.3 Scene-Graph Middleware ...... 474
  - 16.4.4 Graphics Application Platforms ...... 477
- **16.5 3D on Other Platforms** ...... 478
  - 16.5.1 3D on Mobile Devices ...... 479
  - 16.5.2 3D in Browsers ...... 479
- **16.6 Discussion** ...... 479

## 17 Image Representation and Manipulation ...... 481

Much of graphics produces *images* as output. We describe how images are stored, what information they can contain, and what they can represent, along with the importance of knowing the precise meaning of the pixels in an image file. We show how to composite images (i.e., blend, overlay, and otherwise merge them) using coverage maps, and how to simply represent images at multiple scales with MIP mapping.

- 17.1 Introduction ...... 481
- 17.2 What Is an Image? ...... 482
  - 17.2.1 The Information Stored in an Image ...... 482
- 17.3 Image File Formats ...... 483
  - 17.3.1 Choosing an Image Format ...... 484
- 17.4 Image Compositing ...... 485
  - 17.4.1 The Meaning of a Pixel During Image Compositing ...... 486
  - 17.4.2 Computing *U* over *V* ...... 486
  - 17.4.3 Simplifying Compositing ...... 487
  - 17.4.4 Other Compositing Operations ...... 488
  - 17.4.5 Physical Units and Compositing ...... 489
- 17.5 Other Image Types ...... 490
  - 17.5.1 Nomenclature ...... 491
- 17.6 MIP Maps ...... 491
- 17.7 Discussion and Further Reading ...... 492
- 17.8 Exercises ...... 493

## 18 Images and Signal Processing ...... 495

The pattern of light arriving at a camera sensor can be thought of as a function defined on a 2D rectangle, the value at each point being the light energy density arriving there. The resultant image is an array of values, each one arrived at by some sort of averaging of the input function. The relationship between these two functions—one defined on a continuous 2D rectangle, the other defined on a rectangular grid of points—is a deep one. We study the relationship with the tools of Fourier analysis, which lets us understand what parts of the incoming signal can be accurately captured by the discrete signal. This understanding helps us avoid a wide range of image problems, including “jaggies” (ragged edges). It’s also the basis for understanding other phenomena in graphics, such as moiré patterns in textures.

- 18.1 Introduction ...... 495
  - 18.1.1 A Broad Overview ...... 495
  - 18.1.2 Important Terms, Assumptions, and Notation ...... 497
- 18.2 Historical Motivation ...... 498
- 18.3 Convolution ...... 500
- 18.4 Properties of Convolution ...... 503
- 18.5 Convolution-like Computations ...... 504
- 18.6 Reconstruction ...... 505
- 18.7 Function Classes ...... 505
- 18.8 Sampling ...... 507
- 18.9 Mathematical Considerations ...... 508
  - 18.9.1 Frequency-Based Synthesis and Analysis ...... 509
- 18.10 The Fourier Transform: Definitions ...... 511
- 18.11 The Fourier Transform of a Function on an Interval ...... 511
  - 18.11.1 Sampling and Band Limiting in an Interval ...... 514
- 18.12 Generalizations to Larger Intervals and All of R ...... 516
- 18.13 Examples of Fourier Transforms ...... 516
  - 18.13.1 Basic Examples ...... 516
  - 18.13.2 The Transform of a Box Is a Sinc ...... 517
  - 18.13.3 An Example on an Interval ...... 518
- 18.14 An Approximation of Sampling ...... 519
- 18.15 Examples Involving Limits ...... 519
  - 18.15.1 Narrow Boxes and the Delta Function ...... 519
  - 18.15.2 The Comb Function and Its Transform ...... 520
- 18.16 The Inverse Fourier Transform ...... 520
- 18.17 Properties of the Fourier Transform ...... 521
- 18.18 Applications ...... 522
  - 18.18.1 Band Limiting ...... 522
  - 18.18.2 Explaining Replication in the Spectrum ...... 523
- 18.19 Reconstruction and Band Limiting ...... 524
- 18.20 Aliasing Revisited ...... 527
- 18.21 Discussion and Further Reading ...... 529
- 18.22 Exercises ...... 532

## 19 Enlarging and Shrinking Images ...... 533

We apply the ideas of the previous two chapters to a concrete example—enlarging and shrinking of images—to illustrate their use in practice. We see that when an image, conventionally represented, is shrunk, problems will arise unless certain high-frequency information is removed before the shrinking process.

- 19.1 Introduction ...... 533
- 19.2 Enlarging an Image ...... 534
- 19.3 Scaling Down an Image ...... 537
- 19.4 Making the Algorithms Practical ...... 538
- 19.5 Finite-Support Approximations ...... 540
  - 19.5.1 Practical Band Limiting ...... 541
- 19.6 Other Image Operations and Efficiency ...... 541
- 19.7 Discussion and Further Reading ...... 544
- 19.8 Exercises ...... 545

## 20 Textures and Texture Mapping ...... 547

Texturing, and its variants, add visual richness to models without introducing geometric complexity. We discuss basic texturing and its implementation in software, and some of its variants, like bump mapping and displacement mapping, and the use of 1D and 3D textures. We also discuss the creation of texture correspondences (assigning texture coordinates to points on a mesh) and of the texture images themselves, through techniques as varied as “painting the model” and probabilistic texture-synthesis algorithms.

- 20.1 Introduction ...... 547
- 20.2 Variations of Texturing ...... 549
