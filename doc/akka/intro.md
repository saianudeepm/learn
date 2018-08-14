# Akka

## Glossary:
Akka: Messaged driven framework
Actor System: A system to which actors are registered.
Mailbox: A queue from which actors pick up the messages one by one

## Sending a Message

```
//Get reference to the actor from the Actor System:
val actor = actorSystem.actorOf(Props[SummingActor], "summingactor") 

//Send message to the actor using the DSL "!"
actor ! 1 

```

* Actors have methods to communicate with each other actors :
  > 
  1. tell (!) or 2. ask (?) 

  First one is fire and forget 
  Second returns a Future 

* On receiving the message, the actor picks up an underlying thread from thread pool, does its work and releases it.
* Actors are never blocked on current thread, so they are asynchronous by nature.

## Retreiving a result:

Two actors can communicate via messages by simply using `!` (fire and forget) like below:

* lets say actor1 has sent a message to actor 2
``` actor1 ! "hello" ```
* actor 2 can respond after its done its processing like so:
``` sender ! "Hi" ```

But if we want a response the message that is sent, then we can do like this:

```
val future = (actor ? "Hi there").mapTo[String] // we get a future and map its result to a string type
val response = Await.result(future, 10 seconds)

```

> Note: Actors, by nature, know who has sent them the message, thus we always have the sender present in the context of the receive block.

* Instead of string messages, typically we define message types in actors and send them which usually are objects

eg: 
```
 object Messages { 
          case class Done(randomNumber: Int) 
          case object GiveMeRandomNumber 
          case class Start(actorRef: ActorRef) 
        }
```

* So then the process of communication can look like below using message types: 

```
//Actor2
override def receive: Receive = { 
    case GiveMeRandomNumber => println("received a message to generate a random integer") 
    val randomNumber = nextInt 
    sender ! Done(randomNumber) // respond to the sender by sending a Done message with result encapsulated in it.
} 

//Actor1
override def receive: Receive = { 
    case Start(actorRef) => println(s"send me the next random number") 
    actorRef ! GiveMeRandomNumber 
    case Done(randomNumber) => println(s"received a random number $randomNumber") 
} 

//in Main thread
actor1 ! Start(actor2) // send a Start message to actor1 with actorRef as actor2

```

 ## Actor's Queue (Mailbox)
 * Each actor has its own mailbox-like queue from which it picks up the messages one by one
 * Built in type of mailboxes are (PriorityMailbox, controlAwareMailbox ...etc)
 * You can build your own mailbox (queue) by extending MessageQueue interface for custom purposes
 eg: Only accept the messages from certain actors and queue them
 eg: Have a priority in which we want to queue these messages based on many criteria etc.

 *Control-aware mailbox:* When you want your actor to process a certain message first before any other message, at any point of time.
 
 ```
  //in application.conf
  control-aware-dispatcher {  
      mailbox-type = 
       "akka.dispatch.UnboundedControlAwareMailbox" 
      //Other dispatcher configuration goes here 
    }

  //in actor 
   case object MyControlMessage extends ControlMessage  

   def receive = { 
            case MyControlMessage => println("Oh, I have to process
              Control message first") 
            case x => println(x.toString) 
          } 
 ```
