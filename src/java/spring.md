# spring

```java
package com.genson.demo.config;

import org.springframework.boot.CommandLineRunner;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class CustomerConfig {

    @Bean
    CommandLineRunner commandLineRunner() {
        return args -> {
            System.out.println("Command line runner Hayoo");
        };
    }
}

/*
2023-01-31T23:16:43.491+07:00  INFO 18459 --- [           main] com.genson.demo.DemoApplication          : Starting DemoApplication using Java 17.0.2 with PID 18459 (/Users/genson/Desktop/demo/target/classes started by genson in /Users/genson/Desktop/demo)
2023-01-31T23:16:43.495+07:00  INFO 18459 --- [           main] com.genson.demo.DemoApplication          : No active profile set, falling back to 1 default profile: "default"
2023-01-31T23:16:44.393+07:00  INFO 18459 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2023-01-31T23:16:44.404+07:00  INFO 18459 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2023-01-31T23:16:44.404+07:00  INFO 18459 --- [           main] o.apache.catalina.core.StandardEngine    : Starting Servlet engine: [Apache Tomcat/10.1.5]
2023-01-31T23:16:44.478+07:00  INFO 18459 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2023-01-31T23:16:44.479+07:00  INFO 18459 --- [           main] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 923 ms
2023-01-31T23:16:44.816+07:00  INFO 18459 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2023-01-31T23:16:44.824+07:00  INFO 18459 --- [           main] com.genson.demo.DemoApplication          : Started DemoApplication in 1.755 seconds (process running for 2.449)
Command line runner Hayoo   <------------
*/

```
