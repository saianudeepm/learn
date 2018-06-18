# Node:
Its a run time environment for executing javascript on server side (before it was only on browser)
Advantages:
* Highly scalable
* Fewer lines of code than java stack
* Built on javascript (so no need to use different languages for frontend/backend. meaning unified stack)

eg:
* Microsofts Edge browser uses chakra engine
* Chrome browser uses v8 engine
* Firefox browser uses SpiderMonkey engine

Variety
-------
Because of this variety of engines, Javascript can behave diffferently on different browsers

How Node came to be:
-------------------
* In browsers we have window & document objects which can help us interact with them.
* In 2009, they took googles v8 engine and embedded it into c++ program and called it Node.
* Node provide objects (no document object like in client side version) like filesystem (fs), http(to create webserver etc)
* So difference being Node providing different run time environments(although uses same javascript engine underneath)

## Asynchronous:
* Previously, when a request comes to server, a thread is allocated to the request to do the work.
* Some types of works like querying a database, writing to a file etc.. take time before they can finish.
* If there are many clients this model doesnt scale well (you quickly run out of threads/ you need to up your hardware to meet the needs)


## How is it done?
Threads dont have to wait(be idle) for such taks to finish and can be reused for different request. Node uses single thread with an event queue to manage this.

* A message is written into event queue. when the data is available in the message, then node takes this message out and continues processing. 
* So this architecture is very optimal where applications have a lot of
disk I/O or Network I/O
Note: Node is optimal for I/O intensive tasks and not optimal for CPU intensive tasks .





