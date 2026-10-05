spend a lot of time debugging the program at run-time. This is due to the fact that in a dynamically typed language variable types frequently change at run-time. Additionally the debugging tools for dynamically typed languages are mediocre.

In the discussion that follows I will use Ruby and Rails as a *bete noire*. Simply because this is the framework with which I have the most experience and this framework has a huge hype behind it. However the discussion applies equally to other frameworks built with dynamically typed languages.

# Performance

There is a dirty little secret concerning web applications built with dynamically typed languages. These applications are very slow and a lot of engineering effort goes into making them run faster. For example, a C++ web application developed in the Dragonon framework:

( https://github.com/dragonframework/dragonon ) is over fifty times faster than a Ruby/Rails application.

See: https://www.techempower.com/benchmarks/#section=data-r19&hw=ph&test=composite

The main culprit is the interpreter in these languages which must read each source code statement (or it's bytecode) before executing the statement.

Also see a comparison of the Dragon webserver with the gold standard in webservers: Nginx.

https://drog.docsforge.com/master/benchmarks/#test-plan-and-