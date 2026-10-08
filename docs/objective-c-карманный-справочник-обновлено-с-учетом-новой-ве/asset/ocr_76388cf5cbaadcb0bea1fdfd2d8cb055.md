# CHAPTER 1: The Objective-C Philosophy

spectrum, with little by way of encapsulation, no dynamic dispatch, but with one big advantage: It was fast.

C was based heavily on the PDP-11 instruction set. A very naive C compiler could produce quite fast code. This is true even today. Compilers such as LLVM, XLC, and ICC put a lot of effort into optimization, but PCC, which does almost none, still produces reasonably fast code.

Brad Cox and Tom Love use StepStone in 1986, selling a product based on Brad's earlier Object Oriented Precompiler. This product, Objective-C, was a preprocessor and a small Objective-C runtime library. The preprocessor generated C code that you could compile with your platform's C compiler. As recently as 2010, I came across a company still using the StepStone compiler in a commercial product.

In 1988, NeXT bought a license to StepStone code and bought the Objective-C trademark outright. NeXT then rewrote the preprocessor as a front end to the GNU Compiler Collection (GCC). After some legal wrangling, the Free Software Foundation forced them to release this code, but they kept the runtime library private. The GNU project then wrote a replacement for the runtime library, but made some changes. One was that selectors in the GNU runtime had a type associated with them. On NeXT (and Apple) platforms, selectors are just strings.