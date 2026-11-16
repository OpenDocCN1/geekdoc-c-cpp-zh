# # Fuzzy Sets and Natural Language

The traditional way of representing which objects are members of a set is in terms of a characteristic function, sometimes called a discrimination function. If an object is an element of a set, then its characteristic function is 1. If an object is not an element of a set, then its characteristic function is 0. This definition is summarized by the following characteristic function:

```
\mu_A(x) = \begin{cases} 1 \text{ if } x \text{ is an element of set A} \\ 0 \text{ if } x \text{ is not an element of set A} \end{cases}
```

where the objects x are elements of some universe X (Ross 04).

The characteristic function can also be defined in terms of a functional mapping (see Section 1.10 on Functional Programming):

```
\mu_A(x) : X \rightarrow \{0,1\}
```

which states that the characteristic function maps a universal set X to the set consisting of 0 and 1. This definition simply expresses the classical concept that an object is either in a set or not in a set. Sets to which this applies are called crisp sets, in contrast to fuzzy sets. This type of thinking dates from the Aristotelian view of bivalent logic or two-valued logic, in which true and false are the only possibilities.

# Table 5.7 Some Applications of Fuzzy Theory

| Application |
|---|
| Control Algorithms |
| Medical Diagnosis |
| Decision Making |
| Economics |
| Engineering |
| Environmental |
| Literature |
| Operations Research |
| Pattern Recognition |
| Psychology |
| Reliability |
| Security |
| Science |

Unlike traditional or classical logic which attempts to categorize information into binary patterns such as black / white, true / false, yes / no, or all / nothing, fuzzy logic pays attention to the “excluded middle” and tries to account for the “grays,” the partially true and partially false situations which make up most human reasoning in everyday life. It builds upon the assumption that everything consists of degrees on a sliding scale—whether it be truth, age, beauty, wealth,