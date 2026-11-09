
Of course, we want to be able to do things that rely on getting data from the server. We can get data from the server with what we know, but always within the standard synchronous cycle of client-server interaction of the browser. We write client code that sends requests to the server, the server responds to those requests, and when the client’s browser receives the response, it renders it. Without doing something special, we can’t avoid that basic request-response process.

The request-response-render cycle really isn’t enough. We want to write our chat application so that it automatically updates the display whenever there’s a new chat message. But our chat application waits for the user to do a manual refresh. We could write a piece of JavaScript with a timer, which automatically refreshes once a second. But every time that refresh happened, it would be very disruptive to the users. Their interfaces would go blank and then redraw. If they started typing a new message, that message would be lost when the browser refreshed. That’s absolutely not what we want.

What we need to do is to talk to the server asynchronously. That is, we need to write some code that runs separately from the usual request-response-render cycle. This technique is called AJAX: asynchronous JavaScript and XML. It uses a JavaScript construct called an `XMLHttpRequest`. `XMLHttpRequest` is, frankly, rather an ugly hack. Like a lot of the tools that we use for programming the client-side of a web-based cloud app, it’s basically an ad hoc thing that someone slapped together because they really needed it, rather than something carefully designed as part of a toolkit for building UIs. Once people started using it, it became a standard, and now we’re pretty much stuck with it. (As we’ll see in Section 9.3, RPC in GWT, on page 135, the AJAX can be wrapped up and hidden under the covers so that you don’t need to deal with the ugliness, but it’s always best to understand what’s really going on.)

The key to `XMLHttpRequest` is that it’s asynchronous, which means when a request is sent, the sender doesn’t wait for a response. Normally, when we write code that makes HTTP requests, we do it with a function call: we call a method to send the request, and the return value of that function call is the response to the query. The code *blocks*—it does nothing but wait until it gets a response. But an `XMLHttpRequest` doesn’t block. Instead, when we create an `XMLHttpRequest`, one of the parameters is a function called a *callback*. When the client’s browser receives a response to the request, it invokes the callback function. So the client never blocks—it just continues along, and the user gets a very smooth user interface without any interruptions or refreshes. As soon as a response is received, the callback is invoked, and the user interface is updated with the latest information.

### XMLHttpRequest Is Not an XML HTTP Request

XMLHttpRequest is incredibly poorly named. In reality, it’s not a request, and it’s got nothing to do with XML.

XMLHttpRequest is a request manager—an object used to create requests, send those requests, and handle the responses it receives.

The most important thing about XMLHttpRequest is that it’s capable of generating and sending a request outside of the normal browser request-response-render cycle, and it can handle the requests asynchronously, so your program doesn’t need to wait for a response.

This description sounds very abstract. But it’s really not difficult with App Engine, and the best way to show that is by writing code. We’ll go straight to what we really want—a dynamically updated chat view.

To do that, we need to write a bunch of pieces:

- 1. A server request handler that serves the user interface frame without any chat data
- 2. A server request handler for fetching chat data (new messages)
- 3. A JavaScript component that requests updates from the server and then adds messages to the transcript whenever it receives new data.

## The Model: Chat's Request Handlers

The first thing we need to do is build a request handler on the server. We’re going to split our request handler into two pieces by separating the handler that sends the user interface to the client from the handler that sends the data to the client. The first handler, which sends the UI to the client, basically sends the view and the controller to the browser, so that it can run as the client for our application. Then the controller will send requests for data to the server, which will be sent by the second handler.

A response and when the client receives it. In order to make sure that the client doesn’t miss any messages, we want to know what time the server thought it was when it sent the last message to the client.

The code to do all that is pretty straightforward. We’ll just send an XML document. The top-level element will be our own `<ChatUpdate>` element, which will include a `time` attribute. Inside the `<ChatUpdate>`, we’ll put the HTML `<p>` tags containing the chat messages. And as usual, we’ll use a Django template to generate the XML. The template is pretty straightforward:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ChatUpdate chat="{{ chat }}" time="{{ time }}">
{% for m in msg_list %}
<p>{{ m.timestamp }} ({{ m.user }}) ({{ m.timestamp }}): {{ m.message|escape }}</p>
{% endfor %}
</ChatUpdate>
```

The request handler that fills in the template is also very straightforward:

```python
class DataRequestHandler(webapp.RequestHandler):
    def get(self):
        requested_chat = self.request.get("chat", default_value="none")
        messages = db.GqlQuery("SELECT * FROM ChatMessage WHERE chat = :1 "
                               "ORDER BY timestamp", requested_chat).fetch(20)

        template_params = {
            'msg_list': messages,
            'chat': requested_chat,
            'time': self.request.get("time", default_value="0"),
        }
        path = os.path.join(os.path.dirname(__file__), 'update.xml')
        page = template.render(path, template_params)
        self.response.headers['Content-Type'] = "application/xml"
        self.response.headers.add_header("Access-Control-Allow-Origin", "*")
        self.response.headers.add_header("Access-Control-Allow-Methods",
                                          "GET, POST, OPTIONS")
        self.response.out.write(page)
```

That’s it for the model part. As you can see, the model really doesn’t need much specialization in order to work in interactive mode. The only thing you need to do is separate the process of serving the interface from the process of serving the data.

## The Controller: JavaScript on the Client

In the server discussion in the previous section, I said that we’d send the JavaScript controller code with the user interface in the initial handler, but in the code, all that I showed was a script line that would include the JavaScript. Now we’re going to implement the controller. Let’s jump right into the code:

```javascript
function SetUpAndSendRequest(time, chat) {
    var request = new XMLHttpRequest();
    var transcript = document.getElementById("chat-transcript");

    request.onreadystatechange = function() {
        // Wait until the request is done. Done == ready state 4.
        if (request.readyState != 4) {
            return;
        }
        var xmlData = request.responseXML.documentElement;
        if (xmlData != null) {
            transcript.innerHTML = "";
            messages = xmlData.getElementsByTagName("p");
            for (var x = 0; x < messages.length; x++) {
                transcript.innerHTML += "<p>" +
                    messages[x].childNodes[0].nodeValue + "</p>";
            }
            newtime = xmlData.getAttribute("time");
            SetUpAndSendRequest(newtime, chat);
        } else {
            transcript.innerHTML +=
                "<p>Sorry, but there was an error updating this chat</p>";
        }
    }
    request.open("GET", "?latest&time=" + time + "&chat=" + chat, true);
    request.send();
}

function init() {
    SetUpAndSendRequest(0, "book")
}

window.onload = init;
```

- 1. First, we set up a few global variables that we’ll need. The most important one is the XMLHttpRequest. In addition, we set up global references to the main application URL and to the part of the HTML page that contains the chat transcript.
- 2. It’s time to start the actual request code. The first thing we need to do is open a request. The XMLHttpRequest object isn’t a request;
