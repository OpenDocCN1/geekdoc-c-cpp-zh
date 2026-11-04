These web service standards apply to protocols like SOAP. They're written by a standards organization, reviewed, certified, and used by the tool developers — like Microsoft.

What is better is that the additional standards include a lot of really neat functionality that makes SOAP a very rich development experience. Usually, distributed communication standards leave transactions, security, and other such functionality up to the developer.

SOAP isn't like that. It is supposed to have all that stuff baked in.

The WS-* standards include all this useful functionality:

+   - **Web Services Transactions (WS-TX):** Coordinates the outcome of broadly distributed communications.
+   - **Web Services Reliable Exchange (WS-RX):** Provides a confirmation of communication for service calls.
+   - **Web Service Federation (WS-FED):** Allows for a federation of trust between service providers.
+   - **Web Service Remote Portlets (WS-RP):** A standard for web parts using services (like you see in SharePoint).
+   - **Web Service Security (WS-SX):** A supported trusted exchange.
+   - **Web Services Discovery (WS-DD):** A way to find services in a large enterprise.
+   - **Building Information Exchange (oBIX):** Allows buildings to talk to each other about their wiring. No, I'm not kidding!
+   - **OASIS ebXML:** A business XML standard that is designed to provide a standardized data model for communications.

In general, these are fantastic additions. They define a set of functionality that all web service development software providers — Microsoft, IBM, Sun, open source initiatives, whomever — can implement. If you need transactions, they are there. Security? Baked in.

# The impact to you

The problem is that these standards were used differently by every company that implemented them.

No, I am not kidding. The problem with standards this detailed in scope is that in order to be useful, they must either leave a lot to the imagination or define everything. OASIS erred on the side of being too loose, and the implementations are a mess.