```
case ExpressionType.Parameter:
		ParameterExpression paramExpr = (ParameterExpression)expression;
		WriteLine($" {output} Param Type: {paramExpr.Type.Name} ");
		break;
	case ExpressionType.Equal:
	case ExpressionType.AndAlso:
	case ExpressionType.GreaterThan:
		BinaryExpression binExpr = (BinaryExpression)expression;
		if (binExpr.Method != null)
		{
			WriteLine($" {output} Method: {binExpr.Method.Name} ");
		}
		else
		{
			WriteLine(output);
		}
		DisplayTree(indent,"Left", binExpr.Left);
		DisplayTree(indent,"Right", binExpr.Right);
		break;
	case ExpressionType.MemberAccess:
		MemberExpression memberExpr = (MemberExpression)expression;
		WriteLine($" {output} Member Name: {memberExpr.Member.Name} " + 
		" Type: {memberExpr.Expression}");
		DisplayTree(indent,"Member Expr", memberExpr.Expression);
		break;
	default:
		WriteLine();
		WriteLine($" {expression.NodeType} {expression.Type.Name} ");
		break;
	}
```

The expression that is used for showing the tree is already well known. It’s a lambda expression with a Racer parameter, and the body of the expression takes racers from Brazil only if they have won more than six races:

```
Expression<Func<Racer, bool>> expression = 
	 r => r.Country == "Brazil" && r.Wins > 6;

DisplayTree(0,"Lambda", expression);
```

Looking at the tree result, you can see from the output that the lambda expression consists of a Parameter and an AndAlso node type. The AndAlso node type has an Equal node type to the left and a GreaterThan node type to the right. The Equal node type to the left of the AndAlso node type has a MemberAccess node type to the left and a Constant node type to the right, and so on:

```
Lambda! NodeType: Lambda; Expr: r => ((r.Country == "Brazil") AndAlso (r.Wins > 6))
> Parameter! NodeType: Parameter; Expr: r Param Type: Racer
> Body! NodeType: AndAlso; Expr: ((r.Country == "Brazil") AndAlso (r.Wins > 6))
>> Equal NodeType: Equal; Expr: (r.Country == "Brazil") Method: op_Equality
>>>	Left! NodeType: MemberAccess; Expr: r.Country Member Name: Country, Type: String
>>>	Right! NodeType: Constant; Expr: "Brazil"
>> GreaterThan NodeType: GreaterThan; Expr: (r.Wins > 6)
>>>	Left! NodeType: Parameter; Expr: r Param Type: Racer
>>>	Right! NodeType: Constant; Expr: 6
```