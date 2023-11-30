# Docker Projects with Traefik

Welcome to my Docker Projects repository! 🐳 Here, I explore the power of Docker alongside Traefik, a versatile reverse proxy and load balancer. This project demonstrates the orchestration of services using Traefik to distribute incoming HTTP(S) and TCP requests.

## Overview

In this repository, I've implemented a basic Docker project using Traefik as a load balancer. The project includes the following services:

- **whoami:** A container that exposes an API to show its IP address.
- **getting-started:** A simple container using the `docker/getting-started` image.
- **catapp:** A dog GIF generator with versions for both cats and dogs.

## Traefik Features and Middlewares

The Traefik setup in this project includes various features and middlewares:

- **Web UI:** Access the Traefik dashboard at [http://localhost:8080](http://localhost:8080).
- **HTTP and HTTPS Routing:** Services are exposed through routing rules, enhancing accessibility.
- **Middleware Examples:**
  - `test-compress`: Compresses responses for optimized data transfer.
  - `test-auth`: Implements basic authentication for secure access.
  - `test-ratelimit`: Implements rate limiting to control request traffic.

## Networking Enhancement

To further enhance security and accessibility, I've set up a virtual private network using Tailscale. This ensures that the Docker environment works seamlessly within the Tailscale network.

## Usage

To run this project locally, follow these steps:

1. Ensure you have Docker installed.
2. Clone this repository.
3. Navigate to the project directory and run `docker-compose up -d`.

Visit the Traefik dashboard at [http://localhost:8080](http://localhost:8080) to monitor and manage your services.

## Code Snippet

```yaml
# Example snippet from docker-compose.yml
version: '3'

services:
  reverse-proxy:
    image: traefik:v2.9
    command: --api.insecure=true --providers.docker --providers.docker.exposedByDefault=false
    ports:
      - "80:80"
      - "8080:8080"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      # Additional volumes as needed

  whoami:
    image: traefik/whoami
    labels:
      - "traefik.http.routers.whoami.rule=Host(`Fernoss.tail935af.ts.net`)"
      - "traefik.enable=true"

  # Additional services and configurations...
