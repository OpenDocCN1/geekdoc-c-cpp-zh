As with the Requirements and Design Specifications, ideally, the functional model should be executable so as to permit verification with respect to the specification. There are tools tools that will allow us to do this. One such tool is a behavioral Verilog model. UML is also beginning to make executable models a reality.

The functional model is different from the specification and also from the physical architecture that will be developed next. The specification describes the external behavior of the system; functional model targets the internal behavior that will lead to the external. The architectural model addresses the physical hardware and software components onto which the functions are mapped.

In Figure 9.27, we illustrate a first-level decomposition of a simple input/output task. It is important to recognize that the functional decomposition is just that, a hierarchical decomposition; it is not a flow chart. The illustrated decomposition captures and expresses the requirement that the system must support receiving data from and transmitting data to the outside world. Associated with the task, is a required code conversion to ASCII.

![](bbox=[0.27, 0.35, 0.73, 0.55])

Figure 9.27 First-level I/O Task Decomposition

Each of these functions may be further decomposed as necessary. If required, the second-level functions may also be successively refined to give the detail needed to understand and to execute the design.

The next step in the analysis is to identify the messages that flow between the user or other active external objects and the system as well as the internal signals that flow between the major functional blocks. We identify how the user will interact with the system in order to make it do what it is intended to do.

Let's now apply our understanding of partitioning to the functional design of counter system. First and foremost, we must continue to postpone the idea of working with the specific data structures, bits, bytes, microprocessors, or array logics for a while longer. Though important later in the process, at the moment, they limit explorations and can bias the functional decomposition of the system.