Below are two simple Dockerfiles suitable for beginners learning Docker. Both use **Nginx** to serve the application.

## **1. Static Website – HTML, CSS, JavaScript**

**Project structure:**

```
static-website/
├── index.html
├── style.css
├── script.js
└── Dockerfile
```

**Dockerfile**

```

# Use Nginx base image
FROM nginx:alpine

# Remove default Nginx files
RUN rm -rf /usr/share/nginx/html/*

# Copy website files
COPY . /usr/share/nginx/html/

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]

```

**Build and run:**

```
# Build Docker image
docker build -t static-website .

# Run container
docker run -d -p 8080:80 --name my-static-site static-website
```

Open: `http://localhost:8080`

## **2. React Application**

For React, we first build the application using Node.js and then serve the production build using Nginx. This is called a **multi-stage Docker build**.

**Project structure:**

```
react-app/
├── public/
├── src/
├── package.json
├── package-lock.json
└── Dockerfile
```

**Dockerfile**

```

# Stage 1: Build React application
FROM node:22-alpine AS build

# Set working directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm ci

# Copy source code
COPY . .

# Build React application
RUN npm run build


# Stage 2: Serve using Nginx
FROM nginx:alpine

# Copy production build to Nginx
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]

```

**Important:** This example assumes Create React App, which generates the `build` directory. If your React project uses Vite, replace:

```
COPY --from=build /app/build /usr/share/nginx/html
```

with:

```
COPY --from=build /app/dist /usr/share/nginx/html
```

**Build and run:**

```
# Build Docker image
docker build -t react-website .

# Run container
docker run -d -p 8081:80 --name my-react-site react-website
```

Open: `http://localhost:8081`

## **3. Quick comparison**

| Feature           | Static Website | React           |
| ----------------- | -------------- | --------------- |
| Base image        | Nginx          | Node.js + Nginx |
| Build required    | No             | Yes             |
| Build stages      | 1              | 2               |
| Port              | 80             | 80              |
| Production server | Nginx          | Nginx           |

## **4. Useful Docker commands for students**

```
# List running containers
docker ps

# View all containers
docker ps -a

# View container logs
docker logs my-react-site

# Stop container
docker stop my-react-site

# Remove container
docker rm my-react-site

# List Docker images
docker images

# Remove image
docker rmi react-website
```

**Teaching point:** Explain to students that the static website does not require compilation, whereas React needs a build process that converts the source code into optimized static assets. Nginx serves the final files in both cases.
