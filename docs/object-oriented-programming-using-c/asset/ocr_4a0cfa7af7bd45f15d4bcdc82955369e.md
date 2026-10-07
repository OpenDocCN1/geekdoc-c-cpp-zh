# Object Oriented Programming using C#

# The Unified Modelling Language (UML)

+   - Relationships
  - navigability
  - multiplicity
  - dependency
  - aggregation
  - composition

+   - Generalization / specialization
  - inheritance
  - interfaces

+   - Keywords
- Notes and Comments

# 2.3 UML Syntax

As UML diagrams convey precise information there is a precise syntax that should be followed.

Attributes should be shown as: *visibility name : type multiplicity*

Where visibility is one of :-

+   - + public
- - private
- # protected
- ~ package

and Multiplicity is one of :-

+   - n exactly n
- * zero or more
- m..n between m and n

The following are examples of attributes correctly specified using UML :-

+   - custRef : int [1]

a private attribute custRef is a single int value this would often shown as - **custRef : int** However with no multiplicity shown we cannot safely assume a multiplicity of one was intended by the author.

# # itemCodes : String [1..]

a protected attribute itemCodes is one or more String values

# validCard : boolean

an attribute validCard, of unspecified visibility, has unspecified multiplicity