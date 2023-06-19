## Dockerizing a Python App

This guide will walk you through the process of Dockerizing a Python application built with FastAPI.

### Prerequisites

Before you begin, make sure you have the following prerequisites:

1. Docker installed on your machine. You can download and install Docker from the official website: [https://www.docker.com/](https://www.docker.com/)

2. Basic understanding of Python, Docker & Git

### Step 1: Fork & clone the repo

First, let's fork the repository then clone it and navigate into it:

```bash
git clone https://github.com/YOUR_USER/summer-devops.git
cd summer-devops
```

### Step 2: Dockerfile

The Dockerfile is a text file that contains a set of instructions to build a Docker image. Use the empty file named `Dockerfile` in the project directory and open it in a text editor.

<details> 
    <summary>You can try and create the Dockerfile yourself or use the following code</summary>

    # Use the official Python base image
    FROM python:3.9-slim
    
    # Set the working directory inside the container
    WORKDIR /app
    
    # Copy the requirements.txt file to the container
    COPY requirements.txt .
    
    # Install the Python dependencies
    RUN pip install --no-cache-dir -r requirements.txt
    
    # Copy the rest of the application code to the container
    COPY ./app .
    
    # Expose the port on which the FastAPI app will run
    EXPOSE 8000
    
    # Start the FastAPI app
    CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]

</details>

### Step 3: Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. It allows you to specify the services, networks, and volumes required for your application in a YAML file.

Use the existent file named `docker-compose.yml` in the project directory and open it in a text editor.

<details> 
    <summary>You can try and create the docker-compose.yaml yourself or use the following code</summary>

    version: '3'
    services:
      app:
        build:
          context: .
          dockerfile: Dockerfile
        ports:
          - 8000:8000

</details> 

### Step 4: Build and Run the Docker Container

Open a terminal or command prompt and navigate to the project directory (`summer-devops`).

To build the Docker image, run one of the following commands:

```bash
docker build -t dockerized-python-app .
```

or

```bash
docker-compose build
```

Once the build process is complete, you can run the Docker container with one of the following commands:

```bash
docker run --it --rm -p 8000:8000 dockerized-python-app
```

or

```bash
docker-compose up
```

### Step 5: Test the App

Open your web browser and visit `http://localhost:8000/` to see the "OK" message. You can also try accessing `http://localhost:8000/af` to see the "Freak" message.

Congratulations! You have successfully Dockerized your Python.

### Additional Notes

- You can stop the running Docker container by pressing `Ctrl+C` in the terminal or command prompt where the container is running.

- If you make changes to your application code or Dockerfile, you will need to rebuild the Docker image using the `docker-compose build` command before running it again.

- Remember to shut down the Docker container when you're done by running `docker-compose down` or by pressing `Ctrl+C` in the project directory.

That's it! You now have a Dockerized Python app. Happy coding!
