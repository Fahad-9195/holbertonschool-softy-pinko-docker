Docker Infrastructure Project
Description
This project involves building a containerized infrastructure using Docker. The setup consists of a reverse proxy/load balancer, two API application servers, and one front-end static-content server — all orchestrated using Docker Compose.
The goal is to gain hands-on experience with Docker containers, reverse proxies, and load balancing in a real-world-style deployment architecture.

Architecture Overview
Client
  |
  v
[Reverse Proxy / Load Balancer]   <-- single entry point
       |              |
       v              v
 [Front-end      [Load Balancer]
  Static Server]      |        \
                      v         v
               [API Server 1]  [API Server 2]
How Traffic Is Routed

All incoming client requests go through the reverse proxy server, which is the sole entry point.
If the request is for static content, it is forwarded to the front-end server. The response is then passed back through the proxy to the client.
If the request is for the API, the proxy applies a Round Robin load-balancing algorithm to route the request to one of the two API servers alternately.
At no point does the client communicate directly with the API servers or the front-end server.

Round Robin Load Balancing
Round Robin distributes incoming requests evenly across available servers in rotation:

Request 1 → API Server 1
Request 2 → API Server 2
Request 3 → API Server 1
Request 4 → API Server 2
...and so on

This ensures no single server is overwhelmed and each receives an equal share of traffic.

Requirements
Prerequisites

Docker Desktop installed on your local machine

Windows Installation Guide
Mac Installation Guide
Linux Installation Guide
Chromebook: Docker Engine only (results may vary — consider using a campus machine)




Project Structure
.
├── docker-compose.yml        # Orchestrates all containers
├── proxy/
│   └── Dockerfile            # Reverse proxy / load balancer (e.g., Nginx)
├── frontend/
│   └── Dockerfile            # Front-end static-content server
├── api/
│   └── Dockerfile            # API server (used for both instances)
└── README.md

Services
ServiceDescriptionReplicasproxyReverse proxy and load balancer1frontendServes static front-end content1apiApplication/API server2

Usage
Build and Start All Containers
bashdocker compose up --build
Stop All Containers
bashdocker compose down
View Running Containers
bashdocker ps
View Logs
bashdocker compose logs -f

Resources

Docker Official Documentation
Docker Cheat Sheet
What is a Reverse Proxy?
Docker Compose Overview
