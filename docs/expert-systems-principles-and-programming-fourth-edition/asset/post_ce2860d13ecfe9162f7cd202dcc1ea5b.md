
- change management
  - manage change proposals and impact evaluations
  - assign personnel to make changes
  - install new product versions

## Resource Management

- forecast needs for resources
- acquire resources
  - identify expert or knowledge base
  - arrange your schedule for convenience of expert
  - assign responsibilities for optimum use of resources
- provide critical resources to minimize bottlenecks

In particular, note that in the acquisition of resources, the point is made that you should adjust your schedule to that of the expert and not vice versa. Unless you are paying the expert full-time, there will be other duties and their time is very valuable.

Figure 6.2 shows the ideal high-level view of the activities required to produce a system in terms of the stages that a system goes through.

Figure 6.2 General Stages in the Development of an Expert System

| Stage | Description |
| :--- | :--- |
| Feasibility Study | Paper or comparison study to show project is feasible |
| Rapid Prototype | Expert system quickly put together to demonstrate ideas, arouse enthusiasm, and impress upper-level management |
| Refined System (α-test) | In-house verification of the expert system on real problems by knowledge engineers and expert |
| Field Testable (β-test) | System tested by selected users – not knowledge engineers or expert |
| Commercial Quality System | Validated and tested User documentation Training Fast user support by telephone and/or electronic mail |
| Maintenance and Evolution | Fix bugs Enhance capabilities |

In the ideal view, the product is not deployed for end users until all the bugs are worked out. In the case of military products, this is a really good idea since it's not that easy to recall a nuclear missile once it's been launched.

In contrast to government contracts, things are different in the commercial world since there are no guaranteed contracts that pay money on a regular basis, and cost overruns if the project is late. The commercial paradigm followed today is to spend a lot of money on publicity for the product every quarter until it is released several years later. This has two purposes. First, private developers who want to use your product in their products are willing to pay money for pre-release versions even with known bugs. So this provides a continuing source of revenue as the product is being developed instead of your company having to fund all the development costs for several years. A secondary benefit is that you don't need to do much (if any) in-house testing.

Simply make sure that every time the product crashes, it asks the user if it can send an automatic bug report. When the user clicks OK, the message will be automatically sent with diagnostic information as to where the fault occurred. An automatic email program at your company will store the bug report in a database. Standard data mining tools will then look for patterns to notify your particular developer team responsible for a particular aspect of the product. Different trigger levels will be set up so that only when the number of bugs has exceeded their particular trigger level will a notification be sent to the teams. Some teams' work is more important than others so it is not necessary that the same trigger level be used. Depending on the number and severity of the bugs, resources may then be allocated to fix them for the next quarterly release. A special website should be set up for pre-release versions, with a subscription fee charged to access each new quarterly preview version.

Second, and most importantly, the quarterly announcements should be timed to coincide with the quarterly reports to public stockholders required by the Securities and Exchange Commission (SEC) for public companies. Even if you're still private and have not yet released an initial public offering (IPO) of stock, this will attract venture capital to your site and increase the value of your IPO.

## The Delivery Problem

### How will the system be delivered?

Depending on the number of expert systems to be deployed, the delivery problem of the developed systems may be a major factor in development. The delivery problem should be considered in the earliest stage of development. Development systems in the 20th Century cost far more than the system on which the product was to be deployed to end users. Now with low cost machines, that aspect of the delivery problem has been solved.

However, another problem is the wide range of hardware that your product is supposed to run on. This accounted for the initial popularity of Java with their "Write once, use anywhere," slogan and guarantees that applets could only play in the "sandbox." The deployment on different hardware is still a problem unless an interpreter is used and a virtual machine is installed on every different type of hardware. That has worked successfully since bytecode interpreters were introduced with Pascal in the 1970s so that it could run on any microcomputer. This same approach was used by Java.

Although CLIPS does not generate bytecodes, it is designed to produce a standard C version of the finished expert system. This can then be compiled using a standard C compiler for the specific hardware platform and the executable deployed for that particular platform. No “CLIPS Virtual Machine” is required. One of the original design goals of CLIPS was to produce an expert system that could easily be deployed on any new hardware that may arise. If this is not adequate, other versions of CLIPS such as Jess have been developed as mentioned in the Preface. Jess is written in Java and although it does not support multiple inheritance, it has all of the advantages of Java in being easily deployed to different hardware.

In many cases the expert system must be integrated with other existing programs. Consideration should be given to the communication and coordination of the expert system input/output with these programs. It may also be desirable to call the expert system as a procedure from a conventional programming language, and the system should support this. CLIPS is designed so that it can be called from a host language such as a C++ program, do its function, and then return control to the host program. Such a hybrid system was also one of the main design considerations of CLIPS since the performance of an expert system can decrease quickly depending on how many rules are in the system and how much pattern matching must be done. While the Rete Algorithm is good, an expert system is still not as fast as compiled code.

Although you could use CLIPS to simulate a calculator, spreadsheet, or even a word processor, its performance would be not as good as a program written in a third-generation language such as C, C++, or C#. For example, you could create an intelligent data mining tool by calling CLIPS from a standard database such as Oracle or MySQL and return recommendations to the database user. In Oracle, the cursor is designed to let other applications use data and then return control to Oracle. CLIPS follows this same principle of being a good host or a good guest. Another alternative is to use/modify the CLIPS source code and integrate it into your application, then compile the result into a new application for deployment.

## Maintenance and Evolution

### How will the system be maintained and evolve?

The maintenance and evolution of an expert system is more of an open-ended activity than with conventional programs. Because expert systems are not based on algorithms, their performance is dependent on knowledge and expertise. As new knowledge is acquired and old knowledge modified, the performance of the system should ideally remain constant.

However there is a problem in that conventional programs based on algorithms will not have rule conflicts like expert systems. A rule conflict is nothing to be afraid of. In fact that is why inference engines were developed. All a rule conflict means is that more than one rule has matched the pattern on its left-hand-side and can potentially be fired. People do thinking of this type all the time.
