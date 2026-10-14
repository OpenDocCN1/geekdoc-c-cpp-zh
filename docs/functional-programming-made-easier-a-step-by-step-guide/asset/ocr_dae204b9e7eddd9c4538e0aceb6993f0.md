The first thing we’re going to have to be able to do is specify the field name in the Types. We accomplish this by using a Symbol with Proxy.

Let’s look at the kind Symbol:

![](bbox=[0.145, 0.148, 0.853, 0.316])

Symbol lets us to use String literals in Type Definitions.

Let’s first see how we use Proxy with delete:

```
log $ "RESPONSE: " <> (show $ delete (Proxy :: _ "writeBody") res) ① ②
```

+   ① delete field named "writeBody" from the Response, i.e. res.
+   ② The _ is figured out by the compiler to be the Type Proxy.

Here’s a change to our logging using delete to pull out the non-existent field writeBody__. Since we specify the field name in the Type System, and that field doesn’t exist, the following won’t compile:

```
-- COMPILER ERROR!!
log $ "RESPONSE: " <> (show $ delete (Proxy :: _ "writeBody__") res)
```

It causes the following error:

![](bbox=[0.28, 0.692, 0.72, 0.907])

This is because of the Constraints on delete: