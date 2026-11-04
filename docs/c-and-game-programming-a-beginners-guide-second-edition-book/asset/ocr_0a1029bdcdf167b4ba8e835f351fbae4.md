```
public static void Test(object ob) {
    TestClass test;
    if (ob is TestClass) {
        test = (TestClass)ob;
    }
}
public static void Main() {}
}
```

# lock

A lock is a temporary, mutual exclusion used to ensure that multiple threads do not inadvertently access the same section of coding. Locks are used with the this statement and the typeof command, and are written as: lock (expression) executable block. Note: lock statements also require that their expressions be referenced types (see Example B.38).

# Example B.38.

```
namespace Appendix_B {
    class MyName {
        private string name;
        protected MyName(string fn) {this.name = fn;}
        protected string TestName(string fn) {
            lock (this) {
                if (fn != null) {
                    return (this.name);
                }
            }
            return(null);
        }
        public static void Main() {}
    }
}
```

# long

Long is a 64-bit data type used to store values ranging from −9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 (see Example B.39).