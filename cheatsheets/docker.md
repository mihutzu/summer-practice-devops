**Docker Basics:**

1. **Images:**
   - `docker pull <image_name>`: Download an image from Docker Hub.
   - `docker images`: List all downloaded images.
   - `docker rmi <image_name>`: Remove an image.

2. **Containers:**
   - `docker run <image_name>`: Create and start a container from an image.
   - `docker ps`: List running containers.
   - `docker stop <container_id>`: Stop a running container.
   - `docker rm <container_id>`: Remove a stopped container.
   - `docker exec -it <container_id> <command>`: Execute a command inside a running container.

3. **Volumes:**
   - `docker volume create <volume_name>`: Create a named volume.
   - `docker run -v <volume_name>:<container_path> <image_name>`: Mount a volume in a container.
   - `docker volume rm <volume_name>`: Remove a named volume.

4. **Networking:**
   - `docker run -p <host_port>:<container_port> <image_name>`: Publish a container's port to the host.
   - `docker network create <network_name>`: Create a custom network.
   - `docker run --network=<network_name> <image_name>`: Attach a container to a custom network.
