+   protected:
+   public:
+   }
+   
+   It is also possible to inherit a base class in **protected** mode (known as _protected_ derivation). In protected derivation, both the **public** and **protected** members of the base class become **protected** members of the derived class. Table 8.1 summarizes how the visibility of base class members undergoes modifications in all the three types of derivation.

+   1. A function that is a friend of the class.
+   2. A member function of a class that is a friend of the class.
+   3. A member function of a derived class.

While the friend functions and the member functions of a friend class can have direct access to both the **private** and **protected** data, the member functions of a derived class can directly access only the **protected** data. However, they can access the **private** data through the member functions of the base class. Figure 8.5 illustrates how the access control mechanism works in various situations. A simplified view of access control to the members of a class is shown in Fig. 8.6.

\begin{tabular}{ccccc}
\multicolumn{2}{c}{\multirow{2}{*}{**Base class visibility**}} & \multicolumn{3}{c}{**Derived class visibility**} \\
 & & **Public derivation** & **Private derivation** & **Protected derivation** \\
Private & → & Not inherited & Not inherited & Not inherited \\
Protected & → & Protected & Private & Protected \\
Public & → & Public & Private & Protected \\
\end{tabular}