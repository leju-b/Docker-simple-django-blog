# **Simple Django App Dockerization**

## **Project Overview**

This project involves developing a simple Django application, containerizing it with Docker, and deploying it on an EC2 instance. The app will be built and run in a Docker container on EC2, and then pushed to DockerHub for easy access and sharing.

## **Tech Stack**

- **Backend:** Django
- **Containerization:** Docker
- **Deployment:** AWS EC2
- **Container Registry:** DockerHub

## **Getting Started**

### **Prerequisites**

Ensure you have the following installed:

- **Docker:** [Install Docker](https://docs.docker.com/get-docker/)
- **AWS CLI:** [Install AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
- **EC2 Instance:** Set up an EC2 instance with Docker installed.

### **Installation**

1. **Fork the repository:**

2. **Build the Docker image:**

   ```bash
   docker build -t yourusername/Docker-simple-django-blog .
   ```

3. **Run the Docker container:**

   ```bash
   docker run -d -p 8000:8000 yourusername/Docker-simple-django-blog
   ```

4. **View the app:**

   Open your web browser and navigate to `http://localhost:8000/` to see the Django app running locally.

### **Pushing to GitHub**

1. **Initialize a Git repository:**

   ```bash
   git init
   ```

2. **Add and commit your files:**

   ```bash
   git add .
   git commit -m "Initial commit"
   ```

3. **Push to GitHub:**

   ```bash
   git remote add origin https://github.com/yourusername/simple-django-docker.git
   git push -u origin main
   ```

### **Deploying on EC2**

1. **SSH into your EC2 instance:**

   ```bash
   ssh -i your-key.pem ubuntu@your-ec2-public-ip
   ```

2. **Clone your GitHub repository:**

   ```bash
   git clone https://github.com/yourusername/simple-django-docker.git
   cd simple-django-docker
   ```

3. **Build the Docker image on EC2:**

   ```bash
   docker build -t yourusername/simple-django-app .
   ```

4. **Run the Docker container on EC2:**

   ```bash
   docker run -d -p 8000:8000 yourusername/simple-django-app
   ```

5. **View the app from EC2:**

   Open your web browser and navigate to `http://your-ec2-public-ip:8000/` to see the Django app running from your EC2 instance.

### **Pushing to DockerHub**

1. **Log in to DockerHub:**

   ```bash
   docker login
   ```

2. **Tag your Docker image:**

   ```bash
   docker tag yourusername/simple-django-app yourusername/simple-django-app:v1
   ```

3. **Push the image to DockerHub:**

   ```bash
   docker push yourusername/simple-django-app:v1
   ```

## **Configuration**

### **Dockerfile**

Here’s a basic Dockerfile used to containerize the Django app:

```Dockerfile
# Use an official Python runtime as a parent image
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Make port 8000 available to the world outside this container
EXPOSE 8000

# Define environment variable
ENV DJANGO_ENV=production

# Run the command to start uWSGI
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```
The docker file uses the base image of Linux which is python slim for a Django app.

### **requirements.txt**

Specify the dependencies needed for the Django app:

```
Django==4.0.4
```

## **Usage**

- **Starting the container:**
  ```bash
  docker start container_id
  ```

- **Stopping the container:**
  ```bash
  docker stop container_id
  ```

- **Checking logs:**
  ```bash
  docker logs container_id
  ```

## **Future Improvements**

- **Automate the deployment** with CI/CD pipelines.
- **Scale the application** using Docker Swarm or Kubernetes.
- **Secure the application** with HTTPS and environment variable management.

## **Thanks**

A special shoutout to Abhishek Veeramalla for his incredibly helpful [DevOps playlist](https://www.youtube.com/playlist?list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa). His content was instrumental in guiding me through this process—if you're looking to level up your DevOps skills, I highly recommend checking it out! 🙌

## **License**

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
