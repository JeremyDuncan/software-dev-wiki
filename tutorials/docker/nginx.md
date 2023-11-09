---
title: NGINX Web Server
description: Tutorial for the NGINX Web Server Container
published: 1
date: 2023-11-09T04:40:28.909Z
tags: container, docker, nginx, webserver
editor: markdown
dateCreated: 2023-11-09T04:22:03.921Z
---

# Docker Tutorial on NGINX Webserver

## What is NGINX?

NGINX is a high-performance HTTP server and reverse proxy, as well as an IMAP/POP3 proxy server. It is known for its high performance, stability, rich feature set, simple configuration, and low resource consumption.

NGINX is often used as a load balancer and HTTP cache in combination with other web servers. It excels in serving static content quickly and is designed to pass dynamic requests off to other software that is better suited for those purposes.

## Pros of Using NGINX

- **Performance**: NGINX can handle an extremely high number of concurrent connections with a low memory footprint.
- **Reverse Proxy**: It provides an efficient reverse proxy to manage the traffic to your web applications.
- **Load Balancing**: NGINX can distribute traffic across different backend servers for better load distribution.
- **Configuration**: It offers a powerful configuration language that is both straightforward and flexible.
- **Caching**: Built-in caching of content leads to reduced server load and faster response times.
- **Security**: Offers robust security features, including protection against DDoS attacks.

## How to Use NGINX

NGINX can be used to serve static files such as HTML, CSS, and JavaScript, proxy HTTP requests to other servers, handle SSL/TLS encryption, and much more. It’s configured by editing its text-based configuration files, where you can set up virtual hosts, manage access control, rewrite URLs, and set up redirects among other things.

## Setting Up NGINX with Docker

Here’s a simple step-by-step guide to setting up NGINX using Docker.
Refer to [Dockerfile Tutorial](/tutorials/docker/dockerfile) for more information on Dockerfile syntax.

### Step 1: Pull the NGINX Docker Image

To get started, pull the latest NGINX image from the Docker Hub:

	docker pull nginx


## Step 2: Run NGINX in a New Docker Container
You can run NGINX within a Docker container and expose it on port 8080:

	docker run --name some-nginx -p 8080:80 -d nginx

This command will start an NGINX container named `some-nginx` and bind port 8080 on your host to port 80 on the container.

## Step 3: Accessing NGINX
Once the container is running, open your web browser and navigate to:

	http://localhost:8080

You should see the default NGINX welcome page.

## Step 4: Customizing NGINX Configuration
To customize the NGINX configuration, you can mount a custom configuration file into the container:

1. Create an `nginx.conf` file on your host machine.
2. Mount it into your container:

	   docker run --name some-custom-nginx -v /path/to/your/nginx.conf:/etc/nginx/nginx.conf:ro -p 8080:80 -d nginx

Make sure to replace `/path/to/your/nginx.conf` with the actual path to your custom configuration file.

## Step 5: Serving Content with NGINX
To serve your own content instead of the default NGINX page, you can mount a directory:

	docker run --name some-nginx -v /path/to/your/content:/usr/share/nginx/html:ro -p 8080:80 -d nginx

Replace `/path/to/your/content` with the path to the directory that contains your HTML files.

## Conclusion
NGINX is a versatile web server that can be easily set up in a Docker environment. Its lightweight nature and ability to handle a large number of connections make it an ideal choice for modern web applications.

