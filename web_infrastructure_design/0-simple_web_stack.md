# 0. Simple Web Stack

## Diagram

![Simple Web Stack Diagram](https://imgur.com/a/XHJ6tUH)

## Explanations

- **Server**: A computer that provides services (web, app, DB) over a network.  
- **Domain name**: Human-readable address mapped to an IP.  
- **www record**: A DNS A record pointing to `8.8.8.8`.  
- **Web server (Nginx)**: Handles HTTP(S) requests and serves static content.  
- **App server**: Processes dynamic content and runs site logic.  
- **Database (MySQL)**: Stores and retrieves structured data.  
- **Communication**: Uses HTTP/HTTPS to communicate with user browsers.

## Issues

- **SPOF**: Single server failure results in a full outage.  
- **Downtime during deployment**: Restarting the web/app server causes downtime.  
- **No scalability**: Cannot handle high traffic without scaling components.