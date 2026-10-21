it possible for a small number of threads to handle a large number of actors, as with coroutines.

You could use Akka actors to reimplement the parallel ad-fetching and database lookup example:

```
Scala
import akka.actor.typed.{ ActorRef, Behavior }
import akka.actor.typed.scaladsl.Behaviors

case class RequestMsg(replyTo: ActorRef[PageMsg], request: Request)
case class AdMsg(ad: Ad)
case class PageMsg(page: Page)

def requestHandling(): Behavior[RequestMsg] =
  Behaviors.receivePartial {
    case (context, RequestMsg(replyTo, request)) =>
      val dbQueryingActor = context.spawnAnonymous(dbQuerying(replyTo, request))
      context.spawnAnonymous(adFetching(dbQueryingActor, request))
      Behaviors.same
  }

def adFetching(replyTo: ActorRef[AdMsg], request: Request): Behavior[Nothing] =
  Behaviors.setup { context =>
    val ad = fetchAd(request)
    replyTo ! AdMsg(ad)
    Behaviors.stopped
  }

def dbQuerying(replyTo: ActorRef[PageMsg], request: Request): Behavior[AdMsg] =
  Behaviors.setup { context =>
    val data = dbLookup(request)

    Behaviors.receiveMessagePartial {
      case AdMsg(ad) =>
        val page = makePage(data, ad)
        replyTo ! PageMsg(page)
        Behaviors.stopped
    }
  }
```

Listing 27.7: Example of non-blocking concurrency using actors.

Listing 27.7 defines a requestHandling actor to handle messages of type RequestMsg, which contain a request and an address replyTo indicating where to send the final page. Upon receiving a request, this actor spawns two new actors: adFetching,