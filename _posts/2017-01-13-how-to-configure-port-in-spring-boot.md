---
layout: post
title: How to Configure Port in Srping Boot
---

Since Spring Boot provides various configuration externalization mechanism (through various PropertySource implementations and/or processors wired into Environment object in order), you can set any property outside of your jar archive through following methods:

1. Pass property through command line argument
2. 
    `java -jar <path/to/my/jar> --server.port=7788`
    
2. From propety in SPRING_APPLICATION_JSON (Spring Boot 1.3.0+)
    * Define environment variable in UNIX shell:
    
    `SPRING_APPLICATION_JSON='{"server.port":7788}' java -jar <path/to/my/jar>`

    * By using Java system property:
    
    `java -Dspring.application.json='{"server.port":7788}' -jar <path/to/my/jar>`

    * Pass through command line argument:
    
    `java -jar <path/to/my/jar> --spring.application.json='{"server.port":7788}'`

3. Define system property

    `java -Dserver.port=7788 -jar <path/to/my/jar>`

4. Define OS environment variable
    * UNIX Shell
    
    `SERVER_PORT=7788 java -jar <path/to/my/jar>`

    * Windows
    
    ```
    SET SERVER_PORT=7788
    java -jar <path/to/my/jar>
    ```

5. Place property in ./config/application.properties

    `server.port=7788`
    
    and run:
    
    `java -jar <path/to/my/jar>`
    
6. Place property in `./config/application.yaml`

    ```
    server:
        port: 7788
    ```
    
    and run:
    
    `java -jar <path/to/my/jar>`
    
7. Place property in ./application.properties

    `server.port=7788`

    and run:

    `java -jar <path/to/my/jar>`

8. Place property in ./application.yaml

    ```
    server:
        port: 7788
    ```
    
    and run:
    
    `java -jar <path/to/my/jar>`
    
You can combine above methods all together, and the former configuration in the list take precedence over the latter one.

For example:

`SERVER_PORT=2266 java -Dserver.port=5566 -jar <path/to/my/jar> --server.port=7788`

The server will start and listen on port 7788.

This is very useful providing default properties in PropertySources with lower precedence (and usually packaged in the archive or coded in the source), and then override it in the runtime environment.