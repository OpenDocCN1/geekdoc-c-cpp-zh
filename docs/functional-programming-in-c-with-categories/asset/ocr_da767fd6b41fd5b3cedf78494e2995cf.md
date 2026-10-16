# 7.3.3 Object Oriented Interpreter Pattern implementation

Take a moment to appreciate the use of the reader applicative to evaluate expressions. In the object-oriented world exists something isomorphic to the above implementation: the Interpreter design pattern. I am stating bellow an implementation based on ECS6 in order to emphasize the object-oriented characteristics:

```
public class Context
{
    public string Log { get; set; }
}

public abstract class Expr
{
    public abstract void Eval(Context context);
}
public class ValExpr : Expr
{
    public ValExpr(int x) { X = x; }
    public int X { get; }

    public override void Eval(Context context)
    {
        context.Log += $"{X}";
    }
}
public class AddExpr : Expr
{
    public AddExpr(Expr x, Expr y)
    {
        X = x;
        Y = y;
    }

    public Expr X { get; }
    public Expr Y { get; }

    public override void Eval(Context context)
    {
        context.Log += $"Adding(";
        X.Eval(context);
        context.Log += $",";
        Y.Eval(context);
        context.Log += $")";
    }
}
```