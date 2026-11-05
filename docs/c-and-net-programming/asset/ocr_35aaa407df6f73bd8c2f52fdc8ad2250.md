```
```csharp
bc.BroadCast_Date = DateTime.Now;
bc.BroadCast_Message = "New Quiz Is Uploaded!";
EventTicked(this, bc);
}
}

//Step 2 class containing data which is broadcasted by the publisher
class BroadCast {
private DateTime broadCast_Date;
public DateTime BroadCast_Date
{
get { return broadCast_Date; }
set { broadCast_Date = value; }
}
private string broadCast_Message;
public string BroadCast_Message
{
get { return broadCast_Message; }
set { broadCast_Message = value; }
}

//Step 3 create the Subscriber Class. A publisher can have 1 or many subscribers.
Here 2 //subscribers have been created.
Subscriber1 Class
class Subscriber1
{
string SubscriberName = "Raj";

// Below function listen to the event if it is raised by the Publisher
public void Listener(Publisher P)
{
P.EventTicked += P_EventTicked;
}
// Below function is executed when the event fired by the Publisher
void P_EventTicked(Publisher P, BroadCast e)
{
Console.WriteLine("Hello " + SubscriberName + ", Message from " + P.PublisherName
+ " at " + e.BroadCast_Date + " - " + e.BroadCast_Message);
}
}
Subscriber2 Class
class Subscriber2
{
string SubscriberName = "Ravi";
public void Listener(Publisher P)
```
```