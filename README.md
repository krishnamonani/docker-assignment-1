# docker-assignment-1
# Dockerized Web Application

## Objective
This project demonstrates the creation of a simple web application, containerization using Docker, and deploying it on a local environment with Nginx.

## Steps to Complete the Assignment

### 1. Create a Web Application
Developed a simple web application using Python (Flask) to serve as the backend. The application is structured as follows:

```
/app
├── app.py
├── requirements.txt
├── Dockerfile
├── README.md
```

### 2. Write a Dockerfile (Multi-Stage Build)

```dockerfile
# Stage 1: Build dependencies in a full Python image
FROM python:3.9-slim AS builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Stage 2: Use a lightweight runtime environment
FROM python:3.9-alpine
WORKDIR /app
COPY --from=builder /usr/local/lib/python3.9/site-packages /usr/local/lib/python3.9/site-packages
COPY app.py .

# Run the application
CMD ["python", "app.py"]
```

### 3. Build the Docker Image
To build the image with a minimized size:

```sh
docker build -t my-web-app .
```

### 4. Push Image to Docker Hub with Tags
Tag and push the image with at least three versions:

```sh
docker tag my-web-app mydockerhubusername/my-web-app:v1.0

docker tag my-web-app mydockerhubusername/my-web-app:latest

docker push mydockerhubusername/my-web-app:v1.0

docker push mydockerhubusername/my-web-app:latest
```

### 5. Run the Docker Container

```sh
docker run -d -p 5000:5000 --name web-container my-web-app
```

Access the application at `http://localhost:5000`.

### 6. Start an Nginx Container

```sh
docker run -d --name nginx-container -p 8080:80 nginx
```

### 7. Check Connectivity Between Containers
To verify connectivity between the application and Nginx:

```sh
docker exec -it web-container sh
ping nginx-container
```

### 8. Push Everything to GitHub
The project is available on [GitHub](https://github.com/your-repo-link-here).
The repository includes:

- `Dockerfile`
- `app.py`
- `requirements.txt`
- `README.md`
- `screenshots/` (folder containing all screenshots of steps)

## Notes
- No existing applications from labs were used.
- Environment variables are not hardcoded.
- Screenshots for each step are included in the repository.

## Conclusion
This project showcases the ability to containerize a simple web application, optimize the image size, deploy using Docker, and establish connectivity between containers using Nginx.

