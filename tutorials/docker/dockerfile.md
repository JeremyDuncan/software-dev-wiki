---
title: Dockerfile
description: Tutorial for Dockerfile Syntax
published: 1
date: 2023-11-09T04:43:35.291Z
tags: docker, dockerfile
editor: markdown
dateCreated: 2023-11-09T04:43:34.192Z
---

# Dockerfile Components Breakdown

This document provides an overview of various Dockerfile components such as environment variables, volumes, and port mappings.

## Environment Variables (`ENV`)
Environment variables are key-value pairs that are set during the image build and can be used to pass configuration to the application running inside the container.

ENV APP_HOME /usr/src/app
In this example, APP_HOME is set to /usr/src/app, which can be accessed by the application.

## Volumes (`VOLUME`)
Volumes are the preferred mechanism for persisting data generated by and used by Docker containers. They are directories (or files) that are outside of the default Union File System and exist as normal directories and files on the host filesystem.

VOLUME /var/lib/mysql
This line in the `Dockerfile` tells Docker to mount the `/var/lib/mysql` directory as a volume, which can be used for storing persistent data for a MySQL database.

## Port Mapping (`EXPOSE`)
`EXPOSE` informs Docker that the container listens on specific network ports at runtime. Note that `EXPOSE` does not make the ports of the container accessible to the host. To do that, you must use either the `-p` flag to publish a range of ports or the `-P` flag to publish all of the exposed ports when running `docker run`.

EXPOSE 80 443
This `Dockerfile` line indicates that the container will listen on ports 80 (HTTP) and 443 (HTTPS).

## Copying Files and Directories (`COPY` and `ADD`)
`COPY` and `ADD` instructions are used to copy new files and directories into the filesystem of the container.

COPY . /usr/src/app
This line copies everything from the current directory (where the `Dockerfile` is located) into the `/usr/src/app` directory inside the container.

## Running Commands (`RUN`)
The `RUN` instruction will execute any commands in a new layer on top of the current image and commit the results.

RUN apt-get update && apt-get install -y package
This command updates the package list and installs a package in the image.

## Setting the Working Directory (`WORKDIR`)
`WORKDIR` sets the working directory for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY` and `ADD` instructions that follow it.

WORKDIR /usr/src/app
This sets the working directory to `/usr/src/app`.

## Running the Main Process (`CMD` and `ENTRYPOINT`)
`CMD` sets default command and/or parameters, which can be overwritten from command line when Docker container runs.
`ENTRYPOINT` configures a container that will run as an executable.

CMD ["node", "app.js"]
This line provides defaults for an executing container and runs `app.js` using `node`.

By using these components, you can effectively build Docker images that are versatile and cater to the needs of your applications.

```Dockerfile
# ==============================================================================
# Use an official Node runtime as a parent image
# ------------------------------------------------------------------------------
FROM node:14-slim

# ==============================================================================
# Set the working directory in the container
# ------------------------------------------------------------------------------
WORKDIR /usr/src/app

# ==============================================================================
# Set environment variables
# ------------------------------------------------------------------------------
ENV NODE_ENV production
ENV PORT 3000

# ==============================================================================
# Install system dependencies
# ------------------------------------------------------------------------------
RUN apt-get update && apt-get install -y \
    curl \
    && rm -rf /var/lib/apt/lists/*

# ==============================================================================
# Copy the current directory contents into the container at /usr/src/app
# ------------------------------------------------------------------------------
COPY . .

# ==============================================================================
# Install any needed packages specified in package.json
# ------------------------------------------------------------------------------
RUN npm install --production

# ==============================================================================
# Make port 3000 available to the world outside this container
# ------------------------------------------------------------------------------
EXPOSE $PORT

# ==============================================================================
# Define volume /var/lib/app
# Volumes can be used for persistent data
# ------------------------------------------------------------------------------
VOLUME /var/lib/app

# ==============================================================================
# Run app when the container launches
# CMD sets default command and/or parameters, which can be overwritten from command line when container runs.
# ------------------------------------------------------------------------------
CMD ["node", "server.js"]

# ==============================================================================
# At the end, your application should be running on port 3000
# ------------------------------------------------------------------------------

