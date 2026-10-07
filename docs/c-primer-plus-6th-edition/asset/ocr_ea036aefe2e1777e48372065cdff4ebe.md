formatting previously handled by nonmember functions. Also the AcctABC class has two pure virtual functions, so it is, indeed, an abstract class.

# Listing 13.11 acctabc.h

```
// acctabc.h -- bank account classes
#ifndef ACCTABC_H_
#define ACCTABC_H_
#include <iostream>
#include <string>

// Abstract Base Class
class AcctABC
{
private:
    std::string fullName;
    long acctNum;
    double balance;
protected:
    struct Formatting
    {
        std::ios_base::fmtflags flag;
        std::streamsize pr;
    };
    const std::string& FullName() const {return fullName;}
    long acctNum() const {return acctNum;}
    Formatting SetFormatting() const;
    void Restore(Formatting & f) const;
public:
    AcctABC(const std::string& s = "Nullbody", long an = -1,
        double bal = 0.0);
    void Deposit(double amt);
    virtual void Withdraw(double amt) = 0; // pure virtual function
    double Balance() const {return balance;};
    virtual void ViewAcct() const = 0; // pure virtual function
    virtual -AcctABC() {}
};

// Brass Account Class
class Brass :public AcctABC
{
public:
    Brass(const std::string& s = "Nullbody", long an = -1,
        double bal = 0.0) : AcctABC(s, an, bal) { }
    virtual void Withdraw(double amt);
    virtual void ViewAcct() const;
    virtual -Brass() {}
};
```