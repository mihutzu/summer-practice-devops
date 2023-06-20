**Docker Compose Basics:**

1. **Define Services:**
   - Use the `services` keyword to define the services in your Compose file.
   - Example:
     ```yaml
     services:
       web:
         build: .
         ports:
           - "80:80"
     ```

2. **Build Images:**
   - Use the `build` keyword to specify the build context and Dockerfile for a service.
   - Example:
     ```yaml
     services:
       web:
         build:
           context: .
           dockerfile: Dockerfile
     ```

3. **Set Environment Variables:**
   - Use the `environment` keyword to set environment variables for a service.
   - Example:
     ```yaml
     services:
       web:
         environment:
           - MY_VAR=my_value
     ```

4. **Mount Volumes:**
   - Use the `volumes` keyword to mount volumes for a service.
   - Example:
     ```yaml
     services:
       web:
         volumes:
           - ./app:/app
     ```

5. **Define Dependencies:**
   - Use the `depends_on` keyword to specify dependencies between services.
   - Example:
     ```yaml
     services:
       web:
         build: .
       db:
         image: postgres:latest
         depends_on:
           - web
     ```

6. **Run Commands:**
   - Use the `command` keyword to override the default command for a service.
   - Example:
     ```yaml
     services:
       web:
         build: .
         command: python app.py
     ```

7. **Start Services:**
   - Use the `docker-compose up` command in your terminal to create and start all services defined in the Compose file.
   - Example: `docker-compose up`

8. **Stop Services:**
   - Use the `docker-compose down` command in your terminal to stop and remove all containers, networks, and volumes created by `up`.
   - Example: `docker-compose down`
