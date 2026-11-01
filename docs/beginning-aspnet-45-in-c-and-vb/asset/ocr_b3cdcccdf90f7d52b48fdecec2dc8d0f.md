```
{
    return string.Format("Hello {}", name);
}
}
```

5. That's it. You just created a WCF service that can be called from client-side code. Note that if you try to request the .svc file in the browser directly, you get a screen similar to Figure 10-8.

![](bbox=[0.2, 0.26, 0.85, 0.55])

FIGURE 10-8

You get this screen because by default, for security reasons, WCF services don't expose their meta data. This means they don't tell the outside world how they work and how to call them. If you want to test your WCF service you could enable it to publish its meta data by following the instructions on the service page shown in Figure 10-8. Once you've enabled the meta data, you get more information about testing the service using a WCF test client program. I usually don't do this for simple WCF services, though; it's often just as easy to call the service from a client-side page, as you see in a later Try It Out exercise.

# How It Works

WCF services are essentially methods that can be called over a network, like the Internet or your local network. They are designed to enable applications to communicate and exchange data with each other. The default underlying message format for an Ajax-enabled WCF service is JSON. This is a very succinct way to exchange data. For example, the two reviews you saw in an earlier example are transferred from the server to the client using the following JSON code:

```
{
    "d":["_type":"Review:#","Id":1,"Title":"21st Century Breakdown by Green Day"},{"_type":"Review:#","Id":2,"Title":"Sonic Youth: Daydream Nation live in Roundhouse, London"}]
}
```

I split the code over multiple lines to make it more legible. In reality, this code was all placed on a single line. If you look at the comments above your service code file you see that you can also have it return XML. However, for most purposes, JSON is an excellent choice.