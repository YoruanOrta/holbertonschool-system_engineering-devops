# 1. Distributed Web Infrastructure

## Diagram  
![Distributed Web Infrastructure](https://imgur.com/a/ztZOm8n)

## Components
- **1 Load Balancer** (HAProxy)
- **2 Web/App Servers**
    - Nginx
    - Application code
    - MySQL database (Primary + Replica)

## Why These Components?
- **Load Balancer**: Ensures high availability and distributes traffic.
- **Multiple Servers**: Provide redundancy and scalability.
- **Primary-Replica MySQL**: Provides data redundancy and separates read/write loads.

## Load Balancer
- **Algorithm**: Round Robin – cycles requests across both servers.
- **Setup**: Active-Active – both servers handle traffic simultaneously.

## Database Replication
- **Primary Node**: Handles all write operations.
- **Replica Node**: Receives data updates and serves read-only requests.
- Ensures data durability and load distribution.

## Issues
- **Single Point of Failure (SPOF)**: Load balancer has no backup.
- **Security**: No firewall, no HTTPS encryption.
- **No Monitoring**: No tracking of server health, traffic, or alerts.