# Testing strategy

Execution testing can provide a detailed assessment of a product’s reliability. Part of quality assurance is developing a test strategy in conjunction with the product requirements, architecture, and design. Developers on many projects rely on testing as the primary method of both quality assessment and quality improvement. The rest of this chapter demonstrates in more detail that this is too heavy a burden for testing to bear by itself.

Cross-Reference For details on testing, see Chapter 22, "Developer Testing."

# Software-engineering guidelines

Guidelines should control the technical character of the software as it’s developed. Such guidelines apply to all software development activities, including problem definition, requirements development, architecture, construction, and system testing. The guidelines in this book are, in one sense, a set of software-engineering guidelines for construction.

Cross-Reference For a discussion of one class of software-engineering guidelines appropriate for construction, see Section 4.2, "Programming Conventions."

# Informal technical reviews

Many software developers review their work before turning it over for formal review. Informal reviews include desk-checking the design or the code or walking through the code with a few peers.

# Formal technical reviews

One part of managing a software-engineering process is catching problems at the "lowest-value" stage—that is, at the time at which the least investment has been made and at which problems cost the least to correct. To achieve such a goal, developers use "quality gates," periodic tests or reviews that determine whether the quality of the product at one stage is sufficient to support moving on to the next. Quality gates are usually used to transition between requirements development and architecture, architecture and construction, and construction and system testing. The "gate" can be an inspection, a peer review, a customer review, or an audit.

Cross-Reference Reviews and inspections are discussed in Chapter 21, "Collaborative Construction."

A "gate" does not mean that architecture or requirements need to be 100 percent complete or frozen; it does mean that you will use the gate to determine whether the requirements or architecture are good enough to support downstream development. "Good enough" might mean that you’ve sketched out the most critical 20 percent of the requirements or architecture, or it might mean you’ve specified 95 percent in excruciating detail—which end of the scale you should aim for depends on the nature of your specific project.

Cross-Reference For more details on how development approaches vary depending on the kind of project, see Section 3.2, "Determine the Kind of Software You’re Working On."

# External audits

An external audit is a specific kind of technical review used to determine the status of a project or the quality of a product being developed. An audit team is brought in from outside the organization and reports its findings to whoever commissioned the audit, usually management.

# Development Process

Further Reading For a discussion of software development as a process, see Professional Software Development (McConnell 1994).

Each of the elements mentioned so far has something to do explicitly with assuring software quality and implicitly with the process of software development. Development efforts that include quality-assurance activities produce better software than those that do not. Other processes that aren’t explicitly quality-assurance activities also affect software quality.