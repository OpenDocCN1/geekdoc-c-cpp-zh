I do not want to cover the API in detail, but here are the highlights that you need to know for processing annotations:

+   - The `RoundEnvironment` gives you a set of all elements annotated with a particular annotation. Call the method
+   
+       `Set<? extends Element> getElementsAnnotatedWith(Class<? extends Annotation> a)`
+   
+   - The source-level equivalent of the `AnnotatedElement` interface is `AnnotatedConstruct`. Use the methods
+   
+       `A getAnnotation(Class<?> annotationType)`
+       `A[] getAnnotationsByType(Class<?> annotationType)`
+   
+     to get the annotation or repeated annotations for a given annotation class.
+   
+   - A `TypeElement` represents a class or interface. The `getEnclosedElements` method yields a list of its fields and methods.
+   
+   - Calling `getSimpleName` on an `Element` or `getQualifiedName` on a `TypeElement` yields a `Name` object that can be converted to a string with `toString`.

# 8.6.3 Using Annotations to Generate Source Code

As an example, we will use annotations to reduce the tedium of implementing `toString` methods. We can't put these methods into the original classes—annotation processors can only produce new classes, not modify existing ones.

Therefore, we'll add all methods into a utility class `ToStrings`:

```
```
public class ToStrings
{
   public static String toString(Point obj)
   {
      Generated code
   }
   public static String toString(Rectangle obj)
   {
      Generated code
   }
   . . .

   public static String toString(Object obj)
   {
      return Objects.toString(obj);
   }
}
```
```

We don't want to use reflection, so we annotate accessor methods, not fields: