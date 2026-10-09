```
```
//      break;
//      case OperatorToken op:
//        var rhs = stack.Pop();
//        var lhs = stack.Pop();
//        var res = ComputeExpression(op, rhs, lhs);
//        if (res is not null) {
//            stack.Push(res);
//        }
//        break;
//      default:
//        throw new Exception($"Invalid input token: {t}");
//  }
//}
return stack.Peek() ?? throw new Exception($"Failed to compute
the input expression: {input}");
}

// Note the order of the method parameters.
// "rhs" comes before "lhs".
private static Number? ComputeExpression(OperatorToken op, Number?
rhs, Number? lhs) {
    // Note this unusual statement. We do this here just for fun. :) 
    // But, this _can_ become a new idiom in the modern C#. Mark my
    // word. ;)
    _ = lhs ?? rhs ?? throw new Exception($"Invalid input expression.
    Operator = {op}");

    // This is equivalent to the following (more traditional) null-
    // check statement:
    // if ((lhs is null) || (rhs is null)) {
    //     throw new Exception($"Invalid input expression. Operator =
    //     {op}");
    // }

    // There is a lot going on in the above strange-looking
    // statement.
    // First, as stated in the book, ?? is a "null-coalescing
    // operator".
```
```