Here's a Java RMI application:

---

# Java RMI Application

This project demonstrates how to create a simple Java RMI (Remote Method Invocation) application. It includes steps for defining a remote interface, implementing the interface, developing server and client programs, compiling the application, and executing it.

## Overview

The Java RMI application consists of four main components:

1. Remote Interface: Defines the methods that can be invoked remotely.
2. Implementation Class: Provides the actual implementation of the remote interface.
3. Server Program: Hosts the remote object and makes it available to clients.
4. Client Program: Interacts with the remote object hosted on the server.

## Steps to Create Java RMI Application

### 1. Define the Remote Interface

- Create an interface that extends `java.rmi.Remote`.
- Declare all the methods that can be invoked remotely.
- Handle `RemoteException` for potential network issues.

Example:
```java
import java.rmi.Remote;
import java.rmi.RemoteException;

public interface Hello extends Remote {
    void printMsg() throws RemoteException;
}
```

### 2. Develop the Implementation Class

- Implement the remote interface.
- Provide implementation for all the abstract methods of the remote interface.

Example:
```java
import java.rmi.RemoteException;
import java.rmi.server.UnicastRemoteObject;

public class ImplExample extends UnicastRemoteObject implements Hello {
    public ImplExample() throws RemoteException {}

    public void printMsg() {
        System.out.println("This is an example RMI program");
    }
}
```

### 3. Develop the Server Program

- Create a remote object from the implementation class.
- Export the remote object using `UnicastRemoteObject.exportObject()`.
- Bind the remote object to the RMI registry.

Example:
```java
import java.rmi.registry.LocateRegistry;
import java.rmi.registry.Registry;
import java.rmi.RemoteException;

public class Server {
    public static void main(String[] args) {
        try {
            ImplExample obj = new ImplExample();
            Hello stub = (Hello) UnicastRemoteObject.exportObject(obj, 0);
            Registry registry = LocateRegistry.getRegistry();
            registry.bind("Hello", stub);
            System.err.println("Server ready");
        } catch (Exception e) {
            System.err.println("Server exception: " + e.toString());
            e.printStackTrace();
        }
    }
}
```

### 4. Develop the Client Program

- Get the RMI registry.
- Fetch the remote object from the registry using the `lookup()` method.
- Invoke methods on the remote object.

Example:
```java
import java.rmi.registry.LocateRegistry;
import java.rmi.registry.Registry;

public class Client {
    public static void main(String[] args) {
        try {
            Registry registry = LocateRegistry.getRegistry(null);
            Hello stub = (Hello) registry.lookup("Hello");
            stub.printMsg();
        } catch (Exception e) {
            System.err.println("Client exception: " + e.toString());
            e.printStackTrace();
        }
    }
}
```

## Compiling and Executing the Application

To compile and execute the application, follow these steps:

1. Compile all the Java files: `javac *.java`
2. Start the RMI registry: `start rmiregistry`
3. Run the server program: `java Server`
4. Run the client program: `java Client`

## Requirements

- Java Development Kit (JDK)

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---
