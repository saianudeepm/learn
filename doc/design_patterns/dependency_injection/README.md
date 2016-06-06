## Context and Dependency Injection

DI = design pattern to decouple relationship b/w a component & its dependencies
Does this by injecting dependency into an object rather than creating the dependency by using 'new' keyword

By removing creation of dependency from object and delegating responsibility to container, you can swap out dependency for another compatible object at compile, runtime

####CDI (Context and Dependency Injection)- managed beans:
Instantiated when container starts up.
Note all POJO;s should have def constructor.

Injected using @Inject annotation

eg showing dependency Injection:
```
public class Message {
    public String getMessage(){
        return "Hello World!!";
    }

}

public class Service {

    @Inject
    private Message message;

    public void showMessage(){
        System.out.println(message.getMessage());
    }
}
```
### Context Scope
Context is the distinguishing feature between EJB's and CDI-managed beans. CDI beans exist within a defined context unlike EJB's.

CDI beans are created within context of a scope;
@ApplicationScope
@ConversationScope
@SessionScope
@RequestScope

So CDI container controls life of a bean based on beans scope.



