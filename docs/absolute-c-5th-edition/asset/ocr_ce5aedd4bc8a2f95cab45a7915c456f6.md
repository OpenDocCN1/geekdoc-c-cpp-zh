# 244 CHAPTER 6 Structures and Classes

EXAMPLES

```
struct StudentRecord
{
    int studentNumber;
    char grade;
}

int main () {
    StudentRecord yourRecord;
    yourRecord.studentNumber = 2001;
    yourRecord.grade = 'A';
}
```

Some writers call the dot operator the structure member access operator, although we will not use that term.

This coincidence of names will produce no problems. For example, if you declare the two structure variables,

+   - FertilizerStock superGrow;
- CropYield apples;

then the quantity of superGrow fertilizer is stored in the member variable superGrow.quantity and the quantity of apples produced is stored in the member variable apples.quantity. The dot operator and the structure variable specify which quantity is meant in each instance.

A value can be viewed as a collection of member values. A structure value can also be viewed as a single (complex) value (that happens to be made up of member values). Since a structure value can be viewed as a single value, structure variables and values can be used in the same ways as you use simple values and simple variables of the predefined types such as int. In particular, you can assign structure values using the equal sign. For example, if apples and oranges are structure values of the type CropYield defined earlier, then the following is perfectly legal:

apples = oranges;

The previous assignment statement is equivalent to

```
apples.quantity = oranges.quantity;
apples.size = oranges.size;
```