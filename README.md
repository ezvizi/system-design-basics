# System Design Basics

Understanding the fundamentals of system design is pivotal for various reasons:

- **Solid Foundation**: Groundwork for advanced concepts.
- **Problem Solving**: Enables efficient solutions.
- **Performance**: Assures scalable and reliable systems.
- **Teamwork**: Boosts team communication and collaboration.
- **Cost Savings**: Leads to long-term financial efficiency.
- **Career Growth**: Opens advanced tech roles.
- **User Experience**: Ensures user-friendly systems.
- **Adaptability**: Prepares for evolving tech scenarios.
 
As of the current update, this repository hosts the content from the [EZVIZI newsletters](https://blog.ezvizi.com).


## 🌐 **EZF-001-1. REST API Architecture style**

![EZF Image](/images/blog/EZF-001-1.gif)

### EZF-001-1.1. Message formats:
- 📜 XML
- 📄 JSON
- 🌐 Other

### EZF-001-1.2. ✅ Advantages:
- 🔄 Stateless: Scales easily
- 🚀 Cacheable: Improved performance
- 🌐 Uniform Interface: Standardized use
- 📈 Scalable: Supports high request volumes
- 🔗 Interoperable: Works well with HTTP
- 🟢 Simple: Uses standard HTTP methods
- 🌍 Widely Adopted: Many resources available

### EZF-001-1.3. ❌ Disadvantages:
- 📦 Over/Under-fetching: Fixed data returns
- 🌐 Multiple Endpoints: More requests for complex data
- 🔄 Versioning Issues: Changes can break clients
- 📜 Limited Flexibility: Fixed data structures
- 📉 Performance: Multiple trips for complex data.
- 🚫 Stateful Limitations: Not ideal for real-time operations
- 🌐 Nested Resource Complexity: Harder to manage nested data

### EZF-001-1.4. 📋 Use cases:
- 🌐 Web Applications: Backend for web apps with CRUD operations.
- 📱 Mobile Apps: Backend support for mobile app data needs.
- 🔗 Public APIs: Offer services to third-party developers.
- 🔄 Integration: Connect different systems or services.
- 📜 Content Delivery: Distribute content to various platforms.
- 📂 Data Storage: Backend for apps needing database access.
- 🛒 E-Commerce: Manage products, orders, and user accounts.
- 🌐 Social Media Platforms: Handle user data, posts, and interactions.
- 📡 IoT Devices: Communicate with and manage IoT devices.
- 🔄 Legacy System Interface: Modern interface for older systems.

❓ *What API architecture style are you guys currently utilizing in your system?*

---

## 🔄 **EZF-001-2. Caching strategies: Cache Aside (Lazy Loading), Read-Through, Write-Through, Write-Around, Write-Behind (Write-Back), Cache Aside (Lazy Loading)**

![EZF Image](/images/blog/EZF-001-2.png)

### EZF-001-2.1. 💤📌Cache-Aside (Lazy Loading):
- 📜 Data is loaded into the cache on demand.
- 🔄 If data is not found in the cache, the application retrieves it from the datastore and then stores it in the cache.

🟢 Pros:
- 🎯 Only requested data is cached.
- 🔄 Cache can be easily refreshed.

🔴 Cons:
- ❌ Initial cache miss incurs a latency penalty.
- 🔄 Manual intervention required for cache updates.

### EZF-001-2.2. 📖🔍Read-Through:
- 📜 The cache is responsible for loading data from the datastore when a cache miss occurs.

🟢 Pros:
- 🔄 Automatic data loading.
- 🎯 Consistent cache and datastore data.

🔴 Cons:
- ❌ Initial cache miss can slow down the application.

### EZF-001-2.3. ✍️🔍Write-Through:
- 📜 Data is written to both the cache and the datastore synchronously (simultaneously).

🟢 Pros:
- ✅ Immediate data consistency.
- 🔄 Automatic data updates.

🔴 Cons:
- ❌ Slower write operations due to dual writes.

### EZF-001-2.4. ✏️🔄 Write-Around:
- 📜 Data is written directly to the datastore, bypassing the cache. The cache is updated later or during subsequent read operations.

🟢 Pros:
- ⚡ Faster initial write operations.
- 🎯 Reduces cache churn for less frequently accessed data.

🔴 Cons:
- ❌ Subsequent reads might suffer from cache misses.

### EZF-001-2.5. ✏️🔙Write-Behind (Write-Back):
- 📜 Data is first written to the cache, and then asynchronously written to the datastore.

🟢 Pros:
- ⚡ Fast write operations.
- 🔄 Asynchronous updates optimize datastore writes.

🔴 Cons:
- ❌ Risk of data loss if cache fails before async write.

❓ *What combination of caching strategies are you guys currently implementing in your system?*

---

## 🌐 **EZF-001-3. Differences Between API Gateway and Load Balancer**

![EZF Image](/images/blog/EZF-001-3.png)
📜 While both API Gateways and Load Balancers manage incoming requests, they serve different primary roles. In many architectures, especially in microservices, you'll often find both an API gateway and a load balancer working in tandem. An API Gateway focuses on API management, offering a suite of tools for processing and directing API calls. In contrast, a Load Balancer's main job is to distribute traffic to ensure optimal server performance and availability.

### EZF-001-3.1. API Gateway: 🌐 
**Primary Role:** Manages and processes API requests.

- **Functions:**
  - 🚦 Request Routing: Directs requests to the appropriate service.
  - 🧩 API Composition: Aggregates data from multiple services.
  - ⏳ Rate Limiting: Limits request frequency.
  - 🔒 Security: Manages authentication and API keys.
  - 🚀 Caching: Improves response times with stored data.
  - 🔄 Request/Response Transformation: Modifies data formats.
  - 📊 Analytics & Monitoring: Tracks API usage.
  - 🔍 Service Discovery: Identifies available services.
  - ❌ Error Handling & Retry: Manages failed requests.
  - 🔧 Protocol Translation: Converts communication protocols.

- **Use Cases:** Microservices, API management, data aggregation, securing APIs.

### EZF-001-3.2. Load Balancer: ⚖️ 
**Primary Role:** Distributes incoming network traffic.

- **Functions:**
  - 🌊 Traffic Distribution: Prevents server overloads.
  - ❤️ Health Checks: Monitors server health.
  - 🔐 SSL Termination: Handles SSL/TLS processing.
  - 🧬 Session Persistence: Maintains client-server connection.
  - 📡 Layer 4 and Layer 7 Load Balancing: Operates at transport and application layers.

- **Use Cases:** High availability, fault tolerance, application scaling, large-scale web traffic management.

**Key Differences:**
- 🎯 Focus: API gateway = API management. Load balancer = traffic distribution.
- 🔍 Granularity: API gateway = fine-grained control. Load balancer = broader network level.
- 🛠️ Features: API gateway = tailored for API management. Load balancer = traffic and health management.

In modern architectures, especially microservices, both API gateways and load balancers often work together. The load balancer manages traffic, while the API gateway handles API requests.

❓ Are you guys utilizing both API gateways and load balancers in your infrastructure?

## EZF-001-4. Linux commands. Part 1 (37 commands).
![EZF Image](/images/blog/EZF-001-4.png)
### File Operations 📂:
- **ls 📄:** List directory contents
  - Example: `ls -l`
- **cp 📋:** Copy files and directories
  - Example: `cp source.txt destination.txt`
- **mv 🚚:** Move or rename files and directories
  - `Example: mv oldname.txt newname.txt`
- **rm 🗑️:** Remove files or directories
  - `Example: rm unwanted.txt`
- **touch ✍️:** Create an empty file
  - `Example: touch newfile.txt`
- **cat 📖:** Concatenate and display file content
  - `Example: cat file.txt`

**Directory Operations** 📁:
- **pwd 📍:** Print working directory
  - `Example: pwd`
- **cd 🚪:** Change directory
  - `Example: cd /home/user/documents`
- **mkdir 🆕📁:** Make directories
  - `Example: mkdir new_directory`
- **rmdir 🚫📁:** Remove empty directories
  - `Example: rmdir empty_directory`

**System Info** ℹ️:
- **uname 🖥️:** Display system information
  - `Example: uname -a`
- **top 📊:** Display system tasks
  - `Example: top`
- **df 💽:** Disk space usage of file system
  - `Example: df -h`
- **free 🧠:** Display memory usage
  - `Example: free -m`
- **ps 🔄:** Display process status
  - `Example: ps aux`

**Permissions** 🔒:
- **chmod 🔑:** Change file mode bits
  - `Example: chmod 755 script.sh`
- **chown 👤:** Change file owner and group
  - `Example: chown user:group file.txt`
- **chgrp 👥:** Change group ownership
  - `Example: chgrp group file.txt`

**Networking** 🌐:
- **ping 📡:** Send ICMP ECHO_REQUEST to network hosts
  - `Example: ping google.com`
- **netstat 🌐📊:** Network statistics
  - `Example: netstat -tuln`
- **ifconfig 🌐🛠️:** Display or configure a network interface
  - `Example: ifconfig eth0`
- **ssh 🛡️:** Secure shell client (remote login program)
  - `Example: ssh user@hostname`
- **scp 📤:** Secure copy (remote file copy program)
  - `Example: scp file.txt user@hostname:/path/`

**Compression/Archiving** 🗜️:
- **tar 📦:** Tape archiver
  - `Example: tar -czvf archive.tar.gz folder/`
- **gzip 🗜️:** Compress or expand files
  - `Example: gzip file.txt`
- **gunzip 🗜️🔓:** Decompress files
  - `Example: gunzip file.txt.gz`
- **zip 🤐:** Package and compress files
  - `Example: zip archive.zip file1.txt file2.txt`
- **unzip 🤐🔓:** Extract compressed files in a ZIP archive
  - `Example: unzip archive.zip`

**Package Management** 📦:
- **apt-get 📥:** APT package handling utility (Debian-based systems)
  - `Example: sudo apt-get install package_name`
- **yum 📥:** Package manager for RPM-based systems
  - `Example: sudo yum install package_name`
- **dpkg 📥:** Package manager for Debian
  - `Example: sudo dpkg -i package.deb`

**Text Processing** 🔍:
- **grep 🔎:** Search text
  - `Example: grep "pattern" file.txt`
- **sed ✂️:** Stream editor
  - `Example: sed 's/old/new/g' file.txt`
- **awk 📝:** Pattern scanning and text processing language
  - `Example: awk '{print $1}' file.txt`

**Help & Output** 📘:
- **man 📚:** Display manual pages
  - `Example: man ls`
- **echo 🔊:** Display a line of text
  - `Example: echo "Hello, World!"`

**Process Management** ❌:
- **kill ☠️:** Terminate processes
  - `Example: kill -9 12345` (where 12345 is a process ID)

❓ **Which Linux commands do you find most frequently used in your daily operations?**



## EZF-001-5. Diagram as Code
![EZF Image](/images/blog/EZF-001-5.png)

Diagrams (Diagram as Code) allows you to create cloud system architecture diagrams using Python.

Originally designed for quick prototyping of new architectures without specialized design tools, it can also be employed to visualize or describe existing systems. The tool is versatile, supporting a wide range of major cloud providers like AWS, Azure, GCP, Kubernetes, Alibaba Cloud, and Oracle Cloud, as well as On-Premise nodes, SaaS platforms, and key programming languages and frameworks. One of its standout features is its compatibility with version control systems, enabling you to track changes to your architecture diagrams over time. Note: While Diagrams excels at creating architecture diagrams, it neither manages actual cloud resources nor generates cloud formation or terraform scripts. For a deeper dive, check out the optional 6-minute video below.
[![Watch the video](https://img.youtube.com/vi/wbjDTFDNIBo/maxresdefault.jpg)](https://youtu.be/wbjDTFDNIBo)


❓ Which tool or software are you guys utilizing to generate diagrams programmatically?

# EZF-002-1. Webhooks API Architecture style
![EZF Image](/images/blog/EZF-002-1.gif)


## EZF-002-1.1. Message formats:
- JSON

## EZF-002-1.2. ✅ Advantages:
- **Real-Time Notifications 🚨**: Immediate alerts without polling.
- **Event-Driven ⚡**: Supports dynamic, event-based interactions.
- **Reduced Server Load 📉**: Sends data only on events.
- **Configurable 🔧**: Tailored to specific events.
- **Simple to Use 🟢**: Generally straightforward implementation.
- **Asynchronous Operations 🔄**: Non-blocking data transfers.
- **Scalable 📈**: Adapts easily with growing needs.

## EZF-002-1.3. ❌ Disadvantages
- **Security Concerns 🔒**: Public endpoints may pose risks if not secured.
- **Error Handling ❌**: Challenges with endpoint failures or errors.
- **Latency Issues 🐢**: Network delays can affect real-time nature.
- **Resource Use 🔄**: Each call consumes server resources.
- **Debugging 🔍**: Complexity increases with third-party services.
- **Limited Filtering 🚫**: Some providers may lack detailed options.
- **Ordering 📦**: No guaranteed sequence for events.

## EZF-002-1.4. 📋 Use cases
- **Real-Time Notifications 🚨**: Immediate alerts for events like new posts.
- **CI/CD 🛠**: Trigger builds, tests, and deployments on code changes.
- **E-Commerce Updates 🛍**: Notify on order placements, payments, or stock changes.
- **CMS 📝**: Alerts on content changes.
- **Social Media Integration 📲**: Updates on posts and interactions.
- **Monitoring & Analytics 📊**: Alerts for system or security issues.
- **Chatbots 💬**: Notifications for new messages.
- **Payments 💳**: Status updates on transactions.
- **IoT Device Communication 🌐**: Send data when specific conditions are met by IoT devices.
- **Collaboration Tools Integration 🤝**: Notify on task updates or new messages in collaboration apps.

❓ **What API architecture style are you guys currently utilizing in your system?**

## EZF-002-2. Load Balancing Methods: Round Robin, Sticky Round Robin, Weighted Round Robin,IP Hash, Generic Hash, Least Connections, Least Time

![EZF Image](/images/blog/EZF-002-2.gif)
More detailed:
![EZF Image](/images/blog/EZF-002-2.png)

### EZF-002-2.1. 🔁Round Robin
Distributes requests sequentially across all servers in the pool. Simple and predictable.

**Type**: Static

**Pros**:
- 🟢 Easy Setup: Minimal configuration
- 🔁 Even Distribution: Suitable for testing.
- 📊 No Monitoring Needed: Rotates through servers.
- 🔄 Predictable: Can anticipate server handling.

**Cons**:
- ⚠️ Server Overload Risk: Can push servers to overload if they're already heavily loaded.
- 📏 Requires Similar Server Capacity: Best when all servers have roughly the same capacity.
- 📋 Content Uniformity Needed: Requires all servers to host the same content.

**Use Cases**:
- 🧪 Testing Environments: Balanced request distribution for testing.
- 🔄 Stateless Applications: For independent, session-less requests.
- 📏 Uniform Server Capacities: When all servers have similar resources.
- 🚀 Microservices: Even distribution across stateless services.

**Example (NGINX)**:
```json
upstream backend {
server s1.dmn.com;
server s2.dmn.com;
server s3.dmn.com;
}
```
### EZF-002-2.2. 🟢🔁 Sticky Round Robin
Distributes requests sequentially but ensures a user's subsequent requests stick to the initially assigned server, maintaining session persistence.

**Type**: Static

**Pros**:
- 📌 **Session Persistence**: Maintains user session data.
- 🚀 **Better User Experience**: No session timeouts or data loss.
- 🛠️ **Simpler App Design**: Assumes user requests hit the same server.

**Cons**:
- ⚖️ **Potential Imbalance**: Uneven load distribution.
- 📈 **Scaling Issues**: Challenges when adding new servers.
- 🔥 **Server Failure Impact**: Disruptions if a sticky server fails.

**Use Cases**:
- 🛒 **Web Apps with Sessions**: Maintains user carts and preferences.
- 🔐 **Authentication Systems**: Keeps users logged in across requests.
- 📝 **Multi-step Forms**: Remembers data across form pages.
- 🎥 **Streaming Services**: Consistent server connection during streams.
- 🎮 **Online Gaming**: Tracks player states and scores consistently.

**Example (NGINX+)**:
```json
upstream backend{
server s1.dmn.com;
server s2.dmn.com;
server s3.dmn.com;
sticky cookie srv_id expires=2h domain=.dmn.com path=/;
}
```
### EZF-002-2.3. ⚖️🔁Weighted Round Robin
Distributes requests based on assigned server weights, favoring servers with higher capacities or priorities.

**Type**: Static

**Pros**:
- **Adaptive Distribution 📊**: Suits servers with different capacities.
- **Flexibility 🔄**: Adjusts weights as server performance changes.
- **Efficient ⚙️**: Maximizes resource utilization without overloading.

**Cons**:
- **Complexity 🧩**: Requires monitoring and weight adjustments.
- **Potential Imbalance ⚠️**: Incorrect weights can lead to overloads.

**Use Cases**:
- **Mixed Server Capacities 🏢**: When servers have varying resources.
- **Dynamic Environments 🌪️**: Adapting to changing server performance.
- **Traffic Prioritization 🚦**: Directing more traffic to higher-performing servers.

**Example (NGINX)**:
```nginx
upstream backend {  
   server s1.dmn.com weight=3;   
   server s2.dmn.com weight=2;
   server s3.dmn.com weight=1;
}
```

### EZF-002-2.4. 🔗#️⃣IP Hash
Distributes requests based on a hash of the client's IP address, ensuring consistent routing to the same server for a specific IP.

**Type**: Static

**Pros**:
- **Session Persistence 📌**: Clients consistently directed to the same server.
- **Predictable Distribution 🔀**: Based on client IP hash, ensuring even load.

**Cons**:
- **Limited Flexibility ⛓️**: Hard to adjust once set up.
- **Imbalance Risk ⚠️**: Some servers might get more traffic if certain IP ranges are more active.

**Use Cases**:
- **Stateful Applications 🛒**: Where session data needs to be retained.
- **Geo-specific Content 🌍**: Serving content based on client's geographic location.
- **Security & Monitoring 🛡️**: Easier tracking and management of client sessions.

**Example (NGINX)**:
```nginx
upstream backend {
   ip_hash;  
   server s1.dmn.com weight=3;
   server s2.dmn.com weight=2;
   server s3.dmn.com weight=1;
}
```

### EZF-002-2.5. 🔳#️⃣Generic Hash
Distributes requests using a hash of customizable inputs, offering flexible and consistent routing based on various data points.

**Type**: Static

**Pros**:
- **Versatility 🌐**: Hashes on diverse inputs, including text, variables, or combinations like IP-port pairs or URIs.
- **Uniform Distribution 🔀**: Aims for even distribution across servers.

**Cons**:
- **Complexity 🧩**: Requires careful selection of hash function.
- **Potential Imbalance ⚠️**: Hash collisions or poor hash functions can skew distribution.

**Use Cases**:
- **Custom Inputs 🛠️**: Hash based on specific application data or headers.
- **Dynamic Environments 🌪️**: Where inputs for distribution change frequently.
- **Cache Distribution 💾**: Ensuring cached content is evenly distributed.

**Example (NGINX)**:
```nginx
upstream backend {
   hash $request_uri;  
   server s1.dmn.com weight=3;
   server s2.dmn.com weight=2;
   server s3.dmn.com weight=1;
}
```
### EZF-002-2.6. 🔌🔽Least Connections
Directs traffic to servers with the fewest active connections, optimizing for server availability.

**Type**: Dynamic

**Pros**:
- **Adaptive 🌐**: Directs traffic to less-busy servers.
- **Efficiency ⚙️**: Maximizes server utilization without overburdening.

**Cons**:
- **Delayed Reaction ⏱️**: Might not account for sudden server load spikes.
- **Potential Overhead 📊**: Requires monitoring of active connections.

**Use Cases**:
- **Varying Server Capacities 🏢**: Balances load in mixed-capacity environments.
- **High Traffic Sites 🚦**: Distributes large volumes of requests effectively.
- **Real-time Applications 🎮**: Where quick response times are crucial.

**Example (NGINX)**:
```nginx
upstream backend {
   least_conn;
   server s1.dmn.com;
   server s2.dmn.com;
   server s3.dmn.com;
}
```

### EZF-002-2.7. ⏱️🔽Least Time
Routes traffic to servers with the quickest response times, ensuring faster user experiences.

**Type**: Dynamic

**Pros**:
- **Fast Responses 🚀**: Prioritizes quickest servers.
- **Dynamic Adaptation 🌐**: Adjusts based on server response times.

**Cons**:
- **Monitoring Overhead 📊**: Requires continuous tracking of server latencies.
- **Fluctuation Risk ⚠️**: Rapid changes in response times can lead to frequent server switches.

**Use Cases**:
- **User Experience 🛍️**: Ensures users get the fastest server response.
- **High Demand Applications 🎥**: For services like video streaming where latency matters.
- **Variable Server Performance 📉**: Balances in environments with fluctuating server speeds.

**Example (NGINX+)**:
```nginx
upstream backend {
   least_time header;
   server s1.dmn.com;
   server s2.dmn.com;
   server s3.dmn.com;
}
```
❓ What combination of load balancing methods are you guys currently implementing in your system?

## EZF-002-3. HTTP Status Codes

HTTP status codes are three-digit responses sent by servers to indicate the outcome of a request. They categorize the result into five broad classes: informational (1xx), successful (2xx), redirection (3xx), client errors (4xx), and server errors (5xx). Understanding these codes is crucial as they provide insight into the success or failure of an HTTP request, helping diagnose issues, optimize user experience, and ensure smooth communication between client and server.

Short version:
![EZF Image](/images/blog/EZF-002-3s.png)

More detailed:
![EZF Image](/images/blog/EZF-002-3.png)

#### 1xx: Informational 🔄
- 100 Continue 📤
- 101 Switching Protocols 🔄
- 102 Processing ⏳
- 103 Early Hints 💡

#### 2xx: Successful ✅
- 200 OK 🆗
- 201 Created 🆕
- 202 Accepted 🔄
- 203 Non-Authoritative Information ℹ️
- 204 No Content 🚫
- 205 Reset Content 🔄
- 206 Partial Content ⏳
- 207 Multi-Status 📊
- 208 Already Reported 📢
- 226 IM Used 🔄

#### 3xx: Redirection ➡️
- 300 Multiple Choices 🤔
- 301 Moved Permanently ➡️
- 302 Found 🔄
- 303 See Other 👀
- 304 Not Modified 🔄
- 305 Use Proxy 🚧
- 307 Temporary Redirect ➡️
- 308 Permanent Redirect ➡️

#### 4xx: Client Errors ❌
- 400 Bad Request 🚫
- 401 Unauthorized 🔒
- 402 Payment Required 💰
- 403 Forbidden 🚷
- 404 Not Found 🕳️
- 405 Method Not Allowed ❌
- 406 Not Acceptable 🚫
- 407 Proxy Auth Required 🔒
- 408 Request Timeout ⏰
- 409 Conflict ⚠️
- 410 Gone 🕳️
- 411 Length Required ❗
- 412 Precondition Failed ❌
- 413 Payload Too Large 📦
- 414 URI Too Long 📏
- 415 Unsupported Media Type ❌
- 416 Range Not Satisfiable 🚫
- 417 Expectation Failed ❌
- 418 I'm a Teapot ☕ (April Fools' joke)
- 419 Page Expired ⏳
- 420 Method Failure/Enhance Your Calm 🚫
- 421 Misdirected Request ❗
- 422 Unprocessable Entity ❌ (WebDAV)
- 423 Locked 🔒 (WebDAV)
- 424 Failed Dependency ❌ (WebDAV)
- 425 Too Early ⏰
- 426 Upgrade Required ⬆️
- 428 Precondition Required ❗
- 429 Too Many Requests 🚫
- 430 HTTP Status Code 🚫
- 431 Headers Too Large 📏
- 440 Login Time-Out ⏰
- 444 No Response 🚫
- 449 Retry With 🔁
- 450 Blocked by Parental Controls 🔒
- 451 Legal Reasons ⚖️
- 460 Client Closed Connection Prematurely 🚫
- 463 Too Many Forwarded IP Addresses 🚫
- 494 Request Header Too Large 📏
- 495 SSL Certificate Error ❌
- 496 SSL Certificate Required 🔒
- 497 HTTP to HTTPS ❌
- 498 Invalid Token ❌
- 499 Token Required/Client Closed 🚫

#### 5xx: Server Errors🚨
- 500 Internal Server Error 🚨
- 501 Not Implemented ❌
- 502 Bad Gateway 🚧
- 503 Service Unavailable ⛔
- 504 Gateway Timeout ⏰
- 505 HTTP Version Not Supported ❌
- 506 Variant Also Negotiates 🔄
- 507 Insufficient Storage 💾 (WebDAV)
- 508 Loop Detected 🔁 (WebDAV)
- 509 Bandwidth Limit Exceeded 📊
- 510 Not Extended ➕
- 511 Network Authentication Required 🔒
- 520 Unknown Error ❓
- 521 Server Is Down ⛔
- 522 Timeout ⏰
- 523 Origin Unreachable 🚧
- 524 Timeout ⏰
- 525 SSL Handshake Failed 🔒
- 526 Invalid SSL Certificate ❌
- 527 Railgun Listener to Origin 🚄
- 529 Service Overloaded ⚠️
- 530 Site Frozen ❄️
- 598 Network Read Timeout ⏰
- 599 Network Connect Timeout

❓ Imagine you're designing a new HTTP status code that indicates a server has understood the request but refuses to fulfill it, not due to authorization issues but because it deems the request to be potentially harmful or malicious. What would you name this status code, and how would you differentiate its use from the existing 403 Forbidden and 451 Unavailable For Legal Reasons codes?

## EZF-002-4. Fundamental Latency Metrics to Remember

![EZF Image](/images/blog/EZF-002-4.png)

The numbers provided are approximate, based on figures from [Peter Norvig’s article](http://norvig.com/21-days.html#answers).

It's essential to have a general understanding of the orders of magnitude rather than the exact values for the following reasons:

- **Performance Optimization**: Helps identify system bottlenecks and areas for improvement.
  
- **System Design**: Guides decisions about data placement and communication strategies in distributed systems.
  
- **Realistic Expectations**: Sets achievable benchmarks for system operations.
  
- **Efficient Coding**: Enables developers to write latency-aware code, reducing wasteful operations.
  
- **Debugging**: Assists in quickly spotting performance anomalies.
  
- **User Experience**: Directly impacts how users perceive application responsiveness.
  
- **Cost Efficiency**: Faster operations can lead to savings, especially in cloud environments.
  
- **Educated Trade-offs**: Allows for informed decisions when balancing performance, cost, and reliability.

❓ Guys, if you had to design a real-time collaborative document editing platform (similar to Google Docs) where multiple users from around the world can edit a document simultaneously, which latency numbers would be most critical to consider, and how would they influence your design choices to ensure a seamless user experience?

## EZF-002-5. Git commands. Part 1 (21 commands).

![EZF Image](/images/blog/EZF-002-5.png)

### Use case: Developing a new feature for a web application.

- **Git config**: Before starting, Alice sets her Git username and email.
```
git config --global user.name "Alice Smith" git config --global user.email "alice.smith@example.com"
```
- **Git init**: Alice initializes a new Git repository for her project.
```
git init my-web-app
```
- **Git clone**: Bob wants to collaborate with Alice. He clones her repository.
```
git clone https://github.com/alice/my-web-app.git
```
- **Git status**: Alice checks the status of her files.
```
git status
```
- **Git add**: Alice adds a new file to the staging area.
```
git add index.html
```
- **Git commit**: Alice commits her changes with a message.
```
git commit -m "Added homepage."
```
- **Git push**: Alice pushes her changes to the remote repository.
```
git push origin master
```
- **Git branch**: Bob creates a new branch to work on a feature.
```
git branch feature-navbar
```
- **Git checkout**: Bob switches to his new branch.
```
git checkout feature-navbar
```
- **Git merge**: Alice merges Bob's feature branch into the master branch.
```
git merge feature-navbar
```
- **Git pull**: Bob pulls the latest changes from the remote repository.
```
git pull origin master
```
- **Git log**: Alice views the commit history.
```
git log
```
- **Git show**: Bob checks the details of the last commit.
```
git show
```
- **Git diff**: Alice checks the differences between her working directory and the last commit.
```
git diff
```
- **Git tag**: Alice tags the current commit as a new release.
```
git tag v1.0
```
- **Git rm**: Bob removes a file from the repository.
```
git rm old-file.txt
```
- **Git stash**: Alice temporarily saves her changes to work on something else.
```
git stash
```
- **Git reset**: Bob undoes the last commit, keeping the changes in the working directory.
```
git reset HEAD~1
```
- **Git revert**: Alice undoes a specific commit by creating a new commit.
```
git revert commit_id
```
- **Git remote**: Bob checks the remote repositories connected to his local repository.
```
git remote -v
```
- **Git fetch**: Alice fetches the latest changes from the remote repository without merging.
```
git fetch origin
```
## License

This project is licensed under the terms of the Creative Commons CC BY-NC-ND 4.0 license. For more details, see [LICENSE.md](LICENSE.md).


