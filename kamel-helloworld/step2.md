# Run "Hello World" Integration
Running your first Integration is real easy to understand :

``` 
package src;
// camel-k: language=java

import org.apache.camel.builder.RouteBuilder;

public class HelloWorld extends RouteBuilder {
  @Override
  public void configure() throws Exception {

      // Write your routes here, for example:
      from("timer:java?period=1000")
        .routeId("java")
        .setBody()
          .simple("Hello Camel K from ${routeId}")
        .to("log:info");

  }
}
```


To install it you just have to run the integration


`kamel run src/HelloWorld.java`{{ exec }}

Kamel respond with "Integration "hello-world" created"





Now, you can check the logs with

```
 kamel log hello-world
```{{ exec }}

You will see something like this:

You can delete the integration with


```
kamel delete hello-world
```{{ exec }}

