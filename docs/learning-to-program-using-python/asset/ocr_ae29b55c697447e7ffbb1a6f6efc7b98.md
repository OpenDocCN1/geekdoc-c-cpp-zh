```
```
              plural
              << " of beer," << endl;
      Beer.TakeOneDown();
      cout << "Take one down, pass it around
            ," << endl;
      plural = (int) Beer !=1 ? "s":"";
      cout << (int) Beer << " bottle" <<
              plural
              << " of beer on the wall." << endl
            ;
    }
    }

    catch ( Bottle ) {
      cout << "Go to the store and buy some more
            ," << endl;
      cout << "99 bottles of beer on the wall."
            << endl;
    }

    return 0;
  }
```
```

# ## 3.3 Java

```
```
/**
 * Java 5.0 version of the famous "99 bottles of
 *    beer on the wall".
 * Note the use of specific Java 5.0 features and
 * the strictly correct output.
 *
 * @author kvols
 */
import java.util.*;
class Verse {
    private final int count;
    Verse(int verse) {
      count= 100-verse;
    }
    public String toString() {
```
```