

作为参数传递的字符串。方法 `compareTo` 使用词法比较——它比较每个 String 中对应字符的数值。

## String 方法 regionMatches

第 47 行的条件使用 String 方法 `regionMatches` 来比较两个 String 的部分是否相等。第一个参数是调用该方法的 String 中的起始索引。第二个参数是比较用的 String。第三个参数是比较 String 中的起始索引。最后一个参数是两个 String 之间要比较的字符数。该方法仅在指定的字符数词法相等时返回 true。

最后，第 54 行的条件使用 String 方法 `regionMatches` 的五参数版本来比较两个 String 的部分是否相等。当第一个参数为 true 时，该方法会忽略所比较字符的大小写。其余参数与四参数 regionMatches 方法所述的相同。

## String 方法 startsWith 和 endsWith

下一个示例（图 16.4）演示了 String 方法 `startsWith` 和 `endsWith`。方法 `main` 创建包含 "started"、"starting"、"ended" 和 "ending" 的数组 strings。方法 `main` 的其余部分由三个 for 语句组成，用于测试数组的元素是否以或以某个特定字符集结尾。

```
// Fig. 16.4: StringStartEnd.java
// String methods startsWith and endsWith.

public class StringStartEnd
{
   public static void main( String[] args )
   {
      String[] strings = { "started", "starting", "ended", "ending" };

      // test method startsWith
      for ( String string : strings )
      {
         if ( string.startsWith( "st" ) )
            System.out.printf( "\"%s\" starts with \"st\"%n", string );
      } // end for

      System.out.println();

      // test method startsWith starting from position 2 of string
      for ( String string : strings )
      {
         if ( string.startsWith( "art", 2 ) )
            System.out.printf(
               "\"%s\" starts with \"art\" at position 2%n", string );
      } // end for

      System.out.println();
```

图 16.4 | String 方法 startsWith 和 endsWith。（第 1 部分，共 2 部分。）

```
// test method endsWith
for ( String string : strings )
{
    if ( string.endsWith( "ed" ) )
        System.out.printf( "\"%s\" ends with \"ed\"\n", string );
} // end for
} // end main
} // end class StringStartEnd
```

```
"started" starts with "st"
"starting" starts with "st"

"started" starts with "art" at position 2
"starting" starts with "art" at position 2

"started" ends with "ed"
"ended" ends with "ed"
```

第 11–15 行使用仅接受 String 参数的 `startsWith` 方法版本。if 语句（第 13 行）中的条件确定数组中每个 String 是否以字符 "st" 开头。如果是，则方法返回 true，应用程序打印该 String。否则，方法返回 false 且不发生任何事情。

第 20–25 行使用接受 String 和整数作为参数的 startsWith 方法。整数指定在 String 中开始比较的索引。if 语句（第 22 行）中的条件确定数组中每个 String 是否在第三个字符开始处具有字符 "art"。如果是，则方法返回 true，应用程序打印该 String。

第三个 for 语句（第 30–34 行）使用接受 String 参数的 endsWith 方法。第 32 行的条件确定数组中每个 String 是否以字符 "ed" 结尾。如果是，则方法返回 true，应用程序打印该 String。

## 16.3.4 在字符串中定位字符和子字符串

通常很有用在字符串中搜索字符或一组字符。例如，如果你正在创建自己的文字处理器，你可能希望提供搜索文档的功能。图 16.5 演示了 String 方法 **indexOf** 和 **lastIndexOf** 的许多版本，它们在 String 中搜索指定的字符或子字符串。

```
// Fig. 16.5: StringIndexMethods.java
// String searching methods indexOf and lastIndexOf.

public class StringIndexMethods
{
    public static void main( String[] args )
    {
        String letters = "abcdefghijklmnopqrstuvwxyz";
```

```
// test indexOf to locate a character in a string
System.out.printf(
    "'c' is located at index %d\n", letters.indexOf('c') );
System.out.printf(
    "'a' is located at index %d\n", letters.indexOf('a', 1) );
System.out.printf(
    "'$' is located at index %d\n\n", letters.indexOf('$') );

// test lastIndexOf to find a character in a string
System.out.printf( "Last 'c' is located at index %d\n",
    letters.lastIndexOf('c') );
System.out.printf( "Last 'a' is located at index %d\n",
    letters.lastIndexOf('a', 25) );
System.out.printf( "Last '$' is located at index %d\n\n",
    letters.lastIndexOf('$') );

// test indexOf to locate a substring in a string
System.out.printf( "\"def\" is located at index %d\n",
    letters.indexOf("def") );
System.out.printf( "\"def\" is located at index %d\n",
    letters.indexOf("def", 7) );
System.out.printf( "\"hello\" is located at index %d\n\n",
    letters.indexOf("hello") );

// test lastIndexOf to find a substring in a string
System.out.printf( "Last \"def\" is located at index %d\n",
    letters.lastIndexOf("def") );
System.out.printf( "Last \"def\" is located at index %d\n",
    letters.lastIndexOf("def", 25) );
System.out.printf( "Last \"hello\" is located at index %d\n",
    letters.lastIndexOf("hello") );
    } // end main
    } // end class StringIndexMethods
```

```
'c' is located at index 2
'a' is located at index 13
'$' is located at index -1

Last 'c' is located at index 15
Last 'a' is located at index 13
Last '$' is located at index -1

"def" is located at index 3
"def" is located at index 16
"hello" is located at index -1

Last "def" is located at index 16
Last "def" is located at index 16
Last "hello" is located at index -1
```

图 16.5 | String 搜索方法 indexOf 和 lastIndexOf。（第 2 部分，共 2 部分。）

此示例中的所有搜索都在 String letters 上执行（初始化为 "abcdefghijklmnopqrstuvwxyzklm"）。第 11–16 行使用方法 indexOf 来定位 String 中字符的首次出现。如果方法找到该字符，它返回该字符在 String 中的索引——否则，它返回 -1。搜索 String 中字符的 indexOf 有两个版本。第 12 行的表达式使用接受要查找字符的整数表示形式的 indexOf 方法版本。第 14 行的表达式使用另一个 indexOf 方法版本，它接受两个整数参数——字符和搜索 String 应开始的起始索引。

第 19–24 行使用方法 lastIndexOf 来定位 String 中字符的最后一次出现。该方法从 String 的末尾向开头搜索。如果它找到该字符，它返回该字符在 String 中的索引——否则，它返回 -1。搜索 String 中字符的 lastIndexOf 有两个版本。第 20 行的表达式使用接受字符的整数表示形式的版本。第 22 行的表达式使用接受两个整数参数的版本——字符的整数表示形式和向后开始搜索的索引。

第 27–40 行演示了方法 indexOf 和 lastIndexOf 的版本，每个版本都将 String 作为第一个参数。这些版本与前面描述的版本执行相同，只是它们搜索由其 String 参数指定的字符序列（或子字符串）。如果找到子字符串，这些方法返回子字符串中第一个字符在 String 中的索引。

## 16.3.5 从字符串中提取子字符串

类 String 提供了两个 substring 方法，以便通过复制现有 String 对象的部分来创建新的 String 对象。每个方法都返回一个新的 String 对象。两个方法都在图 16.6 中演示。

```
// Fig. 16.6: SubString.java
// String class substring methods.

public class SubString
{
    public static void main( String[] args )
    {
        String letters = "abcdefghijklmabcdefghijklm";

        // test substring methods
        System.out.printf( "Substring from index 20 to end is \"%s\"\n",
            letters.substring( 20 ) );
        System.out.printf( "%s \"%s\"\n",
            "Substring from index 3 up to, but not including 6 is",
            letters.substring( 3, 6 ) );
    } // end main
} // end class SubString
```

从索引 20 到末尾的子字符串是 "hijklm"
从索引 3 起到但不包括 6 的子字符串是 "def"

图 16.6 | String 类 substring 方法。

第 12 行的表达式 letters.substring(20) 使用接受一个整数参数的 substring 方法。参数指定原始

