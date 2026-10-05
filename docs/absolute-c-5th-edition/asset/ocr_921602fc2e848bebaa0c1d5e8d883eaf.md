# Structures 243

Each structure type specifies a list of member names. In Display 6.1 the structure CDAAccountV1 has three member names: balance, interestRate, and term. Each of these member names can be used to pick out one smaller variable that is a part of the larger structure variable. These smaller variables are called member variables. Member variables are specified by giving the name of the structure variable followed by a dot and the member name. For example, if account is a structure of type CDAAccountV1 (as declared in Display 6.1), then the structure variable account has the following three member variables:

member variable

```
account.balance
account.interestRate
account.term
```

The first two member variables are of type double, and the last is of type int. As illustrated in Display 6.1, these member variables can be used just like other variables of those types. For example, the following line from the program in Display 6.1 will add the value to the member variable account.balance and the value contained in the ordinary variable interest and then place the result in the member variable account.balance:

```
account.balance = account.balance + interest;
```

Two or more structure types may use the same member names. For example, it is perfectly legal to have the following two definitions in the same program:

reusing names

```
struct FertilizerStock
{
    double quantity;
    double nitrogenContent;
}
```

and

```
struct CropYield
{
    double quantity;
    double size;
}
```

> The Dot Operator
The dot operator is used to specify a member variable of a structure variable.
SYNTAX
Structure_Variable_Name.Member_Variable_Name