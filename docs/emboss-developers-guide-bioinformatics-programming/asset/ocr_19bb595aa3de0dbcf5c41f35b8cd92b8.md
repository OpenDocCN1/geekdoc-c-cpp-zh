# 3.1.4.2 Software life cycle models

The EMBOS developers use a combination of the ‘Code and fix’ and ‘Synchronise and stabilise’ models (see below). This has proved to be the most pragmatic way to keep users happy, especially balancing the requirements for new functionality with that for stability and consistency in the package as a whole.

The general approach is to fix bugs as soon as they are reported and provide bug fix files (see the _EMBOSS User’s Guide_) as required. New features or applications are developed in close collaboration with the users, typically as requested, and are developed and released in a scheduled manner. This is done in as timely a manner as possible allowing for all bugs to be fixed and major issues to be addressed. All bug fixes and requests for features that cannot immediately be implemented are logged on the SourceForge website (see Section 1.5, ‘Contributing software to EMBOS’). In this way valuable contributions are not lost even if they cannot be acted upon immediately.

Many software life cycle models have emerged and all tend to focus on the development process itself. They are summarised below. It is up to you to adopt one of these models (or something else) that is most appropriate to your needs and situation.

# Code and fix model

The simplest model iterates a cycle of coding and bug-fixing until the software is fit for purpose:

+   1. Write source code
+   2. Compile and run program
+   3. Test and find bugs
+   4. Fix bugs.

# Waterfall model

Development proceeds in a linear series of definite management or development steps. The steps might be followed by testing, which must be passed before proceeding to the next step. Typically, return to a previous step is only allowed if a new problem is identified in the existing step. Thus development proceeds incrementally and logically. The drawback, however, is that such models are rather inflexible to changing requirements.

# Spiral model

The spiral model attempts to address the inflexibility of the waterfall model by iterative cycles of development. This introduces more chances for user involvement but the drawback is that the model is rather cumbersome and therefore difficult to stick to in practice. Each cycle has four phases:

+   1. Specification: user requirements, constraints and possible approaches are identified.
+   2. Evaluation: alternative approaches are evaluated, typically through development of prototype software.