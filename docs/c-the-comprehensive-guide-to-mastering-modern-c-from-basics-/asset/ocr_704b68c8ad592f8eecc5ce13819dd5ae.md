127. Only if you write signed char does it correspond to the Java byte. Java-char corresponds more to C++-short and guaranteed to int16_t. The latter does not have to be present, but it is de facto.

+   - C++optional versus Java-optional
In Java, you often use optional as part of the Java Stream API. In C++, the containers and the new ranges correspond most closely to the Java stream API. However, optional is not a container in C++, and therefore you will not use optional as in Java. However, with C++23 the monadic transformations have been added, which move optional in this direction.

+   - Function objects versus lambdas
At first glance, Java lambdas are similar to C++ lambdas. On closer inspection, the anonymous function objects in C++ are more rounded. In Java, some effort still has to be made at call time in the JVM to dynamically create a function object. In C++, the compiler has completely outsourced the function and only given it an invisible name. Binding to local variables is similar, but in C++ you can choose between binding a value or as a reference.

+   - Values and references in C++ versus Java and the like
Everything that is an object is a reference in Java. In C++, everything is a value and is copied for parameters and returns. Only with special provision with & & * can a function explicitly request references and pointers instead.

+   - Throwing values instead of pointers
In C++, you do not write "throw new X(...)", but only