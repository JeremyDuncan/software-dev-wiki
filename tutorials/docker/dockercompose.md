---
title: Docker Compose
description: Tutorial on Docker Compose
published: 1
date: 2023-11-09T04:50:42.360Z
tags: docker, docker-compose
editor: markdown
dateCreated: 2023-11-09T04:50:41.246Z
---

# Docker Compose File Breakdown

This document explains the structure and syntax of a `docker-compose.yml` file used to define and run multi-container Docker applications.



```yaml
# Define the version of the Compose file format
version: '3.8'

# Define services, which are containers that make up your application
services:
  
  # A service named 'web' for a web application
  web:
    # Specify the Docker image to use
    image: nginx:alpine
    # Define the ports forwarding - the format is <host>:<container>
    ports:
      - "80:80"
    # Set environment variables
    environment:
      - NGINX_HOST=foobar.com
      - NGINX_PORT=80
    # Mount volumes - the format is <host>:<container>
    volumes:
      - ./html:/usr/share/nginx/html
    # Define dependency on another service, ensuring it starts first
    depends_on:
      - app

  # A service named 'app' for the main application
  app:
    # Build from a Dockerfile located in the specified directory
    build: ./app
    # Map the container port to the host
    ports:
      - "3000:3000"
    # Mount volume for persistent storage
    volumes:
      - app_data:/var/lib/app_data
    # Set the environment file
    env_file:
      - .env

  # A service for a database
  db:
    image: postgres:latest
    volumes:
      - db_data:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=exampleuser
      - POSTGRES_PASSWORD=examplepass
      - POSTGRES_DB=exampledb

# Define networks for communication between containers
networks:
  app_net:
    driver: bridge

# Define volumes for persistent data storage
volumes:
  app_data:
    driver: local
  db_data:
    driver: local

# This docker-compose file runs three services: `web`, `app`, and `db`, each configured for a specific role within the application.

# Notes:
# - `version` specifies which version of the Docker Compose file format we're using
# - `services` is where you define your app's services
# - `web`, `app`, and `db` are examples of individual services that make up the app
# - `image` specifies which Docker image to use for the service
# - `build` specifies the location of the Dockerfile for building the image
# - `ports` allows you to map ports from the host to the container
# - `environment` is for setting environment variables within the container
# - `volumes` is for persistent data and mounting paths between the host and container
# - `networks` defines the networking for your services
```


