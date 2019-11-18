# Basic Extension

Add description ...


...


...


Add this dependency to your application pom.xml

```
<groupId>org.mule.extension</groupId>
<artifactId>mule-basic-extension</artifactId>
<version>1.0.0-SNAPSHOT</version>
<classifier>mule-plugin</classifier>
```

1. **BasicExtension.java** 
	<br><br>
	The connector is called as an **extension** in Mule 4, and it's class defined by the annotation **@Extension**. 
	A **@Configurations** annotation is used to point the configuration class.
	<br><br>
	This is the main class of an extension, is the entry point from which configurations, connection providers, operations and sources are going to be declared.	
	<br><br>

2. **BasicConfiguration.java** 
	<br><br>
	Configuration class defines the parameters that we expect appears in configuration part of the connector. 
	We can use **@ConnectionProvider** and **@Operation** annotation with this class to point out the connection providers and the operations connector has implemented.
	<br><br>
	This class represents an extension configuration, values set in this class are commonly used across multiple operations since they represent something core from the extension.
	<br><br>

3. **BasicConnectionProvider** 
	<br><br>
	The next important class is *BasicConnectionProvider*, which is annotated as **@ConnectionProviders in** configuration class. 
	<br> - This class is used to manage and provide the connection with the targeted system.
	<br> - The connection provider must implement the **PoolingConnectionProvider**, other options are **CachedConnectionProvider** and **ConnectionProvider**.
	<br> - Parameter required to establish connection must be defined into the ConnectionProvider class.
	<br> - Also, you must override connect, disconnect, and validate methods to provide the functionality specific to this connection provider.
	<p>
	This class (as it's name implies) provides connection instances and the functionality to disconnect and validate those connections.
	</p>
	<p> 
		All connection related parameters (values required in order to create a connection) must be declared in the connection providers.
	</p>
	<p>
		This particular example is a {@link PoolingConnectionProvider} which declares that connections resolved by this provider will be pooled and reused.
		There are other implementations like {@link CachedConnectionProvider} which lazily creates and caches connections or simply {@link connectionProvider} if you want a new connection each time something requires one.
	</p>
	<p>
		A parameter that is always required to be configured
	</p>
	<p>
		A parameter that is not required to be configured by the user
	</p>
	<br><br>

4. **BasicConnection.java** 
	<br><br>
		The Connection class is used by connection providers to handle the connection. 
		By having the single connection class and multiple connection providers, we can create multiple connection configurations for our Connector.
	<br><br>
	<p>
		This class represents an extension connection just as example (there is no real connection with anything here).
	</p>

5. **BasicOperations.java** 
	<br><br>
		Finally, we have operation class. 
		We can define any number of operation classes and all public methods from this class will be treated as a connector operation. 
		We can inject configurations and connection to particular operation using **@Config** and **@Connection** annotation in method arguments.
	<br><br>
	<p>
		This class is a container for operations, every public method in this class will be taken as an extension operation. 
	</p>












 