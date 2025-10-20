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

