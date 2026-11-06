# LISTING 4-3: *(continued)*

```
```cpp
    int GetDiamondWeight() {
        return Weight;
    }
};

class Jade : public Rock {
public:
    void SetJadeWeight(int newweight) {
        Weight = newweight;
    }

    int GetJadeWeight() {
        return Weight;
    }
};

class MeltedMess : public Diamond, public Jade {
};

int main(int argc, char *argv[])
{
    MeltedMess mymess;
    mymess.SetDiamondWeight(10);
    mymess.SetJadeWeight(20);

    cout << mymess.GetDiamondWeight() << endl;
    cout << mymess.GetJadeWeight() << endl;
    return 0;
}
```
```

One member is called Weight, and it’s part of Rock. The Jade and Diamond classes include two accessor methods, one to set the value of Weight and one to get it.

The MeltedMess class derives from both Diamond and Jade. The code creates an instance of MeltedMess and calls the four methods that access the supposedly single Weight member in Rock. The code calls the accessor for Diamond, setting Weight to 10. Then it calls the one for Jade, setting Weight to 20.

In a perfect world, in which each object only has one Weight, this would have first set the Weight to 10 and then to 20. When you print it, you should see 20 both times. But you don’t: