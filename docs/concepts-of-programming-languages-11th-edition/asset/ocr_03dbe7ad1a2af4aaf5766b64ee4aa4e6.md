```
```java
// A class to define the method that dynamically calls the
// methods of a passed class object
class Reflect {
    public static void callDraw(Object birdObj) {
        Class cls = birdObj.getClass();
        try {
            // Find the draw method of the given class
            Method method = cls.getMethod("draw");
            // Dynamically call the method
            method.invoke(birdObj);
        }
        // In case the given class does not support draw
        catch (NoSuchMethodException e) {
            throw new IllegalArgumentException(
                cls.getName() + "does not support draw");
        }
        // In case the callDraw cannot call draw
        catch (IllegalAccessException e) {
            throw new IllegalArgumentException(
                "Insufficient access permissions to call" +
                "draw in class " + cls.getName());
        }
        // In case draw throws an exception
        catch (InvocationTargetException e) {
            throw new RuntimeException(e);
        }
    }
}

class Bird1 {
    public void draw() {
        System.out.println("This is draw from Bird1");
    }
}

class Bird2 {
    public void draw() {
        System.out.println("This is draw from Bird2");
    }
}

class Bird3 {
    public void draw() {
        System.out.println("This is draw from Bird3");
    }
}
```
```

The output of this program is as follows:

```
```text
This is the draw from Bird3
This is the draw from Bird1
This is the draw from Bird2
```
```