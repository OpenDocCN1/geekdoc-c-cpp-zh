+   1. Your computer sends your request for the web page to a router. The router distributes Internet access throughout your home or workplace.
+   2. The router passes your request onto your Internet service provider (ISP). In the United States, your ISP is a company like Comcast, Time Warner, AT&T, or Verizon.
+   3. Your ISP then converts the words and characters in your URL — “huffingtonpost.com,” in my example — into a numerical address called the *Internet protocol address* (or, more commonly, *IP address*). An IP address is a set of four numbers separated by periods (such as, for example, 192.168.1.1). Just like your physical address, this number is unique, and every computer has one. Your ISP has a digital phone book, similar to a physical phonebook, called a *domain name server* that’s used to convert text URLs into IP addresses.
+   4. With the IP address located, your ISP knows which server on the Internet to forward your request to, and your personal IP address is included in this request.
+   5. The website server receives your request, and sends a copy of the web page code to your computer for your browser to display.
+   6. Your web browser renders the code onto the screen.

![](bbox=[0.269, 0.523, 0.768, 0.759])

When you edited the website code using the Developer Tools, you modified only the copy of the website code that exists on your computer, so only you could see the change. When you reloaded the page, you started steps 1 through 6 again, and retrieved a fresh copy of the code from the server, overwriting any changes you made on your computer.