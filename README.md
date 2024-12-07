# **NETFILEX** 🌐  
![Waketime](https://img.shields.io/badge/Waketime-115%20hrs%2021%20minutes-blueviolet?style=plastic)

## **Author**  
**Shreyas Mehta**  

---
### **Overview** 📝
- **Project Name**: NetFileX
- **Project Type**: Distributed File System
- **Project Duration**: 3 weeks
- **Project Status**: Completed
- This project was part of the `Operating Systems and Networks` course at **IIIT Hyderabad**.

The **`Naming Server`** is a critical component in a distributed system designed to facilitate efficient communication between **`Clients`** and **`Storage Servers`**. It serves as the mediator for managing metadata, ensuring requests are routed correctly, and mapping client requests to the appropriate storage locations. In a larger system, the **`Naming Server`** plays an integral role in ensuring high performance, scalability, and fault tolerance.

### **Roles of the System Components**:

1. **`Naming Server`** 🗄️:
   - **Primary Role**: Acts as the central directory for the system, managing the metadata of files and mapping them to appropriate storage servers.
   - **Responsibilities**:
     - Receives client requests for file access and retrieves necessary metadata.
     - Maintains a registry of available **`Storage Servers`** and their resources.
     - Routes requests from clients to the appropriate storage server based on metadata.
     - Handles caching of frequently accessed data using an **`LRU`** cache for improved performance.
     - Coordinates the addition or removal of **`Storage Servers`** in the network.

2. **`Storage Servers`** 💾:
   - **Primary Role**: Stores the actual data and provides storage capabilities to the distributed system.
   - **Responsibilities**:
     - Store the data requested by clients.
     - Send metadata information (e.g., location, size) to the **`Naming Server`** during registration.
     - Handle read and write requests directed to them by the **`Naming Server`**.
     - Respond to the **`Naming Server`** with the data requested by clients.

3. **`Clients`** 👥:
   - **Primary Role**: Initiates requests for data stored in the distributed system and interacts with the **`Naming Server`** to retrieve file metadata.
   - **Responsibilities**:
     - Send requests to the **`Naming Server`** for file information.
     - Receive metadata from the **`Naming Server`** to determine which **`Storage Server`** holds the requested data.
     - Retrieve data from the appropriate **`Storage Server`**.
     - Handle user interface or application logic that interacts with the distributed storage system.

### **How It All Fits Together**:
The **`Naming Server`** provides an essential role in the distributed system by serving as the point of interaction between **`Clients`** and **`Storage Servers`**. Clients query the **`Naming Server`** to get file metadata and the location of the storage. Once the location is determined, the **`Naming Server`** routes the client request to the correct **`Storage Server`**. This architecture ensures that file access is efficient and that clients can scale their requests across multiple servers.

This system also uses caching mechanisms, such as an **`LRU`** (Least Recently Used) cache in the **`Naming Server`**, to reduce lookup times for frequently accessed files. The **`Storage Servers`** remain lightweight, focused on data storage and retrieval, while the **`Naming Server`** handles the coordination and routing of requests, making the system more organized and performant.

---

## **File Structure** 📂

```
NetFileX/
├── README.md                            # Project overview and instructions
├── 'OSN Course Project Evaluation.md'   # Project evaluation file
├── client/                              # Client-side code and assets
│   ├── client.c                         # Client implementation in C
│   ├── client.h                         # Client header file
│   ├── large.txt                        # Sample file for large write operations
├── naming_server/                       # Naming server-side code
│   ├── app.py                           # To build multiple storage servers at once for testing
│   ├── caching/                         # Caching-related files
│   ├── errors.h                         # Error handling header
│   ├── globals.h                        # Global constants and configurations
│   ├── log/                             # Logging functionality
│   │   ├── log.c                        # Logging implementation
│   │   └── log.h                        # Logging header
│   ├── lru/                             # Least Recently Used (LRU) caching
│   │   ├── a.out                        # Executable for LRU
│   │   ├── lru.c                        # LRU cache implementation
│   │   └── lru.h                        # LRU cache header
│   ├── main/                            # Main server-side logic
│   ├── Makefile                         # Build instructions for naming server
│   ├── namingServer                     # Naming server implementation
│   ├── path/                            # Path management files
│   │   ├── path.c                       # Path handling logic
│   │   └── path.h                       # Path header
│   ├── return_struct.h                  # Struct definitions for return values
│   └── tries/                           # Trie-based structure for file management
│       ├── a.out                        # Executable for tries
│       ├── tries.c                      # Trie implementation
│       └── tries.h                      # Trie header
├── storage_server/                      # Storage server-side code
│   ├── a.out                            # Executable for storage server
│   ├── file.c                           # File handling on storage server
│   ├── file.h                           # File header
│   ├── gdbss                            # Debugging file for storage server
│   ├── lib.h                            # Library for storage server operations
│   ├── network.c                        # Network communication for storage server
│   ├── network.h                        # Network header
│   ├── ss                               # Storage server executable
│   ├── storage                          # Directory or files related to storage management
│   ├── storage_server.c                 # Main implementation of the storage server
│   └── storage_server.h                 # Storage server header
├── logs.txt                             # System log file
├── Makefile                             # Build instructions for the entire project
└── color.h                              # Color configuration file (likely for output formatting)
```

---

## **Key Features** 🧑‍💻

- **Write Operations**:
  - Supports writing interactive text input (`WRITE`) up to **`any number of bytes`**.
  - **`Large file writes`** using `LARGE.txt` for files larger than 8192 bytes.
  - **Asynchronous writes** for files over **`8192 bytes`**, improving performance without blocking the client.

- **Naming Server (NM)**:
  - Coordinates file access, ensuring **`non-blocking`** and **`efficient`** client requests.
  - Uses a **`Trie-based`** structure for optimized search and quick file location.
  - Handles dynamic **`IP management`** for network flexibility.

- **File Copying**:
  - Allows copying of **files** up to **`any number of bytes`** and **directories** (without copying the directory itself).

- **Audio Streaming**:
  - **Uninterrupted streaming** once started, with no ability to stop mid-way.

- **Trie-Based Storage**:
  - Efficient **file management** with unique paths, avoiding naming conflicts.

- **Multiple Clients**:
  - Supports **`concurrent clients`** with one writer and multiple readers per file.
  - Handles asynchronous operations for non-blocking writes.

- **Error Handling**:
  - Clearly defined error codes for issues like **`file unavailability`** and **`write conflicts`**.

- **Search Optimization**:
  - Uses a **`Trie`** for fast **file searches** and efficient access to relevant **Storage Servers**.

- **Data Replication and Fault Tolerance**:
  - **`Replication`** ensures data availability across multiple **Storage Servers**.
  - Asynchronous data duplication for improved **`fault tolerance`**.

---

## **Detailed Functionality** ⚙️

### **1. Write Operations** ✍️
- **Interactive Writes**: Input a single line up to **`8192 bytes`** for smaller file writes.
- **Large Writes**: Transfer large files using `LARGE.txt`.
- **Asynchronous Writes**: For files over **`8192 bytes`**, the system acknowledges the client immediately while the file is written asynchronously in chunks.

### **2. Naming Server (NM)** 🗂️  
- **Concurrency**: Handles multiple client requests with **`non-blocking`** acknowledgments.
- **Efficient Search**: Uses **`Trie-based`** structures to rapidly identify the correct **Storage Server** for each request.
- **Error Handling**: Returns detailed error codes for different failure scenarios.

### **3. Copy Command Behavior** 📂
- **File-to-File**: Supports copying files up to **`1024 bytes`**.
- **Directory-to-Directory**: Only the contents of the directory are copied, not the directory itself.

### **4. Audio Streaming** 🎧  
- Once streaming begins, it cannot be stopped until completion.

### **5. Data Structure** 📊  
- **`Trie`** ensures unique paths for all files and directories, enhancing search speed and file management.

### **6. Multiple Clients Handling** 🤝  
- **`Concurrent Client Access`**: Allows multiple clients to read files concurrently, while only one client can write at a time.
- **Client Timeouts**: Handles client timeouts when the **Naming Server** fails to respond promptly.

### **7. Error Codes** ⚠️  
- Defined error codes for **`file not found`**, **`write conflicts`**, and **`server failures`**.

### **8. Search in Naming Server** 🔍  
- **Trie-Based Search** and **LRU Caching** for fast and efficient data retrieval.

### **9. Backing up Data** 🔄  
- **Replication** ensures availability in case of failures.
- **Asynchronous Duplication** for data redundancy.

### **10. Redundancy** 💾  
- Ensures **storage server recovery** with synchronization of data after failure.

### **11. Bookkeeping** 📜  
- **Logging** of all requests and communications, aiding in debugging and monitoring.


## **Future Enhancements** ⏳  
- **Scalability**: Future updates will support **`horizontal scaling`** of both the **Naming Server** and **Storage Servers**.
- **Security**: Implement **`encryption`** for file transfers.
- **Data Integrity**: Incorporate **`checksum validation`** to ensure data integrity.



## **Installation & Build Instructions** 💾

1. **Clone the repository**:
   ```bash
   git clone https://github.com/ShreyasMehta05/NetFileX.git
   ```

2. **Navigate to the project directory**:
   ```bash
   cd NetFileX
   ```

3. **Install dependencies**:
   - Install `gcc` for C compilation.
   - Install `mpv` for audio functionality:
     ```bash
     sudo apt install gcc mpv
     ```

---


## **Build Instructions** 🛠️

### **1. Naming Server (NM) Build**  
To compile the **Naming Server**, run the following command in named `naming_server` directory:

```bash
gcc namingServer.c lru/lru.c log/log.c caching/caching.c path/path.c tries/tries.c -o main -pthread -g
```

- **Explanation**:  
  This command compiles all the necessary source files for the Naming Server and links them together. The `-pthread` flag enables multi-threading, and the `-g` flag is used for debugging.

#### **Alternative Build Command**  
Alternatively, you can use `make` to compile the Naming Server with a pre-configured `Makefile` in the `NETFILEX` directory:

```bash
make naming_server
```

### **2. Storage Server (SS) Build**  
To compile the **Storage Server**, navigate to the `storage_server` directory and run:

```bash
gcc *.c -o ss -pthread -g
```

- **Explanation**:  
  This command compiles all the `.c` files in the `storage_server` directory and generates an executable named `ss`. The `-pthread` flag enables multi-threading support.

#### **Alternative Build Command**  
To use `make` for building the Storage Server in the `NETFILEX` directory:

```bash
make storage_server
```

### **3. Client Build**  
To compile the **Client**, run the following command in the `client` directory:

```bash
gcc client.c -o client -lmpv
```

- **Explanation**:  
  This command compiles the client-side code and links the `libmpv` library for audio functionality.

#### **Alternative Build Command**  
Alternatively, to use `make` to compile the Client in the `NETFILEX` directory:

```bash
make client
```

---

## **Running the Executables** 💻

After compiling the project, you can run the respective components with the following commands. You must supply the necessary command-line arguments.
Here’s the corrected and refined version of your documentation:

---

### **1. Running the Naming Server (NM)**  
To run the **Naming Server**, execute the following command:

```bash
./main
```

If you wish to modify the configuration, update the global variables in the `globals.h` file accordingly, and then run the command again as shown above.

---

## **Configuration and Assumptions** 📡

The **Naming Server** runs with the following default configuration parameters:

### **Global Constants** 🛠️
These constants are defined in the `globals.c` file of the **Naming Server** and can be adjusted as needed for your network setup.

```c
#define __NAMING_SS_PORT__ 8080              // Default port for Storage Server connections
#define __NAMING_CLIENT_PORT__ 8081          // Default port for Client connections
#define __NAMING_SERVER_IP__ "192.168.16.138" // Default IP address for the Naming Server
#define __MAX_STORAGE_SERVERS__ 100          // Maximum number of Storage Servers supported
#define __MAX_CLIENTS__ 100                  // Maximum number of clients that can connect concurrently
#define __BUFFER__ 5                         // Buffer size for handling requests
#define __BUFFER_SIZE__ 4096                 // Maximum buffer size for data storage/transfer
#define __MAX_LRU_CACHE_SIZE__ 10            // Maximum size of Least Recently Used (LRU) cache
```

- **Port Numbers**:  
  The **Naming Server** listens on port `8080` by default for Storage Server connections and port `8081` for Client connections. These port values can be modified by changing the `__NAMING_SS_PORT__` and `__NAMING_CLIENT_PORT__` definitions in `globals.h`.

- **IP Address**:  
  The **Naming Server** uses the default IP `192.168.16.138`. In a production environment, you should replace this IP with the actual IP address of your **Naming Server** machine. Modify the `__NAMING_SERVER_IP__` definition in `globals.h` as needed.

- **Maximum Storage Servers**:  
  The system supports a maximum of `100` **Storage Servers**, as specified by the `__MAX_STORAGE_SERVERS__` constant. You can adjust this value based on the scale of your setup.

- **Maximum Clients**:  
  The **Naming Server** can handle up to `100` concurrent client connections, as specified by `__MAX_CLIENTS__`. Adjust this value as needed to support more clients.

- **Buffer Sizes**:  
  The system uses a buffer size of `5` for handling requests (`__BUFFER__`) and `4096` bytes for data storage/transfer (`__BUFFER_SIZE__`). These values can be tuned to optimize memory and processing based on system requirements.

- **LRU Cache Size**:  
  The **Naming Server** uses an LRU (Least Recently Used) caching strategy with a default cache size of `10` entries (`__MAX_LRU_CACHE_SIZE__`). This helps improve access times for frequently requested data.

### **Assumptions** 🔧

1. **Naming Server IP and Port**:  
   The **Naming Server** listens on IP `192.168.16.138` by default and port `8080` for Storage Server communication. Clients should connect to port `8081`. Modify these values in `globals.h` if a different setup is required.

2. **Multi-Server Setup**:  
   The system can handle up to `100` **Storage Servers** and up to `100` concurrent client connections, as defined by `__MAX_STORAGE_SERVERS__` and `__MAX_CLIENTS__`.

3. **System Buffer**:  
   The system uses a buffer size of `4096` bytes (`__BUFFER_SIZE__`) to handle incoming requests efficiently. You can adjust this buffer size in `globals.h` for optimized memory usage.

4. **LRU Cache**:  
   The **Naming Server** utilizes an LRU caching strategy to store the most frequently accessed data. The cache can hold up to `10` entries by default, and this can be modified by adjusting `__MAX_LRU_CACHE_SIZE__` in `globals.h`.

---



### **2. Running the Storage Server (SS)**  
To run the Storage Server, execute the following command, passing in the required arguments:

```bash
./ss <nm_server_ip> <nm_server_port> <client_port>
```

- **Arguments**:  
  - `<nm_server_ip>`: IP address of the Naming Server.
  - `<nm_server_port>`: Port of the Naming Server.
  - `<client_port>`: Port for the Storage Server to listen for incoming client connections.

For example:

```bash
./ss 192.168.1.10 8080 9090
```

### **3. Running the Client**  
To run the Client, provide the **Naming Server IP** as a command-line argument:

```bash
./client <naming_server_ip>
```

- **Arguments**:  
  - `<naming_server_ip>`: IP address of the Naming Server.

For example:

```bash
./client 192.168.1.10
```

The client will now interact with the **Naming Server** and allow you to perform operations like listing files, reading, writing, and more.

--- 

## **Client Functionality** 🎮

- **LIST**: List available files.
- **READ**: Read file content.
- **WRITE**: Write data to a file.
- **DELETE**: Delete a file or folder.
- **CREATE**: Create a new file or folder.
- **COPY**: Copy a file to a different path.
- **AUDIO**: Stream an audio file.
- **EXIT**: Exit the client application.

---
### **Dependencies** 📦
The **Naming Server** requires the following dependencies:

- **GCC**: The GNU Compiler Collection (for compiling C programs).
- **POSIX Threads (pthreads)**: For multi-threading support.
- **Libraries**: (e.g., any network-related libraries if used).

### Troubleshooting:

- **Error: "Unable to bind to port"**  
  This error typically means the specified port is already in use. Try changing the port number in `globals.h` and recompile.

- **Error: "Connection Refused"**  
  Ensure the server is running and that the correct IP and port are used by the client.

- **Memory Allocation Issues**  
  If you run into memory-related issues, check that your buffer sizes and cache settings in `globals.h` are configured correctly.
---

## **Project Evaluation** 📝

The project will be evaluated based on the following `OSN Course Project Evaluation.md` file

---

### **Contributors** 🧑‍💻

- **Shreyas Mehta**  
  - **Role**: Implementation of Naming Server.
  - **Contribution**: Designing the system architecture, implementing the Naming Server, and coordinating the project.
- **Inesh Dheer**  
  - **Role**: Implementation of Client.
  - **Contribution**: Developing the client-side functionality and testing the system.
- **Shubham Goel**
  - **Role**: Implementation of Storage Server.
  - **Contribution**: Building the Storage Server, handling file operations, and ensuring data integrity.
- **Swam Singla**
  - **Role**: Implementation of Storage Server, Async Write, Audio Streaming, Polling.
  - **Contribution**: Enhancing the Storage Server with async write, audio streaming, and polling functionality.

---


## **Conclusion** 🎯

The **NetFileX** project demonstrates the design and implementation of a distributed file system with a **`Naming Server`**, **`Storage Servers`**, and **`Clients`**. By leveraging a **`Trie-based`** structure for file management, **`LRU caching`** for performance optimization, and **`asynchronous operations`** for improved efficiency, the system provides a robust foundation for distributed file access.

The project showcases the collaboration and contributions of team members in building a functional distributed system that supports various file operations, client interactions, and data streaming. With future enhancements planned for scalability, security, and data integrity, **NetFileX** aims to evolve into a versatile and reliable distributed file system for diverse applications.

---

