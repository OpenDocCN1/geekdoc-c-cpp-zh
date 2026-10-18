\begin{tabular}{ccc}
Operator ® & Description & Examples \\
"expr"\_expr (C++11) & User-defined literals. & // constexpr for the compile-time constant \\
 &  & constexpr const long double kPi = 3.141592653589793238463; \\
 &  & // User-defined literal - to convert xx\_deg into radians \\
 &  & constexpr long double operator"\_deg ( long double deg ) \\
 &  & { \\
 &  & return deg * kPi / 180.0; \\
 &  & } \\
 &  & void UserTypeConstant_Test( void ) \\
 &  & { \\
 &  & cout << "cos( 30\_deg )=" << cos( 30.0\_deg ) << endl; \\
 &  & } \\
 &  & User-defined literals let us define a custom suffix for selected type literals. Using proper conversions or scaling, a function can be defined. For example, we can write 112\_km + 80\_m with mixed dimensions and still obtain the correct result. In the previous example, using the custom\_deg suffix, it is possible to provide angle values in degrees, instead of radians as expected by trigonometric functions. \\
 &  & In addition, using constexpr in front of the constant and function lets the compiler evaluate them during compilation, rather than at program execution time (Section 7.3). \\
- expr & Unary minus. & double a {}, b {}; \\
+ expr & Unary plus. & // ... \\
 &  & double p = - b / ( + 2.0 * a ); // unary + before the binary * \\
\end{tabular}