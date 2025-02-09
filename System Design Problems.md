System Design Detail book - https://github.com/mehulrathod71/system-design

Design URL Shortener like TinyURL - https://dev.to/karanpratapsingh/system-design-url-shortener-10i5
https://www.geeksforgeeks.org/system-design-url-shortening-service/
Design Text Storage Service like Pastebin - https://medium.com/codex/designing-pastebin-77e6e86172eb
Design Leaderboard - https://medium.com/@mayilb77/design-a-real-time-leaderboard-system-for-millions-of-users-08b96b4b64ce
Design Content Delivery Network (CDN) - 	https://www.geeksforgeeks.org/designing-content-delivery-network-cdn-system-design/
Uber Design - https://www.geeksforgeeks.org/system-design-of-uber-app-uber-system-architecture/?ref=lbp
Netflix - https://www.geeksforgeeks.org/system-design-netflix-a-complete-architecture/?ref=lbp
Dropbox - https://www.geeksforgeeks.org/design-dropbox-a-system-design-interview-question/?ref=lbp
Vending Machine - https://www.geeksforgeeks.org/vending-machine-high-level-system-design/?ref=lbp
Tic Tac Toe - https://www.geeksforgeeks.org/low-level-design-of-tic-tac-toe-system-design/?ref=lbp
Design Parking lot - https://www.geeksforgeeks.org/designing-parking-lot-garage-system-system-design/
Design Key Value Storage - https://dev.to/zeeshanali0704/design-a-key-value-storage-n88
Distributed Design Cache - https://www.geeksforgeeks.org/design-distributed-cache-system-design/
Design Authentication System - https://www.geeksforgeeks.org/designing-authentication-system-system-design/
Design UPI - https://www.geeksforgeeks.org/designing-upi-system-design/
Design Whatsapp - https://www.geeksforgeeks.org/designing-whatsapp-messenger-system-design/
Design Spotify - https://levelup.gitconnected.com/system-design-interview-question-design-spotify-4a8a79697dda
Design Job Scheduler - https://www.geeksforgeeks.org/design-distributed-job-scheduler-system-design/
Design Notification Service - https://www.geeksforgeeks.org/design-notification-services-system-design/
Design Instagram - https://www.geeksforgeeks.org/design-instagram-a-system-design-interview-question/
Design Tinder - https://kasunprageethdissanayake.medium.com/tinder-fully-explained-system-design-and-architecture-1225ecdfe64e
Design Facebook - https://www.geeksforgeeks.org/design-facebook-system-design/
Design Twitter - https://www.geeksforgeeks.org/design-twitter-a-system-design-interview-question/
Design Reddit - https://www.geeksforgeeks.org/design-reddit-system-design/
Design Youtube - https://www.hellointerview.com/learn/system-design/problem-breakdowns/youtube
Design Search Engine - https://jc1175.medium.com/how-i-would-design-a-search-engine-9b423a18afe7
Design Ecommerce - https://medium.com/@ibrahim.zananiri/design-amazon-e-commerce-system-7f2dd57637bb
Design Tiktok - https://www.geeksforgeeks.org/designing-tiktok-system-design/
Design Spotify - https://blog.algomaster.io/p/design-spotify-system-design-interview
Design AirBnB - https://blog.bytebytego.com/p/a-brief-history-of-airbnbs-architecture
Google Search Autocomplete - https://www.geeksforgeeks.org/googles-search-autocomplete-high-level-designhld/
Design Rate Limiter - https://medium.com/geekculture/system-design-design-a-rate-limiter-81d200c9d392
https://www.geeksforgeeks.org/how-to-design-a-rate-limiter-api-learn-system-design/
Design Distributed Messaging - https://www.geeksforgeeks.org/distributed-messaging-system-system-design/
Design Expedia - https://medium.com/@abhishekranjandev/building-a-flight-reservation-system-like-expedia-9df3874c9960
Design Code Editor - https://www.geeksforgeeks.org/designing-online-code-editor-system-design/
Design Stock Exchange - https://www.geeksforgeeks.org/how-to-design-a-database-for-stock-trading-app-like-groww/
Design Logging - https://www.geeksforgeeks.org/centralized-logging-systems-system-design/
Design Payment Gateway - https://newsletter.pragmaticengineer.com/p/designing-a-payment-system
Design Digital Wallet - https://walletera.dev/designing-a-digital-wallet
Design Doordash - https://www.linkedin.com/pulse/system-design-architecture-food-delivery-app-like-durgesh-sharma-tdhec/
Design Google Doc - https://systemdesignschool.io/problems/google-doc/solution
Design Google Maps - https://www.geeksforgeeks.org/designing-google-maps-system-design/
Design Zoom - https://www.geeksforgeeks.org/designing-zoom-system-design/
Design Distributed System - https://www.geeksforgeeks.org/what-is-a-distributed-system/
Design Book my Show - https://medium.com/@prithwish.samanta/online-movie-ticket-booking-platform-system-design-e-g-bookmyshow-69048440901c
Design Web Crawler - https://www.geeksforgeeks.org/design-web-crawler-system-design/
Design CI/CD design - https://www.geeksforgeeks.org/cicd-pipeline-system-design/
Design S3 - https://www.codesmith.io/blog/diagramming-system-design-s3-storage-system
Design Slack - https://systemdesign.one/slack-architecture/
https://scaleyourapp.com/system-design-case-study-real-time-messaging-architecture/
Design Live Comments - https://systemdesign.one/live-comment-system-design/



Design Stock Exchange 

Designing a stock exchange system involves creating a platform that efficiently matches buyers and sellers of securities. Here's a detailed overview of the high-level design (HLD) and low-level design (LLD):

### **High-Level Design (HLD)**

**1. Requirements:**
- **Functional Requirements:**
  - **Order Placement:** Users can place buy and sell orders.
  - **Order Matching:** Match buy and sell orders based on price and time priority.
  - **Order Types:** Support various order types such as market orders, limit orders, and stop orders.
  - **Real-Time Data:** Provide real-time updates on stock prices and order book.
  - **User Accounts:** Manage user accounts and portfolios.
  - **Risk Management:** Implement risk checks to ensure compliance and prevent fraud.

- **Non-Functional Requirements:**
  - **Scalability:** Handle high volumes of transactions and users.
  - **High Availability:** Ensure the system is always available.
  - **Low Latency:** Provide quick order execution and real-time updates.
  - **Security:** Protect user data and prevent unauthorized access.

**2. Architecture Components:**
- **API Gateway:** Routes requests to the appropriate service.
- **Order Management System (OMS):** Handles order placement, modification, and cancellation.
- **Matching Engine:** Matches buy and sell orders based on price and time priority.
- **Market Data Service:** Provides real-time updates on stock prices and order book.
- **User Account Service:** Manages user accounts, portfolios, and authentication.
- **Risk Management Service:** Performs risk checks and ensures compliance.
- **Database:** Stores user data, orders, and transaction history.
- **Cache:** Stores frequently accessed data to reduce latency.
- **Load Balancer:** Distributes incoming requests across multiple instances.

**3. Workflow:**
- **Order Placement:**
  - User places an order through the API Gateway.
  - API Gateway routes the request to the Order Management System.
  - Order Management System validates the order and forwards it to the Matching Engine.
  - Matching Engine attempts to match the order with existing orders in the order book.
  - If matched, the transaction is executed and recorded in the database.
  - If not matched, the order is added to the order book.

- **Real-Time Data:**
  - Market Data Service continuously updates stock prices and order book.
  - Users receive real-time updates through WebSocket connections.

### **Low-Level Design (LLD)**

**1. Database Schema:**
- **User Table:**
  - `user_id` (Primary Key)
  - `username` (Text, Unique)
  - `password_hash` (Text)
  - `email` (Text, Unique)
  - `created_at` (Timestamp)

- **Order Table:**
  - `order_id` (Primary Key)
  - `user_id` (Foreign Key)
  - `stock_symbol` (Text)
  - `order_type` (Text)
  - `quantity` (Integer)
  - `price` (Decimal)
  - `status` (Text)
  - `created_at` (Timestamp)

- **Transaction Table:**
  - `transaction_id` (Primary Key)
  - `buy_order_id` (Foreign Key)
  - `sell_order_id` (Foreign Key)
  - `stock_symbol` (Text)
  - `quantity` (Integer)
  - `price` (Decimal)
  - `executed_at` (Timestamp)

**2. Matching Engine Algorithm:**
- **Order Matching:**
  - Use a priority queue to manage buy and sell orders.
  - Match orders based on price and time priority.
  - Execute transactions and update the order book accordingly.

**3. Caching Strategy:**
- Use Redis to cache frequently accessed data such as user portfolios and order book.
- Implement cache invalidation policies to keep the cache updated.

**4. API Endpoints:**
- **POST /orders:** Place a new order.
- **GET /orders/{order_id}:** Retrieve order details.
- **GET /market-data:** Get real-time market data.
- **POST /users:** Create a new user account.
- **POST /login:** Authenticate a user.

**5. Load Balancing:**
- Use a load balancer (e.g., AWS ELB) to distribute traffic across multiple instances of the services.

**6. Security Measures:**
- Implement rate limiting to prevent abuse.
- Use HTTPS to secure data in transit.
- Validate and sanitize input to prevent SQL injection and other attacks.
- Implement two-factor authentication (2FA) for user accounts.

**7. Monitoring and Logging:**
- Use tools like Prometheus and Grafana for monitoring system performance.
- Implement logging for all requests and responses to aid in debugging and analytics.

### **Scalability Considerations:**
- **Database Sharding:** Distribute the database across multiple shards to handle large volumes of data[1](https://www.youtube.com/watch?v=2rMJguHuqoA).
- **Replication:** Use database replication to ensure high availability and fault tolerance[2](https://www.youtube.com/watch?v=DH2-vDPFiE4).
- **Auto-Scaling:** Automatically scale the number of service instances based on traffic load[3](https://www.youtube.com/watch?v=PzuL3lxtrs0).

### **Security Considerations:**
- **Rate Limiting:** Prevent abuse by limiting the number of requests from a single IP address[1](https://www.youtube.com/watch?v=2rMJguHuqoA).
- **Authentication and Authorization:** Ensure only authorized users can place orders and access account information[2](https://www.youtube.com/watch?v=DH2-vDPFiE4).
- **Data Encryption:** Encrypt sensitive data both in transit and at rest[3](https://www.youtube.com/watch?v=PzuL3lxtrs0).

### **Monitoring and Analytics:**
- **Logging:** Track all requests and responses for debugging and analytics[1](https://www.youtube.com/watch?v=2rMJguHuqoA).
- **Metrics:** Monitor key performance indicators like request latency, error rates, and transaction volumes[2](https://www.youtube.com/watch?v=DH2-vDPFiE4).
- **Alerts:** Set up alerts for unusual activity or system failures[3](https://www.youtube.com/watch?v=PzuL3lxtrs0).

Would you like to dive deeper into any specific aspect of this design?

[1](https://www.youtube.com/watch?v=2rMJguHuqoA): Code Recipe
[2](https://www.youtube.com/watch?v=DH2-vDPFiE4): System Design One
[3](https://www.youtube.com/watch?v=PzuL3lxtrs0): DEV Community

## Design Distributed Locking Service
Designing a distributed locking service involves creating a system that ensures mutual exclusion across distributed nodes, preventing concurrent processes from interfering with each other. Here's a detailed overview of the high-level design (HLD) and low-level design (LLD):

### **High-Level Design (HLD)**

**1. Requirements:**
- **Functional Requirements:**
  - Acquire and release locks.
  - Ensure mutual exclusion, so only one client can hold a lock at a time.
  - Support lock timeouts to prevent deadlocks.
  - Provide lock status queries.

- **Non-Functional Requirements:**
  - High availability and fault tolerance.
  - Low latency for lock acquisition and release.
  - Scalability to handle a large number of clients and locks.
  - Security to prevent unauthorized access to locks.

**2. Architecture Components:**
- **API Gateway:** Routes requests to the appropriate service.
- **Lock Service:** Manages lock acquisition, release, and status queries.
- **Distributed Consensus System:** Ensures consistency and fault tolerance (e.g., ZooKeeper, etcd, or Consul).
- **Database:** Stores lock metadata and state.
- **Cache:** Stores frequently accessed lock information to reduce latency.
- **Load Balancer:** Distributes incoming requests across multiple instances of the lock service.

**3. Workflow:**
- **Lock Acquisition:**
  - Client sends a request to acquire a lock.
  - API Gateway routes the request to the Lock Service.
  - Lock Service checks the lock status in the distributed consensus system.
  - If the lock is available, it is granted to the client and the status is updated.
  - If the lock is not available, the client is informed or the request is queued.

- **Lock Release:**
  - Client sends a request to release a lock.
  - API Gateway routes the request to the Lock Service.
  - Lock Service updates the lock status in the distributed consensus system.
  - The lock is made available for other clients.

### **Low-Level Design (LLD)**

**1. Database Schema:**
- **Lock Table:**
  - `lock_id` (Primary Key)
  - `owner_id` (Text)
  - `status` (Text)
  - `created_at` (Timestamp)
  - `expires_at` (Timestamp, Optional)

**2. Lock Acquisition Algorithm:**
- **Steps:**
  - Generate a unique identifier for the lock request.
  - Check the lock status in the distributed consensus system.
  - If the lock is available, set the lock status to "acquired" with the client identifier.
  - If the lock is not available, return a failure response or queue the request.

**3. Lock Release Algorithm:**
- **Steps:**
  - Verify the client identifier matches the lock owner.
  - Update the lock status to "released" in the distributed consensus system.
  - Notify any queued requests that the lock is now available.

**4. Caching Strategy:**
- Use Redis to cache frequently accessed lock information.
- Implement cache invalidation policies to keep the cache updated.

**5. API Endpoints:**
- **POST /locks/acquire:** Acquire a lock.
- **POST /locks/release:** Release a lock.
- **GET /locks/status/{lock_id}:** Query the status of a lock.

**6. Load Balancing:**
- Use a load balancer (e.g., AWS ELB) to distribute traffic across multiple instances of the Lock Service.

**7. Security Measures:**
- Implement rate limiting to prevent abuse.
- Use HTTPS to secure data in transit.
- Validate and sanitize input to prevent SQL injection and other attacks.
- Implement authentication and authorization to ensure only authorized clients can acquire and release locks.

**8. Monitoring and Logging:**
- Use tools like Prometheus and Grafana for monitoring system performance.
- Implement logging for all requests and responses to aid in debugging and analytics.

### **Scalability Considerations:**
- **Database Sharding:** Distribute the database across multiple shards to handle large volumes of data[1](https://martin.kleppmann.com/2016/02/08/how-to-do-distributed-locking.html).
- **Replication:** Use database replication to ensure high availability and fault tolerance[2](https://www.alibabacloud.com/knowledge/developer1/design-model-of-distributed-locks).
- **Auto-Scaling:** Automatically scale the number of service instances based on traffic load[3](https://www.alibabacloud.com/blog/the-technical-practice-of-distributed-locks-in-a-storage-system_597141).

### **Security Considerations:**
- **Rate Limiting:** Prevent abuse by limiting the number of requests from a single IP address[1](https://martin.kleppmann.com/2016/02/08/how-to-do-distributed-locking.html).
- **Authentication and Authorization:** Ensure only authorized clients can acquire and release locks[2](https://www.alibabacloud.com/knowledge/developer1/design-model-of-distributed-locks).
- **Data Encryption:** Encrypt sensitive data both in transit and at rest[3](https://www.alibabacloud.com/blog/the-technical-practice-of-distributed-locks-in-a-storage-system_597141).

### **Monitoring and Analytics:**
- **Logging:** Track all requests and responses for debugging and analytics[1](https://martin.kleppmann.com/2016/02/08/how-to-do-distributed-locking.html).
- **Metrics:** Monitor key performance indicators like request latency, error rates, and lock acquisition times[2](https://www.alibabacloud.com/knowledge/developer1/design-model-of-distributed-locks).
- **Alerts:** Set up alerts for unusual activity or system failures[3](https://www.alibabacloud.com/blog/the-technical-practice-of-distributed-locks-in-a-storage-system_597141).

Would you like to dive deeper into any specific aspect of this design?

[1](https://martin.kleppmann.com/2016/02/08/how-to-do-distributed-locking.html): [Martin Kleppmann](https://martin.kleppmann.com/2016/02/08/how-to-do-distributed-locking.html)
[2](https://www.alibabacloud.com/knowledge/developer1/design-model-of-distributed-locks): [Alibaba Cloud](https://www.alibabacloud.com/knowledge/developer1/design-model-of-distributed-locks)
[3](https://www.alibabacloud.com/blog/the-technical-practice-of-distributed-locks-in-a-storage-system_597141): [Wikipedia](https://en.wikipedia.org/wiki/Distributed_lock_manager)


# Design Data Intensive application

"Designing Data-Intensive Applications" by Martin Kleppmann provides a comprehensive guide to building reliable, scalable, and maintainable data systems. Here are some key principles and considerations from the book that are essential for designing data-intensive applications:

### **Key Principles:**

1. **Reliability:**
   - **Fault Tolerance:** Design systems to handle hardware failures, software bugs, and human errors gracefully.
   - **Replication:** Use data replication to ensure availability and durability.
   - **Backups:** Regularly back up data to prevent data loss.

2. **Scalability:**
   - **Horizontal Scaling:** Scale out by adding more machines rather than scaling up with more powerful machines.
   - **Partitioning:** Distribute data across multiple nodes using techniques like sharding.
   - **Load Balancing:** Distribute incoming requests evenly across servers to prevent bottlenecks.

3. **Maintainability:**
   - **Operability:** Ensure the system is easy to operate, monitor, and debug.
   - **Simplicity:** Keep the system design simple to reduce complexity and potential errors.
   - **Evolvability:** Design the system to accommodate future changes and new requirements.

### **System Design Considerations:**

1. **Data Models:**
   - **Relational Databases:** Use for structured data with complex queries and transactions.
   - **NoSQL Databases:** Use for unstructured or semi-structured data, high write throughput, and flexible schemas.
   - **Graph Databases:** Use for data with complex relationships and connections.

2. **Storage and Retrieval:**
   - **Indexing:** Use indexes to speed up data retrieval.
   - **Caching:** Use caching to reduce latency and improve performance.
   - **Compression:** Compress data to save storage space and reduce I/O.

3. **Consistency Models:**
   - **Strong Consistency:** Guarantees immediate consistency across all nodes.
   - **Eventual Consistency:** Allows temporary inconsistencies but guarantees eventual consistency.
   - **Causal Consistency:** Ensures operations that are causally related are seen in the correct order.

4. **Data Processing:**
   - **Batch Processing:** Process large volumes of data in batches using tools like Hadoop.
   - **Stream Processing:** Process data in real-time using tools like Apache Kafka and Apache Flink.
   - **Lambda Architecture:** Combine batch and stream processing to handle both real-time and historical data.

5. **Distributed Systems:**
   - **Consensus Algorithms:** Use algorithms like Paxos or Raft to achieve consensus in distributed systems.
   - **Leader Election:** Designate a leader node to coordinate tasks and manage state.
   - **Quorum-Based Replication:** Use quorum-based approaches to ensure data consistency and availability.

### **Practical Examples:**
- **Case Studies:** The book provides real-world examples and case studies from major online services to illustrate the application of these principles.
- **Trade-Offs:** It discusses the trade-offs involved in choosing different technologies and architectures, helping you make informed decisions based on your specific requirements.

These principles and considerations form the foundation for designing robust data-intensive applications. If you have any specific questions or need further details on any of these topics, feel free to ask!

[1](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321): [Amazon](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321)
[2](https://martin.kleppmann.com/2017/03/27/designing-data-intensive-applications.html): [Martin Kleppmann's Publications](https://martin.kleppmann.com/2017/03/27/designing-data-intensive-applications.html)
[3](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781098119058/): [O'Reilly Media](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781098119058/)