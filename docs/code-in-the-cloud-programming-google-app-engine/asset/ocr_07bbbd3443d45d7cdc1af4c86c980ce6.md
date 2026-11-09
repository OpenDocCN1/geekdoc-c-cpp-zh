Google therefore uses something called *asynchronous* or *continuation passing* style for remote calls. The call itself returns nothing. Instead, it takes an extra parameter, which is a function to invoke on the result of the RPC whenever it’s received.

For example, imagine we have a factorial service. In traditional style, what we want to do is this:

```
System.out.println("Foo = " + Math.log(3 * f.fact(n)));
```

In continuation passing style, that would be something like this:

```
f.fact(n, new AsyncCallback<int>() {
    public void onSuccess(int result) {
        System.out.println("Foo = " + Math.log(3 ~ result));
    }
});
```

All I did was take the original code that was going to use the return value of the RPC and wrap it up in an object that I could pass to the remote call. All that does is start the process. My code can go off and do other things while the RPC is translating the call to a message, sending it, waiting for the server to send a respond, and then translating the response message back to a result value. Whenever the result comes back, the callback will be invoked, and the result of the call will be processed.

It can feel a bit unnatural when you’re used to imperative programming. (Functional programmers do this all the time, even when they’re not doing distributed programming.) It takes some time to get used to, and even then, it sometimes seems a bit twisted. But overall, the advantage of not having to wait for the RPC outweighs the problems. It makes applications more responsive to the users, and that’s the most important thing.

# Client-Side RPC in GWT

No matter how great a toolkit is, communication is never simple. We need to be able to deal with translating parameters into a format that can be passed as a message, and we need to be able to deal with delays or even failures due to the network. To cope with that, GWT uses a very Google-ish idiom. At Google, we have some very distinctive and stylized ways of handling certain basic problems. In particular, we have a way of doing remote procedure calls using an asynchronous response handler. It’s pretty foreign to people who haven’t done a lot of distributed programming in the Google style. In general, GWT is really terrific about making plumbing invisible. However, in this case they decided not to.