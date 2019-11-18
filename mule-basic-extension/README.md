# Mule Extension

## Introduction

MuleSoft's Anypoint Connectors helps to connect third-party APIs and service through the Mule flow. You can use the connector to send or receive a message from Mule flow to one or more external services over protocol or API. Mule flow designing is graphical, so you don't need to write a single line of code to connect external services when you are using Anypoint connectors. Today, MuleSoft has a large collection of different connectors to connect and integrate diverse systems including Salesforce, Database, different Google and AWS services, and many more.


You can develop your own connector using new Mule SDK platform, which is the replacement of earlier Mule devkit tool. In this article, I'd like to walk you through how to develop your own connector using Mule SDK.


## Prerequisites

1. Java JDK Version 8.x
2. Anypoint Studio 7.x
3. Apache Maven 3.3.9 or higher

## Steps to Create a Connector

Go to the directory where you want to create connector (studio-workspace) and execute a command to create project structure with sample test cases:

`$ mvn org.mule.extensions:mule-extensions-archetype-maven-plugin:generate`


Add this dependency to your application pom.xml

    	<groupId>org.mule.extension</groupId>
    	<artifactId>mule-basic-extension</artifactId>
    	<version>1.0.0-SNAPSHOT</version>
    	<classifier>mule-plugin</classifier>


## Java classes

1.  **BasicExtension.java**
    <br><br>
    The connector is called as an **extension** in Mule 4, and it's class defined by the annotation **@Extension**.
    A **@Configurations** annotation is used to point the configuration class.
    <br><br>
    This is the main class of an extension, is the entry point from which configurations, connection providers, operations and sources are going to be declared.
    <br><br>

2.  **BasicConfiguration.java**
    <br><br>
    Configuration class defines the parameters that we expect appears in configuration part of the connector.
    We can use **@ConnectionProvider** and **@Operation** annotation with this class to point out the connection providers and the operations connector has implemented.
    <br><br>
    This class represents an extension configuration, values set in this class are commonly used across multiple operations since they represent something core from the extension.
    <br><br>

3.  **BasicConnectionProvider.java**
    <br><br>
    The next important class is _BasicConnectionProvider_, which is annotated as **@ConnectionProviders in** configuration class.
    <p> - This class is used to manage and provide the connection with the targeted system. </p>
    <p> - The connection provider must implement the **PoolingConnectionProvider**, other options are **CachedConnectionProvider** and **ConnectionProvider**. </p>
    <p> - Parameter required to establish connection must be defined into the ConnectionProvider class. </p>
    <p> - Also, you must override connect, disconnect, and validate methods to provide the functionality specific to this connection provider.</p>

    <p> This class (as it's name implies) provides connection instances and the functionality to disconnect and validate those connections. </p>
    <p> All connection related parameters (values required in order to create a connection) must be declared in the connection providers. </p>
    <p> This particular example is a {@link PoolingConnectionProvider} which declares that connections resolved by this provider will be pooled and reused.
    	There are other implementations like {@link CachedConnectionProvider} which lazily creates and caches connections or simply {@link connectionProvider} if you want a new connection each time something requires one. </p>
    <p> A parameter that is always required to be configured. </p>
    <p> A parameter that is not required to be configured by the user </p>

4.  **BasicConnection.java**
    <p>	The Connection class is used by connection providers to handle the connection.
    	By having the single connection class and multiple connection providers, we can create multiple connection configurations for our Connector. </p>

    <p> This class represents an extension connection just as example (there is no real connection with anything here). </p>

5.  **BasicOperations.java**
    <p> Finally, we have operation class.
    	We can define any number of operation classes and all public methods from this class will be treated as a connector operation.
    	We can inject configurations and connection to particular operation using **@Config** and **@Connection** annotation in method arguments. </p>
    <p>	This class is a container for operations, every public method in this class will be taken as an extension operation. </p>
    <p>	Example of an operation that uses the configuration and a connection instance to perform some action. </p>
    <p>	Example of a simple operation receives a string parameter and returns a new string message that will be set on the payload </p>
    <p>	Private Methods are not exposed as operations </p>
    
    
## Reference
https://dzone.com/articles/how-to-create-a-custom-connector-in-new-mule-sdk-4 

