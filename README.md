<img width="1919" height="1199" alt="image" src="https://github.com/user-attachments/assets/9599d3ff-ab63-4441-8da9-10c563eb25ad" />


# Multithreaded TCP Server (Java)

This project is a simple multithreaded **TCP server** implemented in Java using a **thread pool**. It accepts multiple client connections concurrently and responds with a greeting message. The server is tested with **Apache JMeter** for load and performance benchmarking.

## Features

* Uses **ExecutorService** with a fixed thread pool.
* Accepts multiple client connections concurrently.
* Responds with a custom message: `Hello from server <client_ip>`.
* Demonstrates basic multithreaded socket programming in Java.
* Load tested with **Apache JMeter**.

## How It Works

1. The server starts on port `8010`.
2. A fixed-size thread pool (default `10` threads) is created using `Executors.newFixedThreadPool()`.
3. For every incoming client connection:

   * A new task is submitted to the thread pool.
   * The server sends back a greeting message to the client.

## Code Overview

```java
ServerSocket serverSocket = new ServerSocket(port);
Socket clientSocket = serverSocket.accept();
threadPool.execute(() -> handleClient(clientSocket));
```

The `handleClient()` method sends:

```java
toSocket.println("Hello from server " + clientSocket.getInetAddress());
```

## Requirements

* Java 8 or above
* Apache JMeter (for performance testing)

## Run Instructions

1. Clone the repository:

   ```bash
   git clone https://github.com/NirajSalunke/ThreadPool-Server.git
   cd ThreadPool-Server
   ```
2. Compile the server:

   ```bash
   javac Server.java
   ```
3. Run the server:

   ```bash
   java Server
   ```

## Testing the Server

You can test using **Netcat** or **Telnet**:

```bash
nc localhost 8010
```

Expected output:

```
Hello from server /127.0.0.1
```

## Performance Testing with JMeter

The server was tested with **Apache JMeter 5.6.3** using a TCP Sampler.

### Results Summary

* **Number of Samples**: 13,829
* **Average Response Time**: \~1 ms
* **Median Response Time**: 1 ms
* **Deviation**: 2 ms
* **Throughput**: \~60,039 requests/minute
* **Errors**: 0

### Result Graph

<img width="1919" height="1198" alt="image" src="https://github.com/user-attachments/assets/fbdfe2e3-0d8c-4a90-a1e9-f906f93abd3b" />


The graph shows stable throughput with very low latency, demonstrating the efficiency of the thread pool approach.

## Future Improvements

* Add configurable port and pool size via command-line arguments.
* Implement request/response processing instead of static messages.
* Add logging support.
* Provide a client implementation for easier testing.
* Containerize with Docker for deployment.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
