```
# Redis and Apache Setup with Docker

This guide provides a comprehensive tutorial on how to install and run Redis and Apache web server using Docker, and how to connect them for your development projects. The instructions focus on pulling a custom Redis Docker image and running it alongside Apache, demonstrating a basic integration for practical use.

---

## Table of Contents
- [Prerequisites](#prerequisites)
- [Step 1: Pull and Run the Custom Redis Docker Image](#step-1-pull-and-run-the-custom-redis-docker-image)
- [Step 2: Install and Run Apache Web Server](#step-2-install-and-run-apache-web-server)
- [Step 3: Connect Apache to Redis](#step-3-connect-apache-to-redis)
- [Testing Your Setup](#testing-your-setup)
- [Additional Notes](#additional-notes)
- [Troubleshooting](#troubleshooting)
- [References](#references)

---

## Prerequisites

Before starting, ensure you have the following installed and configured:

- [Docker](https://docs.docker.com/get-docker/) installed on your system.
- Basic familiarity with Docker commands.
- Administrative or sudo privileges to run Docker commands.
- Internet connection to pull Docker images.

---

## Step 1: Pull and Run the Custom Redis Docker Image

This guide uses a custom Redis image available on Docker Hub: `johnydi/custom-redis`.

### Pull the Redis Image

Open your terminal and run:

```
docker pull johnydi/custom-redis
```

This command fetches the latest version of the custom Redis image.

### Run the Redis Container

Run the following command to start Redis in detached mode and map the Redis default port 6379 to your localhost:

```
docker run -d -p 6379:6379 --name redis johnydi/custom-redis
```

- `-d` runs the container in the background (detached mode).
- `-p 6379:6379` exposes Redis default port 6379.
- `--name redis` names the container "redis" for easy reference.

Verify Redis is running:

```
docker ps
```

You should see the Redis container listed and running.

---

## Step 2: Install and Run Apache Web Server

You can run Apache either in a Docker container or install it directly on your machine.

### Option 1: Running Apache in Docker

Pull and run an official Apache image:

```
docker pull httpd
docker run -d -p 8080:80 --name apache-server httpd
```

- This command pulls the Apache HTTP Server image.
- It runs Apache on port 8080 on your local machine mapped to port 80 inside the container.

### Option 2: Installing Apache Directly

For example, on Ubuntu/Debian:

```
sudo apt update
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
```

Your Apache server should be running at `http://localhost` (or `http://localhost:8080` if using Docker).

---

## Step 3: Connect Apache to Redis

Redis is often used with web servers like Apache to manage sessions, cache data, or share state.

### Basic Example: Use Redis with a PHP Web Application under Apache

1. Install PHP and Redis PHP extension

- If Apache is running inside Docker, create a custom Dockerfile extending the Apache image to include PHP and the Redis PHP extension.
- If running locally, install PHP and Redis extension:

  ```
  sudo apt install php php-redis -y
  ```

2. Create a simple PHP script to test Redis connection:

Create `index.php` in Apache’s web root (`/var/www/html` or mounted directory):

```
<?php
$redis = new Redis();
$redis->connect('127.0.0.1', 6379);

$redis->set("tutorial-name", "Redis and Apache Integration");
echo "Stored string in Redis: " . $redis->get("tutorial-name");
?>
```

3. Access the PHP page via browser:

- If Apache is local: http://localhost/index.php
- If Apache is Docker container: http://localhost:8080/index.php

You should see the message confirming Redis and Apache are connected.

---

## Testing Your Setup

1. From the terminal, check if Redis container is running:

```
docker ps | grep redis
```

2. Test Apache by opening `http://localhost` or `http://localhost:8080`.

3. Test your PHP Redis connection script in the browser or command line.

---

## Additional Notes

- Ensure the Redis host IP matches the environment your Apache/PHP container or server is running in.
- For Dockerized Apache and Redis in separate containers in the same network, connect via container name:

```
$redis->connect('redis', 6379);
```

- For advanced setups, consider Docker Compose to orchestrate Apache, PHP, and Redis containers.

---

## Troubleshooting

- **Redis container not starting:** Check Docker logs with `docker logs redis`.
- **Cannot connect to Redis from PHP:** Verify Redis is listening on your network interface, check firewall rules.
- **PHP Redis extension errors:** Confirm the extension is installed and enabled in your PHP setup.

---

## References

- Redis Official Documentation: https://redis.io/docs/
- Docker Redis Images: https://hub.docker.com/r/johnydi/custom-redis
- Apache HTTP Server Documentation: https://httpd.apache.org/docs/
- PHP Redis Extension: https://github.com/phpredis/phpredis

---

This completes the full tutorial to install, run, and connect Redis with Apache using Docker for a basic web environment setup.

Happy coding!
```
