Below, we document the ST monad from Haskell's Control.Monad.ST library.16

+   • data ST s a

The ST monad allows for destructive updates, but is escapable. A computation of type ST s a returns a value of type a, and execute in “thread” s. It serves to keep the internal states of different invocations of runST separate from each other.

+   • runST :: (forall s. ST s a) -> a

Return the value computed by a state thread. The forall ensures that the internal state used by the ST computation is inaccessible to the rest of the program.

Below, we document the STArray's from Haskell's Data.Array.ST library.17

+   • data STArray s i e

Mutable, boxed, non-strict arrays in the ST monad. s is the state variable argument for the ST type, i is the index type of the array (should be an instance of Ix), and e is the element type of the array.

# C.4. Other

Below, we document the foldMap function from Haskell's Data.Foldable library.18

+   • foldMap :: Monoid m => (a -> m) -> t a -> m

Map each element of the structure into a monoid, and combine the results with (<>). This fold is right-associative and lazy in the accumulator.

Below, we document the ReaderT monad transformer taken from Haskell's Control.Monad.Trans.Reader library.19

+   • newtype ReaderT r m a = ReaderT {runReaderT :: r -> m a}

The reader monad transformer, which adds a read-only environment to the given monad m. The return function ignores the environment, while (>>=) passes the inherited environment to both subcomputations.

# References

+   [1] M. Abadi, P. Barham, J. Chen, Z. Chen, A. Davis, J. Dean, M. Devin, S. Ghemawat, G. Irving, M. Isard, M. Kudlur, J. Levenberg, R. Monga, S. Moore, D.G. Murray, B. Steiner, P.A. Tucker, V. Vasudevan, P. Warden, M. Wicke, Y. Yu, X. Zhang, Tensorflow: a system for large-scale machine learning, CoRR arXiv:1605.08695 (abs) (2016).
+   [2] A.G. Baydin, B.A. Pearlmutter, A.A. Radul, J.M. Siskind, Automatic differentiation in machine learning: a survey, J. Mach. Learn. Res. 18 (1) (2017) 5595–5637.
+   [3] J. Backus, Can programming be liberated from the von neumann style? a functional style and its algebra of programs, Commun. ACM 7 (8) (1964) 463–464, https://doi.org/10.1145/355586.364791.
+   [4] W.K. Clifford, Preliminary sketch of bi-quaternions, Proc. Lond. Math. Soc. 4 (1873) 381–395.
+   [5] R.B. D. de Moor, Algebra of Programming, Prentice-Hall, Inc., USA, 1997.
+   [6] M. Magnagu, Local Rings, Wiley Interscience, 1962.
+   [7] C. Elliott, Denotational design with type class morphisms (extended version), Tech. Rep. 2009-01, LambdaPix, March 2009, http://conal.net/papers/type-class-morphisms/.
+   [8] P. Jansson, C. Ionescu, J.-P. Bernardy, Domain-Specific Languages of Mathematics, Texts in Computing, vol. 24, College Publications, 2022.
+   [9] G. Hutton, A tutorial on the universality and expressiveness of fold, J. Funct. Program. 9 (4) (1999) 355–372, https://doi.org/10.1017/s0956796899003500.
+   [10] R.J.M. Brisard, R. Paterson, Functional programming with bananas, lenses, envelopes and barbed wire, in: Proceedings of the 5th ACM Conference on Functional Programming Languages and Computer Architecture, Springer-Verlag, Berlin, Heidelberg, 1991, pp. 124–144.
+   [11] E. Meijer, Calculating compilers, Ph.D. thesis, Katholieke Universiteit Nijmegen, 1992.
+   [12] F. Kawienc, S. Peyton Jones, N. Krishnaswami, T. Ellis, R.A. Eisenberg, A.W. Higgitt, Probably correct, asymptotically efficient, higher-order reverse-mode automatic differentiation, Proc. ACM Program. Lang. 6 (POPL) (2022) 1–28, https://doi.org/10.1145/3498710.
+   [13] L. Számoki-Kalocs, Higher order functions in automatic differentiation, Numer. Algorithms 72 (3) (2016) 755–811, https://doi.org/10.1007/s11075-015-0067-6, doi.org/10.3311/PP.16341.
+   [14] P.E.H. Harrison, Abstract data types in parametric polymorphism, Numer. Algorithms 72 (3) (2016) 755–811, https://doi.org/10.1007/s11075-015-0067-6, doi.org/10.3311/PP.16341.
+   [15] J. van der Zwaan, G. Hutton, Modern Compiler Algebra, 3rd edition, Cambridge University Press, 2013.
+   [16] A. Gill, G. Hutton, The worker/wrapper transformation, J. Funct. Program. 19 (2) (2009) 227–251, https://doi.org/10.1017/S0956796809007175.
+   [17] C.A.R. Hoare, Proof of correctness of data representations, Acta Inform. 1 (4) (1972) 271–281, https://doi.org/10.1007/BF00289507.
+   [18] P. Wadler, Theorems for free!, in: J. Stoy (Ed.), Proceedings of the Fourth International Conference on Functional Programming Languages and Computer Architecture, 1989, pp. 347–359.
+   [19] J.C. Reynolds, Types, abstraction and parametric polymorphism, in: R.E.A. Mason (Ed.), Information Processing 83, Proceedings of the IFIP 9th World Computer Congress, Paris, France, September 19-23, 1983, North-Holland/IFIP, 1983, pp. 513–523.
+   [20] J.C. Reynolds, Types, abstraction and parametric polymorphism, in: R.E.A. Mason (Ed.), Information Processing 83, Proceedings of the IFIP 9th World Computer Congress, Paris, France, September 19-23, 1983, North-Holland/IFIP, 1983, pp. 513–523.

+   16 https://hackage.haskell.org/package/base-4.18.0.0/docs/Control-Monad-ST.html.
+   17 https://hackage.haskell.org/package/array-0.5.5.0/docs/Data-Array-ST.html.
+   18 https://hackage.haskell.org/package/base-4.18.0.0/docs/Data-Foldable.html.
+   19 https://hackage.haskell.org/package/transformers-0.6.1.0/docs/Control-Monad-Trans-Reader.html.