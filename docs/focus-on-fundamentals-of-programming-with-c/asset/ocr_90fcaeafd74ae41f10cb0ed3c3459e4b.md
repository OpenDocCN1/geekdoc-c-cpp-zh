# Arrays of Structures

Just as we can declare arrays of integers, floats, doubles, etc., we can also declare arrays of structures. For example:

```
#define SIZE 25
typedef struct {
    char name[30];
    float gpa;
    int year;
} Student;
int main(void) {
    Student myClass[SIZE];
    ...
    ...
    return 0;
}
```

This defines an array called myClass that consists of 1000 Student structs. Each element of the array is defined to be of type Student. The array might be illustrated as follows:

| | name | gpa | year |
|---|---|---|---|
| [0] | Haley | 3.75 | 2015 |
| [1] | Sammie | 3.85 | 2016 |
| [2] | Naomi | 3.25 | 2017 |
| ... | ... | ... | ... |
| ... | ... | ... | ... |
| [24] | Garrett | 2.85 | 2019 |