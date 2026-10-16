```
Number subclass: #Complex
    instanceVariableNames:
        'realPart imaginaryPart '
    classVariableNames: ''
    poolDictionaries: ''

realPart: r imaginaryPart: i
    "(Class method.) Answer an instance of class Complex
    and initialize the realPart and imaginaryPart
    instance variables to r and i respectively."
    ^self basicNew realPart: r imaginaryPart: i

realPart: r imaginaryPart: i
    "(Instance method.) Answer the receiver. The
    realPart and imaginaryPart of the receiver are
    set to the r and i arguments respectively."
    realPart := r.
    imaginaryPart := i.
    ^self

imaginaryPart
    "Answer the imaginary part."
    ^imaginaryPart

realPart
    "Answer the real part."
    ^realPart

> aNumber
    "Answer true if receiver is greater than aNumber or false otherwise."
    ^(self realPart > aNumber realPart) realPart or: [
        (self realPart = aNumber realPart) and: [
            self imaginaryPart > aNumber imaginaryPart]]

* aNumber
    "Answer the result of multiplying
    the receiver by aNumber."
    | rp ip |
    rp := self realPart * aNumber realPart -
        self imaginaryPart * aNumber imaginaryPart.
    ip := self realPart * aNumber imaginaryPart +
        self imaginaryPart * aNumber realPart.
    ^self class realPart: rp imaginaryPart: ip
```