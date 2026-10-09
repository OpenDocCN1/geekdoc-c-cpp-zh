
# key-value-store/Commands/Set.cs

```csharp
namespace KV;
using System.CommandLine;
using System.CommandLine.Invocation;

public sealed class SetCommand : Command {
    private IServer<string> server;

    public SetCommand(IServer<string> server,
        string name = "set",
        string description = "Set the value of a key to the given value")
    : base(name, description) {
        this.server = server;

        AddOption(new Option<string>(new[] { "--key", "-k" }, "Key"));
        AddOption(new Option<string>(new[] { "--value", "-v" }, "Value as a string"));
        Handler = CommandHandler.Create<string, string>(Set);
    }

    public void Set(string key, string value) {
        var oldValue = server.Set(key, value);
        if (oldValue is not null) {
            Console.WriteLine($"Replaced {oldValue} with {value} for {key}.");
        } else {
            Console.WriteLine($"Created a new item for {key} with value {value}.");
        }
    }
}
```

# key-value-store/Commands/Keys.cs

```csharp
namespace KV;
using System.CommandLine;
using System.CommandLine.Invocation;

public sealed class KeysCommand : Command {
    private IServer<string> server;

    public KeysCommand(IServer<string> server,
                      string name = "keys",
                      string description = "List all keys") : base(name, description) {
        this.server = server;

        Handler = CommandHandler.Create(Keys);
    }

    public void Keys() {
        var keys = server.Keys();
        Console.WriteLine($"All keys: {string.Join(", ", keys)}");
    }
}
```

# key-value-store/Commands/Exists.cs

```csharp
namespace KV;
using System.CommandLine;
using System.CommandLine.Invocation;

public sealed class ExistsCommand : Command {
    private IServer<string> server;

    public ExistsCommand(IServer<string> server,
        string name = "exists",
        string description = "Returns true if a key exists, false otherwise") : base(name, description) {
        this.server = server;

        AddOption(new Option<string>(new[] { "--key", "-k" }, "Key"));
        Handler = CommandHandler.Create<string>(Exists);
    }

    public void Exists(string key) {
        if (server.Exists(key)) {
            Console.WriteLine($"{key} exists");
        } else {
            Console.WriteLine($"{key} does not exist");
        }
    }
}
```

# key-value-store/Commands/Del.cs

```csharp
namespace KV;
using System.CommandLine;
using System.CommandLine.Invocation;

public sealed class DelCommand : Command {
    private IServer<string> server;

    public DelCommand(IServer<string> server,
        string name = "del",
        string description = "Delete the entry for a given key") :
        base(name, description) {
        this.server = server;

        AddOption(new Option<string>(new[] { "--key", "-k" }, "Key"));
        Handler = CommandHandler.Create<string>(Del);
    }

    public void Del(string key) {
        var oldValue = server.Del(key);
        if (oldValue is not null) {
            Console.WriteLine($"Deleted {oldValue} for {key}.");
        } else {
            Console.WriteLine($"Item for {key} does not exist.");
        }
    }
}
```

## Code Listing - Part IV
## Reverse Polish Calculator 1

# reverse-polish-1/Program.cs

```csharp
using ReversePolish;

// What would be the value of this expression (in the postfix notation) ?
// Before you write your code, make sure that you have a valid test case(s).
const string input = "1 3 + 1 + 2.0 * -5 + 5 -";

try {
  var number = new Calculator().Compute(input);
  Console.WriteLine($"Result = {number:V}");
} catch (Exception ex) {
  Console.WriteLine($"Failed to compute = {input}: Error = {ex.Message}");
}
```

# reverse-polish-1/Calculator.cs

```csharp
namespace ReversePolish;

public sealed class Calculator {
  private Stack<Token> stack;

  public Calculator() => stack = new();

  public Token Compute(string input) {
    stack.Clear();

    var words = input.Split();
    foreach (var w in words) {
      var t = ParseWord(w);
      var num = t.T switch {
        TokType.FLOAT or TokType.INT => t,
        TokType.OPERATOR => ComputeExpression(t, stack.Pop(),
          stack.Pop()) ?? throw new Exception(),
        _ => throw new Exception($"Invalid input token: {t}"),
      };
      if (num is not null) {
        stack.Push(num);
      } else {
        throw new Exception($"Invalid input token: {t}");
      }
    }

    return stack.Peek() ?? throw new Exception($"Failed to compute the input expression: {input}");
  }

  // Note the order of the method parameters.
  // "rhs" comes before "lhs".
  // This is in order to support the (stack.Pop(), stack.Pop()) syntax in Compute().
  private static Token? ComputeExpression(Token op, Token? rhs, Token? lhs) {
    if (!op.IsValidOperator() || rhs is null || !rhs.IsNumber || lhs is null || !lhs.IsNumber) {
      throw new Exception($"Invalid expression. Op = {op}; rhs = {rhs}; lhs = {lhs}");
    }

    return op.Char switch {
      '+' => lhs! + rhs!,
      '-' => lhs! - rhs!,
      '*' => lhs! * rhs!,
      '/' => lhs! / rhs!,
      _ => null,
    };
  }

  private static Token ParseWord(string word) {
    Token tok = Token.InvalidToken;
    if (long.TryParse(word, out long l)) {
      tok = new Token(TokType.INT, l);
    } else if (double.TryParse(word, out double d)) {
      tok = new Token(TokType.FLOAT, d);
    } else if (char.TryParse(word, out char c) && Token.IsValidOperator(c)) {
      tok = new Token(TokType.OPERATOR, c);
    }
    return tok;
  }
}
```

# reverse-polish-1/Token.cs

```csharp
namespace ReversePolish;

public sealed record Token(TokType T, object V) {
    public static readonly Token InvalidToken = new(TokType.INVALID, '\0');

    public char Char => (T == TokType.OPERATOR) ? (char)V : throw new InvalidCastException();

    public static bool IsValidOperator(char c) => c switch {
        '+' or '-' or '*' or '/' => true,
        _ => false,
    };

    public bool IsInt => T == TokType.INT;
    public bool IsFloat => T == TokType.FLOAT;
    public bool IsNumber => T == TokType.INT || T == TokType.FLOAT;
    public bool IsValidOperator() => T == TokType.OPERATOR &&
        (V is char c) && (c == '+' || c == '-' || c == '*' || c == '/');

    public static explicit operator long(Token tok) => (long)tok.V;
    public static explicit operator double(Token tok) => (double)tok.V;

    public static implicit operator Token(long l) => new(TokType.INT, l);
    public static implicit operator Token(double d) => new(TokType.FLOAT, d);

    public static Token operator +(Token lhs, Token rhs) => (lhs.T, rhs.T) switch {
        (TokType.INT, TokType.INT) => (long)lhs.V + (long)rhs.V,
        (TokType.INT, TokType.FLOAT) => (long)lhs.V + (double)rhs.V,
        (TokType.FLOAT, TokType.INT) => (double)lhs.V + (long)rhs.V,
        _ => (double)lhs + (double)rhs,
    };

    public static Token operator -(Token lhs, Token rhs) => (lhs.T, rhs.T) switch {
        (TokType.INT, TokType.INT) => (long)lhs.V - (long)rhs.V,
        (TokType.INT, TokType.FLOAT) => (long)lhs.V - (double)rhs.V,
        (TokType.FLOAT, TokType.INT) => (double)lhs.V - (long)rhs.V,
        _ => (double)lhs - (double)rhs,
    };

    public static Token operator *(Token lhs, Token rhs) => (lhs.T, rhs.T) switch {
        (TokType.INT, TokType.INT) => (long)lhs.V * (long)rhs.V,
        (TokType.INT, TokType.FLOAT) => (long)lhs.V * (double)rhs.V,
        (TokType.FLOAT, TokType.INT) => (double)lhs.V * (long)rhs.V,
        _ => (double)lhs * (double)rhs,
    };

    // Note: We use the int division when both operands are integers.
    // That is, 1/3 = 0.
    public static Token operator /(Token lhs, Token rhs) => (lhs.T, rhs.T) switch {
        (TokType.INT, TokType.INT) => (long)lhs.V / (long)rhs.V,
        (TokType.INT, TokType.FLOAT) => (long)lhs.V / (double)rhs.V,
        (TokType.FLOAT, TokType.INT) => (double)lhs.V / (long)rhs.V,
        _ => (double)lhs / (double)rhs,
    };

    public override string ToString() => T switch {
        TokType.INT => $"{T.ToName()}:(long){V}",
        TokType.FLOAT => $"{T.ToName()}:(double){V}",
        TokType.OPERATOR => $"{T.ToName()}:(char){V}",
        _ => $"{T.ToName()}:{V}",
    };
}
```
