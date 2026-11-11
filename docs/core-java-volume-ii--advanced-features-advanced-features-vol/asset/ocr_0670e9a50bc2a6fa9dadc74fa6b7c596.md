# Listing 3.6 *(Continued)*

```
```java
36    String filename;
37    if (args.length == 0)
38    {
39        System.out.print("Input file: ");
40        filename = in.nextLine();
41    }
42    else
43        filename = args[0];

45    Document doc = builder.parse(filename);
46    var done = false;
47    while (!done)
48    {
49        System.out.print("\\nXPath expression (empty line to exit): ");
50        String expression = in.nextLine();
51        if (expression.trim().isEmpty()) done = true;
52        else
53        {
54            try
55            {
56                XPathEvaluationResult<?> result
57                    = path.evaluateExpression(expression, doc);
58                if (result.type() == XPathEvaluationResult.XPathResultType.NODESET)
59                {
60                    for (Node n : (XPathNodes) result.value())
61                        System.out.println(description(n));
62                }
63                else if (result.type() == XPathEvaluationResult.XPathResultType.NODE)
64                    System.out.println((Node) result.value());
65                else
66                    System.out.println(result.value());
67            }
68            catch (XPathExpressionException e)
69            {
70                System.out.println(e.getMessage());
71            }
72        }
73    }
74  }
75 }

77 public static String description(Node n)
78 {
79     if (n instanceof Element) return "Element " + n.getNodeName();
80     else if (n instanceof Attr) return "Attribute " + n;
81     else return n.toString();
82 }
83 }
```
```