# An application that uses AJAX

To illustrate how an application that uses AJAX works, the topics that follow present an application that uses a shout box. A shout box can be used to implement an informal comment system on a web site. Unlike traditional comment systems, users aren’t required to register to enter shouts and shouts are typically displayed only for a short period of time. By AJAX-enabling this shout box, it can be updated without interfering with what the user is doing.

# The Shout Box application

Figure 21-11 presents the Shout Box application. To start, this application lets the user display the products in a selected category in a DataList control. This part of the web page is not AJAX-enabled and works just like the Product List application you saw in chapter 13.

To the right of the DataList control are the controls that are used to implement the shout box. These controls are placed inside two UpdatePanel controls. The first update panel includes a label that displays the shout box, along with a Timer control that causes the shout box to be updated every five seconds. The second update panel includes two text boxes that let the user enter the information for a shout, labels that identify the text boxes, required field validators for the text boxes, a button that submits the shout, and an UpdateProgress control.

Notice that the shouts in the shout box are displayed in reverse chronological order. In other words, they’re displayed from the newest shout to the oldest shout. That way, if there are many shouts being displayed, the user won’t have to scroll down to see the newest ones.

The shouts for this application are displayed in the shout box for three minutes. The shouts that are currently displayed are stored in a list in application state. That makes sense since the shouts are temporary. If you wanted to have a permanent record of the shouts, however, you could store them in a database and then display just the most recent shouts in the shout box.