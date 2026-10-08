# 1.3 Algorithms and Program Development

developing a computerized solution to a problem is to develop an algorithm to solve the problem. At the same time, the algorithm must filter out inappropriate data.

#  1.3.1 Concept of an Algorithm

An algorithm is a procedure consisting of a finite number of precisely defined steps for solving a problem. Each step of an algorithm must be an unambiguous instruction which, when written in a computer language, can be executed by a computer. The order of the steps is critical, because most computers execute steps in the order in which they are presented. An algorithm must terminate whether not the task is completely successfully executed. That, it must recognize the end of the input data and when an answer is sufficiently accurate. Algorithms that monitor the weather, automatic teller machines, and nuclear reactors are continuously active. These types of algorithms are apparent exceptions to the termination requirement. However, they idle as they continuously poll input devices and are normally reactivated as needed.

> Programming Warning: Every step in the algorithm must be clear and precise and the algorithm must terminate.

Programmers should choose an algorithm on the basis of efficiency, reliability, and clarity. Algorithms should be efficient with respect to computational time, storage requirements, and response time. The degree of accuracy required is specified by the user. An algorithm is reliable when it consistently produces answers from valid data and rejects invalid data. Clarity means that an understandable programming style is used. Clarity should not be compromised. However, sometimes a compromise between the other factors is necessary. For example, efficiency may be sacrificed for the sake of a high degree of reliability.

The design of algorithms to solve simple problems can be straightforward, but design of algorithms for large, complex problems can be difficult and time consuming. Although this can only deal with simple problems, the techniques we use are important in the design of algorithms for complex problems.

One common approach to large and complex problems is to use top-down design. Top-down design starts at the top of the structure with a general statement of the problem written in a precise, formal way to provide a high-level specification of the algorithm. This is divided into separate logical parts and a