# Spring Boot
## Very Simple Spring Application
``` java
package com.apress.spring;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
@RestController
public class SimpleWebApp {

    @RequestMapping("/")
    public String greetings() {
        return "<h1> Spring Boot Rocks in Java too!</h1>";
    }

    public static void main(String[] args) {
        SpringApplication.run(SimpleWebApp.class, args);
    }
}
```

Run with ```spring run *.java```

## Base pom.xml with Spring Dependencies
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>myapp</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <!-- Spring Boot Parent Dependencies-->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.3.1.RELEASE</version>
    </parent>

    <!-- Add dependencies: starter poms -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter</artifactId>
    </dependency>

    <!-- Spring Boot Plugin for creating JAR/WAR files -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

**FOR A WEB PROJECT**
...replace the artifact id in dependency with spring-boot-starter-web.


## Base build.gradle with Spring Dependencies
```
buildscript {
    repositories {
        jcenter()
        maven { url "http://repo.spring.io/snapshot" }
        maven { url "http://repo.spring.io/milestone" }
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:1.3.1.RELEASE")
    }
}

apply plugin: 'java'
apply plugin: 'spring-boot'

jar {
    baseName = 'myproject'
    version =  '0.0.1-SNAPSHOT'
}

repositories {
    jcenter()
    maven { url "http://repo.spring.io/snapshot" }
    maven { url "http://repo.spring.io/milestone" }
}

dependencies {
    // starter poms dependencies
    compile('org.springframework.boot:spring-boot-starter')
}
```

**FOR WEB APPLICATIONS**
```
compile("org.springframework.boot:spring-boot-starter-web")
testCompile("org.springframework.boot:spring-boot-starter-test")
```


## Scaffolding with Spring Initializr
http://start.spring.io
Creates a project in a ZIP file you can download

Then, use curl to download the starter project. There are two
versions, a maven template and gradle template.


curl -s https://start.spring.io/starter.zip -o myapp.zip
**or**
curl -s https://start.spring.io/starter.zip -o myapp.zip -d type=gradle-project

**For a web project...***
curl -s https://start.spring.io/starter.zip -o myapp.zip -d type=maven-project -d dependencies=web

**To generate the pom.xml file...***
curl -s https://start.spring.io/pom.xml -d packaging=war -o pom.xml -d
dependencies=web,data-jpa

**Or the gradle build***
curl -s https://start.spring.io/build.gradle -o build.gradle -d
dependencies=web,data-jpa


