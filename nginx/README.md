# NGINX Local Load Balancing Example

## Overview

This repository provides an example of configuring NGINX for local load balancing on a single server.

## Notes

- **Reverse Proxying**: NGINX can act as a reverse proxy server, forwarding client requests to backend server.
- **Load Balancing**: NGINX can distribute incoming requests across multiple backend servers to improve performance, scalability, and fault tolerance. It supports various load balancing algorithms such as round-robin, least connections, and IP hash.
- **SSL Termination**: NGINX can handle SSL/TLS termination, offloading encryption and decryption from backend servers. This improves performance and simplifies certificate management.
- **Security**: NGINX provides security features such as access control, rate limiting, and Web Application Firewall (WAF) capabilities. It helps protect against cyber threats, unauthorized access, and malicious attacks.
- **Static Content Serving**: NGINX is efficient at serving static content (e.g., HTML, CSS, JavaScript files, images) directly to clients. This reduces the load on backend servers and improves overall response times.

## NGINX Configuration

```nginx
http {
    upstream backend {
        server 127.0.0.1:3000;
        server 127.0.0.1:3001;
        server 127.0.0.1:3002;
    }

    server {
        listen 80;

        location / {
            proxy_pass http://backend;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
        }
    }
}
```
This NGINX configuration sets up a reverse proxy to distribute incoming requests to three backend servers running on localhost and ports 3000, 3001, and 3002.