| To | Do this |

| Call a static method | Write the name of the class, followed by a period, followed by the name of the method. For example: 

Click here to view code image

int pointsCreatedSoFar = Point.ObjectCount(); |

| Declare a static field | Use the keyword static before the type of the field. For example: 
Click here to view code image

```java
class Point
{
    private static int objectCount;
}
``` |

| Declare a const field | Write the keyword const before the declaration of the field and omit the static keyword. For example: 

Click here to view code image

```java
class Math
{
    public const double PI = ...;
}
``` |

| Access a static field | Write the name of the class, followed by a period, followed by the name of the static field. For example: 

Click here to view code image

double area = Math.PI * radius * radius; |