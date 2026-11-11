# Listing 12.22 *(Continued)*

```
```c
332    maxsize = (*env)->GetIntField(env, this_obj, id_maxsize);
333    hkey = (*env)->GetIntField(env, this_obj, id_hkey);
334    cret = (char*)malloc(maxsize);

336    /* find the next name */
337    if (RegEnumValue(hkey, index, cret, &maxsize, NULL, NULL, NULL, NULL) != ERROR_SUCCESS)
338    {
339       (*env)->ThrowNew(env, (*env)->FindClass(env, "Win32RegKeyException"),
340          "Enum value failed");
341       free(cret);
342       RegCloseKey(hkey);
343       (*env)->SetIntField(env, this_obj, id_index, count);
344       return NULL;
345    }

348    ret = (*env)->NewStringUTF(env, cret);
349    free(cret);

351    /* increment index */
352    index++;
353    (*env)->SetIntField(env, this_obj, id_index, index);

355    if (index == count) /* at end */
356    {
357       RegCloseKey(hkey);
358    }

360    return ret;
361 }
```
```

# Listing 12.23 `win32reg/Win32RegKeyTest.java`

```
```java
1   import java.util.*;
2
3   /**
4    * @version 1.02 2007-10-26
5    * @author Cay Horstmann
6    */
7   public class Win32RegKeyTest
8   {
9      public static void main(String[] args)
10     {
11        Win32RegKey key = new Win32RegKey(
12           Win32RegKey.HKEY_CURRENT_USER, "Software\\JavaSoft\\Java Runtime Environment");
13
14        key.setValue("Default user", "Harry Hacker");
15     }
16  }
```
```