4. Assume the classes described in Exercise 3 and consider a main method that contains the following statements:
LandVehicle landVeh;
MotorizedLandVehicle motorVeh;

+   a. Which of these objects can invoke the method wheelCount?

+   b. Which of these objects can invoke the method fuelType?

5. Consider the following classes:

```
class Expr
{
private:
    char Array[MAX_STRING+1];
public:
    ...
    int getLength() const;
    virtual void display() const;
};
// end Expr
class AlgExpr : public Expr
{
public:
    bool isExpression() const;
    bool isBlank(int first, int last) const;
};
// end AlgExpr
class InfixExpr : public AlgExpr
{
public:
    bool isExpression() const;
    int valueOf() const;
    void display() const;
    ...
protected:
    int endFactor(int first, int last) const;
    int endTerm(int first, int last) const;
    int endExpression(int first, int last) const;
private:
    Stack<int> values;
    Stack<char> operators;
};
// end InfixExpr
```

The class AlgExpr represents algebraic expressions, including prefix, postfix, and infix expressions. Its method isExpression simply examines the expression for valid characters but does not consider the order of the characters.

The class InfixExpr represents infix expressions. Its isExpression calls isBlank, and its display calls valueOf.

+   a. Should isBlank be public, protected, or private? Explain.

+   b. If inExpr is an instance of InfixExpr in the main method, can inExpr invoke endExpression? Explain.

+   c. What small change(s) would you make to the classes to ensure that the correct version of isExpression is called?