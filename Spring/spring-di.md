# Dependency Injection
spring-context

## General DI Topics
IoC, if the term is still even valid, separate into two categories:

**Dependency Injection**
A component's dependencies are provided to the dependent object by the framework. Favor inject over lookups wherever you have the choice.
    
**Dependency Lookup**
The dependent object pulls dependencies from a registry of managed components. For example, JNDI lookups or context.getBean in spring.
 
 
### Setter Injection vs. Constructor Injection
Utilize constructor injection when the dependent object *must* have an instance of the dependency in order to function. Otherwise, you may use setter injection.


## Using BeanFactory Directly
The BeanFactory serves as the base class for more commonly used services like ApplicationContext. You can use it directly for manually wiring DI.

*A simple example utilizing BeanFactory with configuration in XML:*
``` java
// Oracle Interface
public interface Oracle {
    String defineMeaningOfLife();
}

// BookwormOracle
public class BookwormOracle implements Oracle {
    @Override
    public String defineMeaningOfLife() {
        return "Encyclopedias are a waste of money - use the Internet";
    }
}

// Main method with pulled dependencies
import org.springframework.beans.factory.support.DefaultListableBeanFactory;
import org.springframework.beans.factory.xml.XmlBeanDefinitionReader;
import org.springframework.core.io.ClassPathResource;

public class XmlConfigWithBeanFactory {
    public static void main(String[] args) {
        DefaultListableBeanFactory factory = new DefaultListableBeanFactory();

        XmlBeanDefinitionReader rdr = new XmlBeanDefinitionReader(factory);
        rdr.loadBeanDefinitions(new
            ClassPathResource("META-INF/spring/xml-bean-factory-config.xml"));

        Oracle oracle = (Oracle) factory.getBean("oracle");

        System.out.println(oracle.defineMeaningOfLife());
    }
}
```

*Configuration file for the example above:*
``` xml
<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="oracle" name="wiseworm" class="com.apress.prospring4.ch3.BookwormOracle"/>
</beans>
```



## Application Configuration with ApplicationContext

``` xml
<!-- BASIC COMPONENT SCAN -->
<context:component-scan base-package="com.apress.prospring4.ch3.annotation" />

<!-- COMPONENT SCAN with EXCLUDE-FILTER -->
<context:component-scan base-package="com.apress.prospring4.ch3.annotation" >
    <context:exclude-filter type="assignable" expression="com.example.NotAService"/>
</context:component-scan>

<!-- DECLARE A BEAN TO PROVIDE FOR INTERFACE MessageRenderer  -->
<bean id="messageRenderer" 
    class="com.apress.prospring4.ch3.xml.StandardOutMessageRenderer"/>
```


### Setter Injection
``` xml
<!-- SETTER INJECTION -->
<bean id="messageRenderer"
    class="com.apress.prospring4.ch3.xml.StandardOutMessageRenderer">
    <property name="messageProvider" ref="messageProvider"/>
</bean>

<!-- SETTER INJECTION WITH "P" NAMESPACE  -->
xmlns:p="http://www.springframework.org/schema/p"
<bean id="messageRenderer"
    class="com.apress.prospring4.ch3.xml.StandardOutMessageRenderer"
    p:messageProvider-ref="messageProvider"/>
    
<!-- INJECTING ONE BEAN INTO ANOTHER WITH REF -->
<bean id="oracle" name="wiseworm" class="com.apress.prospring4.ch3.BookwormOracle"/>
<bean id="injectRef" class="com.apress.prospring4.ch3.xml.InjectRef">
    <property name="oracle">
        <ref bean="oracle"/> <!-- could use the name or id here -->
    </property>
</bean>
```


### Constructor Injection
``` xml
<!-- CONSTRUCTOR INJECTION -->
<bean id="messageProvider"
    class="com.apress.prospring4.ch3.xml.ConfigurableMessageProvider">
    <constructor-arg value="Configurable message"/>
</bean>

<!-- CONSTRUCTOR INJECTION WITH "C" NAMESPACE -->
xmlns:c="http://www.springframework.org/schema/c"
<bean id="messageProvider"
    class="com.apress.prospring4.ch3.xml.ConfigurableMessageProvider"
    c:message="This is a configurable message"/>

<!-- CONSTRUCTOR INJECT WITH TYPE TO AVOID CONSTRUCTOR AMBIGUITY -->
<bean id="constructorConfusion"
    class="com.apress.prospring4.ch3.xml.ConstructorConfusion">
    <constructor-arg type=”int”>
        <value>90</value>
    </constructor-arg>
</bean>
```


**NOTE** LEFT OFF AT 'Injection and ApplicationContext Nesting in Chapter 3

## Standard Java Configuration
@Configuration
@Bean


## Component Scanning
``` java
@ComponentScan(basePackages = "<packageName>")
@Autowired
@Qualifier("classID")
```

You can autowire to a collection, which will assign all matched beans into the collection. Neat!

**javax method, don't use by default. less general**
@Resource

You can and should limit the scope of a component scan by making a package for each type you want find.
    repositories
    services
    controllers

**By default, all Sprint managed beans are singletons!**
@Scope("singleton") is the default
@Scope("prototype") will make the context return an instance rather than a singleton.

WebMVC adds request and session to the list of valid scopes.

This means that spring intends to manage things that make sense as singletons. It isn't necessarily designed to replace the new keyword throughout your code.

``` java
@Bean(initMethod="" destroyMethod="")
@PostConstruct
@PreDestroy
```

    
