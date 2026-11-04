```
account = account1;
account = account2;
}
}
```

# Reading and Writing to Private Members

Encapsulation is a key point when working with private members, but for varying reasons we often find that we need to gain at least limited access in order to implement changes within our programs. These changes can be facilitated with the use of specialized member functions. Practically, these functions are usually broken up into two forms: the first to read (compare, get) those values, and the second to set (put, write) or alter those values. Typically, the setting functions are void, while the reading functions are meant to return the implied value. Both are usually only used to access one class member, but several equivalent member functions may be written to include as many members as required (see Example 5.24).

# Example 5.24. Reading and writing to private members.

```
public decimal ReadInterestRate() {
    return(InterestRate);
}

public void SetInterestRate(decimal IRate) {
    InterestRate = IRate;
}
```

# The Keyword this

The keyword this is a specialized reference signature used to indicate the referencing object of a passing class, therefore, this is a longhand version for the otherwise abbreviated member. While the this reference is implied, its definitions can become ambiguous and should be included to prevent this error (see Examples 5.25 and 5.26).