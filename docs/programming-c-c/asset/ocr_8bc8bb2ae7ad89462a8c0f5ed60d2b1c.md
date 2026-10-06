Example:

```
class Student {
    private: // private data member
    int rollno;
    public:
    // public function to get value of rollno - getter
    int getRollNo() {
        return rollno;
    }
    // public function to set value for rollno - setter
    void setRollNo(int i) {
        rollno=i;
    }
}
```

```
int main() {
    Student A;
    A.rollno=1; //Compile time error
    cout<< A.rollno; //Compile time error
    A.setRollNo(1); //Rollno initialized to 1
    cout<< A.getRollNo(); //Output will be 1
}
```

So, this is how we use the private data members of any class using the getter and setter methods.

# Accessing Protected Data Members

Protected data members, can be accessed directly using dot (.) operator inside the subclass of the current class, for non-subclass we will have to follow the steps as to access private data member.