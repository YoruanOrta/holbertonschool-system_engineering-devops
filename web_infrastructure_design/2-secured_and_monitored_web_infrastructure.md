# 2. Secured and Monitored Web Infrastructure

**Diagram**:  
[View Diagram](https://imgur.com/a/S56ddvj)

## ✅ Components and Why They're Added

### 🔐 Firewalls (3)
- Protect public entry points and internal servers.
- Allow only necessary traffic (e.g., port 443 for HTTPS, port 3306 for MySQL internally).
    - One firewall in front of the Load Balancer.
    - One firewall for the app servers.
    - One firewall for the MySQL database servers.

### 🔒 SSL Certificate
- Used on the Load Balancer to serve `https://www.foobar.com`.
- Encrypts data between the user's browser and the server, ensuring confidentiality and integrity.

### 📈 Monitoring Clients (3)
- Collect performance and health metrics.
- Installed on all web/app servers.
- Forward logs and metrics to monitoring services like **Sumo Logic**, **Datadog**, or **Prometheus**.

---

## 🔍 Key Concepts Explained

### 🔥 What Are Firewalls For?
- Control traffic flow based on rules.
- Protect infrastructure from unauthorized access or malicious traffic.

### 🌐 Why Serve Over HTTPS?
- Encrypts the connection between users and the web server.
- Prevents eavesdropping, man-in-the-middle attacks, and data tampering.
- Essential for security and trust.

### 📊 What Is Monitoring For?
- Detect failures, performance bottlenecks, or traffic surges.
- Enables alerting and automated scaling/failover decisions.

### 🔄 How Does Monitoring Collect Data?
- Monitoring agents run on servers and:
    - Collect logs (e.g., Nginx access/error logs).
    - Collect system metrics (CPU, RAM, disk, network).
    - Send data to a central service via HTTPS or TCP.

### ❓ How to Monitor QPS (Queries Per Second)?
- Enable Nginx or app server access logging.
- Use tools like:
    - `GoAccess` for real-time log analytics.
    - `Prometheus` + `Grafana` for QPS dashboards.
    - Configure monitoring agents to extract QPS from logs or metrics.

---

## ⚠️ Issues With This Infrastructure

### 🔐 SSL Termination at Load Balancer
- **Problem**: SSL is decrypted at the Load Balancer, then traffic to the backend is unencrypted.
- **Risk**: Internal traffic can be sniffed if not secured.
- **Solution**: Use **end-to-end encryption** (re-encrypt to the backend) or internal TLS.

### 🛢️ Single MySQL Write Node
- **Problem**: Only one node accepts writes.
- **Risk**: If the primary fails, writes are impossible.
- **Solution**: Add automated failover or multi-master replication (with caution).

### 📦 Identical Server Roles (App + DB)
- **Problem**: Database, app, and web logic run on the same server.
- **Risk**: High coupling makes it hard to scale or isolate bottlenecks.
- **Solution**: Use dedicated database servers and decouple components (microservices or layered architecture).

---