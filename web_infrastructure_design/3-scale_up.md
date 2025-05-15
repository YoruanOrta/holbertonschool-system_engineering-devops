# 3. Scale Up - Web vs Application Servers

**Diagram**:  
![Infrastructure Diagram](https://imgur.com/a/rypbq6j)

## ✅ Infrastructure Overview

This setup demonstrates a properly scaled and decoupled web infrastructure:

### 🔄 Load Balancer Cluster (HAProxy)
- Two HAProxy instances configured in **Active-Passive** mode.
- One actively balances traffic; the other serves as a hot standby.
- Ensures **high availability** in case one load balancer fails.

### 🌐 Web Servers (Nginx)
- Host **static content** (HTML, CSS, JS, images).
- Forward dynamic requests to application servers.
- Adding multiple Nginx servers improves performance and redundancy.

### ⚙️ Application Servers
- Run application logic (e.g., Python Flask, Node.js, Django).
- Connect to the backend database.
- Separated from the web server to scale independently.

### 🛢️ Database Server (MySQL)
- Centralized data storage.
- All app servers communicate with a **single MySQL server** (can be upgraded to a Primary-Replica setup later).

---

## 💡 Why These Components Are Added

### ➕ Additional Server
- Improves capacity and performance.
- Isolates roles and enhances fault tolerance.

### ➕ Second Load Balancer
- Prevents a **Single Point of Failure (SPOF)** in traffic distribution.
- Provides **redundancy** and seamless failover with an HA setup.

### ⚙️ Split Web/App/DB Servers
- Enhances **scalability**: Web and app layers can grow independently.
- Improves **security**: Access control per layer (e.g., DB not exposed to the internet).
- Promotes **performance tuning**: Each server can be optimized for its specific task.

---

## 🆚 Web Server vs Application Server

| Component          | Purpose                                   | Examples              |
|---------------------|-------------------------------------------|-----------------------|
| **Web Server**      | Handles HTTP requests, serves static files | Nginx, Apache         |
| **Application Server** | Runs backend logic, generates responses | Gunicorn, uWSGI, Node.js |

---

## ✅ Key Takeaways

- Load balancers enhance **availability** and **traffic distribution**.
- Web servers focus on **serving content** and **proxying requests**.
- Application servers handle **processing logic**.
- Splitting roles achieves **better architecture**, **isolation**, and **scalability**.