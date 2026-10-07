The check for a delegate value changes from what is shown in Listing 4.39 to simply

```
PropertyChanged?.Invoke(propertyChanged(this, new PropertyChangedEventArgs(nameof(Name))));
```

Because an event is just a delegate, the sample pattern of invoking a delegate via the null-conditional operator and an Invoke() is always possible.

# Bitwise Operators (<<, >>, |, &, ~)

An additional set of operators that is common to virtually all programming languages is the set of operators for manipulating values in their binary formats: the bit operators.

> BEGINNER TOPIC

# Bits and Bytes

All values in a computer are represented in a binary format of 1s and 0s, called binary digits (bits). Bits are grouped together in sets of eight, called bytes. In a byte, each successive bit corresponds to a value of 2 raised to a power, starting from $2^0$ on the right and moving to $2^7$ on the left, as shown in Figure 4.1.

| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 2⁷ | 2⁶ | 2⁵ | 2⁴ | 2³ | 2² | 2¹ | 2⁰ |

FIGURE 4.1: Corresponding placeholder values

In many scenarios, particularly when dealing with low-level or system services, information is retrieved as binary data. To manipulate these devices and services, you need to perform manipulations of binary data.