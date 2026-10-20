

Enter a sentence and press Enter
This is a sentence with seven tokens
Number of elements: 7
The tokens are:
This
is
a
sentence
with
seven
tokens

Fig. 16.18 | StringTokenizer object used to tokenize strings. (Part 2 of 2.)

## 16.7 正则表达式、类 Pattern 和类 Matcher

正则表达式是一个描述用于匹配其他字符串中字符的搜索模式的字符串。此类表达式可用于验证输入并确保数据符合特定格式。例如，邮政编码必须由五位数字组成，而姓氏只能包含字母、空格、撇号和连字符。正则表达式的一种应用是促进编译器的构建。通常，使用大型且复杂的正则表达式来验证程序的语法。如果程序代码与正则表达式不匹配，编译器就知道代码中存在语法错误。

类 String 提供了用于执行正则表达式操作的多个方法，其中最简单的是匹配操作。String 方法 matches 接收一个指定正则表达式的字符串，并将调用它的 String 对象的内容与正则表达式进行匹配。该方法返回一个布尔值，表示匹配是否成功。

正则表达式由字面字符和特殊符号组成。图 16.19 指定了一些可与正则表达式一起使用的预定义字符类。字符类是表示一组字符的转义序列。数字是任何数字字符。单词字符是任何字母（大写或小写）、任何数字或下划线字符。空白字符是空格、制表符、回车符、换行符或换页符。每个字符类匹配我们尝试用正则表达式匹配的字符串中的单个字符。

正则表达式不限于这些预定义的字符类。表达式采用各种运算符和其他形式的记法来匹配复杂的模式。

| Character | Matches | Character | Matches |
|---|---|---|---|
| \d | any digit | \D | any nondigit |
| \w | any word character | \W | any nonword character |
| \s | any white-space character | \S | any nonwhite-space character |

Fig. 16.19 | Predefined character classes.

// Fig. 16.21: Validate.java
// Validate user information using regular expressions.
import java.util.Scanner;

public class Validate
{
    public static void main( String[] args )
    {
        // get user input
        Scanner scanner = new Scanner( System.in );
        System.out.println( "Please enter first name:" );
        String firstName = scanner.nextLine();
        System.out.println( "Please enter last name:" );
        String lastName = scanner.nextLine();
        System.out.println( "Please enter address:" );
        String address = scanner.nextLine();
        System.out.println( "Please enter city:" );
        String city = scanner.nextLine();
        System.out.println( "Please enter state:" );
        String state = scanner.nextLine();
        System.out.println( "Please enter zip:" );
        String zip = scanner.nextLine();
        System.out.println( "Please enter phone:" );
        String phone = scanner.nextLine();

        // validate user input and display error message
        System.out.println( "\nValidate Result:" );

        if ( !ValidateInput.validateFirstName( firstName ) )
            System.out.println( "Invalid first name" );
        else if ( !ValidateInput.validateLastName( lastName ) )
            System.out.println( "Invalid last name" );
        else if ( !ValidateInput.validateAddress( address ) )
            System.out.println( "Invalid address" );
        else if ( !ValidateInput.validateCity( city ) )
            System.out.println( "Invalid city" );
        else if ( !ValidateInput.validateState( state ) )
            System.out.println( "Invalid state" );
        else if ( !ValidateInput.validateZip( zip ) )
            System.out.println( "Invalid zip code" );
        else if ( !ValidateInput.validatePhone( phone ) )
            System.out.println( "Invalid phone number" );
        else
            System.out.println( "Valid input.  Thank you." );
    } // end main
} // end class Validate

Please enter first name:
Jane
Please enter last name:
Doe
Please enter address:
123 Some Street

Please enter city:
**Some City**
Please enter state:
**SS**
Please enter zip:
123
Please enter phone:
**123-456-7890**

Validate Result:
Invalid zip code

Please enter first name:
Jane
Please enter last name:
**Doe**
Please enter address:
**123 Some Street**
Please enter city:
**Some City**
Please enter state:
**SS**
Please enter zip:
12345
Please enter phone:
**123-456-7890**

Validate Result:
Valid input. Thank you.

Fig. 16.21 | Inputs and validates data from user using the ValidateInput class. (Part 2 of 2.)

Figure 16.20 validates user input. Line 9 validates the first name. 要匹配没有预定义字符类的字符集，请使用方括号，[]。例如，模式 "[aeiou]" 匹配单个元音字符。字符范围是通过在两个字符之间放置连字符 (-) 表示的。在示例中，"[A-Z]" 匹配单个大写字母。如果方括号中的第一个字符是 "^"，则表达式接受除所指示字符之外的任何字符。然而，"[^Z]" 与 "[A-Y]" 不同，后者匹配大写字母 A—Y——"[^Z]" 匹配除大写 Z 之外的任何字符，包括小写字母和非字母字符，例如换行符。字符类中的范围由字母的整数值决定。在此示例中，"[A-Za-z]" 匹配所有大写和小写字母。范围 "[A-z]" 匹配所有字母，还匹配那些整数值介于大写 Z 和小写 a 之间的字符（例如 [ 和 ]）【有关字符整数值的更多信息，请参阅附录 B】。与预定义的字符类一样，由方括号分隔的字符类匹配搜索对象中的单个字符。

在第 9 行，第二个字符类之后的星号表示可以匹配任意数量的字母。一般来说，当正则表达式运算符 "*" 出现在正则表达式中时，应用程序会尝试匹配紧跟在 "*" 之前的子表达式的零个或多个出现。运算符 "+" 尝试匹配紧跟在 "+" 之前的子表达式的一个或多个出现。因此，"A*" 和 "A+" 都将匹配 "AAA" 或 "A"，但只有 "A*" 会匹配空字符串。

如果方法 validateFirstName 返回 true（图 16.21 的第 29 行），应用程序将尝试通过调用 validateLastName（图 16.20 的第 13–16 行）来验证姓氏（第 31 行）。用于验证姓氏的正则表达式匹配由空格、撇号或连字符分隔的任意数量的字母。

图 16.21 的第 33 行调用方法 validateAddress（图 16.20 的第 19–23 行）来验证地址。第一个字符类匹配一个或多个数字（\d+）。使用两个 \ 字符，因为 \ 通常在字符串中开始转义序列。因此，String 中的 \\d 表示正则表达式模式 \d。然后我们匹配一个或多个空白字符（\s+）。字符 "|" 匹配其左侧或右侧的表达式。例如，"Hi (John|Jane)" 匹配 "Hi John" 和 "Hi Jane"。括号用于对正则表达式的部分进行分组。在此示例中，| 的左侧匹配单个单词，右侧匹配由任意数量的空白字符分隔的两个单词。因此，地址必须包含一个数字后跟一个或两个单词。因此，"10 Broadway" 和 "10 Main Street" 在此示例中都是有效地址。城市（图 16.20 的第 26–29 行）和州（图 16.20 的第 32–35 行）方法也匹配至少一个字符的任何单词，或者如果单词由单个空格分隔，则匹配至少一个字符的两个单词，因此 Waltham 和 West Newton 都将匹配。

## 量词

星号 (*) 和加号 (+) 正式称为量词。图 16.22 列出了所有量词。我们已经讨论了星号 (*) 和加号 (+) 量词的工作方式。所有量词仅影响紧跟在量词之前的子表达式。量词问号 (?) 匹配其所量化的表达式的零次或一次出现。包含一个数字的花括号 ({n}) 匹配其所量化表达式的确切 n 次出现。我们在图 16.20 的第 40 行演示此量词来验证邮政编码。在花括号中包含的数字后加上逗号，匹配量化表达式的至少 n 次出现。包含两个数字的花括号 ({n,m}) 匹配其所限定表达式的 n 到 m 次出现（包含）。量词可以应用于括在括号中的模式，以创建更复杂的正则表达式。

| Quantifier | Matches |
|---|---|
| * | Matches zero or more occurrences of the pattern. |
| + | Matches one or more occurrences of the pattern. |
| ? | Matches zero or one occurrences of the pattern. |
| {n} | Matches exactly n occurrences. |
| {n,} | Matches at least n occurrences. |
| {n,m} | Matches between n and m (inclusive) occurrences. |

Fig. 16.22 | Quantifiers used in regular expressions.

所有量词都是贪婪的。这意味着只要匹配仍然成功，它们就会尽可能多地匹配出现次数。但是，如果任何这些量词是

