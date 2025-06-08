---
layout: single
title:  "How to start with Docker"
date:   2025-06-08 10:00:00 +0100
categories: tutorials
tags: docker python poetry
---

We will install Docker and learn how to dockerize a Python app with Poetry dependency management in three incremental steps: running a Docker container, dockerizing a simple Python app, and finally dockerizing a Python app with Poetry.

Docker is a powerful tool that enables developers to package applications and their dependencies into a portable container. If you're new to Docker, this guide will help you understand the basics and get your first containers up and running — fast.

[**Official Docs**](https://docs.docker.com/get-started/)

## 🔧 Installation (Windows)

1. Download Docker Desktop for Windows.
2. Open CMD as Administrator.
3. Run the installer with administrative privileges:

```
"Docker Desktop Installer.exe" install --always-run-service
```

After installation, you will need to restart your PC.

## ▶️ Running Your First Docker Container

Let’s start by running a test container.
In PowerShell, run

```
docker run -d -p 8080:80 docker/welcome-to-docker
```

What Does This Do?
- `docker run` starts a container.
- `-d` runs it in detached (background) mode.
- `-p 8080:80` maps your machine's port 8080 to the container's port 80.
- `docker/welcome-to-docker` is the Docker image to run.

Now, open your browser and go to [http://localhost:8080](http://localhost:8080) to see the running app.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/docker-congrats.png){: .align-center}

## 🐍 Dockerizing a Python App

Take a Python app you want to dockerize. Suppose you have a folder with a Python application `app.py`. You should also add a `requirements.txt` file listing any package dependencies (skip this if there are none).

For testing, write this minimal code in `app.py`:
```
print("Hello World!")
```
Since there are no dependencies, you can omit `requirements.txt`.

Next, create a file without extension named `Dockerfile`. That's the key file Docker needs to set up the container. Insert this into the file:  

```
# Use the official Python image from the Docker Hub
FROM python:3.9-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . .

# Run the Python script
CMD ["python", "app.py"]
```  

In PowerShell, navigate to your project folder and build the Docker image:

```
docker build -t my-python-app .
```
 
This tells Docker to build an image named `my-python-app` using the Dockerfile in the current directory (`.`).

Finally, run the Docker container with:

```
docker run my-python-app
```

This will run `my-python-app` container, which will execute the `app.py` script and print "Hello from Docker!" to the console. Yay!

## 🧪 Dockerizing a Python App with Poetry

The last step is including `Poetry` package management. We will use my tiny project `esa-obs-stats` ([available on GitHub](https://github.com/Shavril/esa-obs-stats)) as an example. Your project folder should contain:
- main.py
- poetry.lock
- pyproject.toml

Create `Dockerfile` with following content: 

```
# Use the official Python image from the Docker Hub
FROM python:3.10-slim

# Install curl and build-essentials
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl build-essential && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Install poetry
RUN curl -sSL https://install.python-poetry.org | python3 - \
    && ln -s /root/.local/bin/poetry /usr/local/bin/poetry

# Set the working directory inside the container
WORKDIR /app

# Copy all project files, including README.md, pyproject.toml, poetry.lock, source code
COPY . /app

# Install dependencies
RUN poetry config virtualenvs.create false \
    && poetry install --no-root --no-interaction --no-ansi

# Run the Python script
# Specifies the command to run your Python script when the container starts.
CMD ["python", "main.py"]

```

Notes:
- `curl` and `build-essentials` are needed to install Poetry.
- Installing `Poetry` via the official installer, instead of `pip install poetry`, ensures we get the recommended version.
- Virtual environment is disabled, since the Docker container is already isolated. We install the dependencies globally in the container.  
- `--no-root` parameter prevents Poetry from installing the app as a package, because there is no `__init__.py`. 
- The container runs `"main.py"` when started.

Then in PowerShell, go into the folder of the Python project 
and build the Docker image:

```
docker build -t esa-obs-stats .
```
 
Run the container: 

```
docker run --rm esa-obs-stats
```

To interact with the container in a terminal session (e.g., if your app requires input):  
```
docker run --it --rm esa-obs-stats
```

Oops! The app generates `result.txt` file, but we do not see it in our folder as we should. The file stayed inside the Docker container. To get the file out, we map our current folder as a volume:

```
docker run --rm -v ${PWD}:/app esa-obs-stats
```

How does it work?
- `-v` option mounts a local folder into the container.
- `${PWD}` resolves to our project folder `C:/esa-obs-stats/`
- `/app` is the working directory inside the container, specified in Dockerfile's `WORKDIR /app`
- `-v ${PWD}:/app` tells Docker: “mount my current folder into the container at /app”
- Because the app writes to `result.txt` in the current working directory, it will now write to `C:/esa-obs-stats/result.txt` on our PC, even when running in Docker.

Now you’re ready to start shipping Python applications with Docker like a pro.  
Happy containerizing! 🐳
 