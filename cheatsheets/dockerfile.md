**Dockerfile Basics:**

1. **Specify Base Image:**
   - Use the `FROM` keyword to specify the base image.
   - Example: `FROM ubuntu:latest`

2. **Copy Files:**
   - Use the `COPY` or `ADD` keywords to copy files from the host to the container.
   - Example: `COPY app.py /app`

3. **Set Working Directory:**
   - Use the `WORKDIR` keyword to set the working directory inside the container.
   - Example: `WORKDIR /app`

4. **Run Commands:**
   - Use the `RUN` keyword to execute commands inside the container during build time.
   - Example: `RUN pip install -r requirements.txt`

5. **Expose Ports:**
   - Use the `EXPOSE` keyword to specify which ports the container listens on at runtime.
   - Example: `EXPOSE 80`

6. **Set Environment Variables:**
   - Use the `ENV` keyword to set environment variables inside the container.
   - Example: `ENV MY_VAR=my_value`

7. **Define Entrypoint/Command:**
   - Use the `CMD` or `ENTRYPOINT` keywords to specify the command to run when the container starts.
   - Example: `CMD ["python", "app.py"]`
