sum() function can be called in two different ways. The simple way is to call it unaryFunc will be an invalid QScriptValue, and the action performed will be simply to sum the numbers and return the result. The subtler way is to call the function with an ECMAScript function as the first argument, followed by any number of numeric arguments. In this case, the given function is called for each number, and the sum of the results is accumulated and returned. We use this same function in ECMAScript in first section of this chapter (p. 514). Using C++ rather than ECMAScript to implement low-level functionality can sometimes lead to significant performance gains.

Before we call C++ functions from a script, we must make them available to the interpreter using newFunction() and setProperty():

```
QScriptValue qsSquare = interpreter.newFunction(square);
interpreter.globalObject().setProperty("square", qsSquare);
```

```
QScriptValue qsSum = interpreter.newFunction(sum);
interpreter.globalObject().setProperty("sum", qsSum);
```

We have made both square() and sum() available as global functions to the interpreter. Now we can use them in scripts, as the following snippet shows:

```
interpreter.evaluate("print(sum(1, 2, 3, 4, 5, 6));");
interpreter.evaluate("print(sum(square, 1, 2, 3, 4, 5, 6));");
```

This concludes our coverage of making Qt applications scriptable using the Qt module. The module is provided with extensive documentation including a broad overview, and detailed descriptions of the classes it provides, including QScriptContext, QScriptEngine, QScriptValue, and QScriptable, all of which are worth reading.