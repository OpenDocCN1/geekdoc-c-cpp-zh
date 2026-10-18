\begin{tabular}{ccc}
**Operator** & **Description** & **Examples** \\
typedd (expr) (C++) & The runtime type identification (RTTI) mechanism; see also Section 6.6.9.2. & void workerFun( void ) ; // function declaration try { workerFun() ; // call some action; can throw an exception } catch( std::exception \& e ) // catch exception \\
typeid ( type ) (C++) & Type identification. & cerr << "Caught: " << e.what() << endl; // find what it is cerr << "Type: " << typeid( e ) .name() << endl; // print to error stream catch( ... ) cerr << "Unknown error" << endl; \\
\end{tabular}