# **1. Start with a real-world problem: "It works on my machine!"**

Imagine a company has developed an application. The developer says:

"My application works perfectly on my laptop, but when I deploy it to the production server, it doesn't work."

Why?

- Developer uses Node.js 20, but the server has Node.js 16.
- Developer uses a different Python version.
- Some dependencies are missing.
- Database configurations are different.
- Operating system configurations differ.

Ask your students:

**How can we make sure that an application runs exactly the same way on every machine?**

Introduce Docker.

[Why Every Backend Developer Should Learn Docker (Even If You Hate DevOps) | by Mohit Bisht | CodeToDeploy | Dec, 2025 | Medium](https://images.openai.com/static-rsc-4/xUEoA2VAKHLT7XfK6E9aTRPdugc4NfBUbuqnj9U2w-RmaEnOgrPLHvOU4-CR82ue5_8mfHDMc4ocOvqKHNUbwdIPpeAhuRlSBlPorYna2BwQWsbc7uIRa-ji9AM4ZylEUEW0fMeWoFXW1HYeIMbVsEeuVuWYlLni_jh0ghJVdC4?purpose=inline)

[medium.com](https://medium.com/codetodeploy/why-every-backend-developer-should-learn-docker-even-if-you-hate-devops-69ef4051c0b4?utm_source=chatgpt.com)

Explain:

Docker packages an application along with its dependencies and configuration into a portable container.

The same container can run on:

- Developer's laptop.
- Testing environment.
- AWS EC2.
- Azure Virtual Machine.
- On-premises servers.

This is the first real-world use case they should understand.

# **2. Teach Docker using a real-world application**

I recommend building a small e-commerce application throughout.

Imagine a company called ShopEase.

[Deploy a simple 3-tier Application using Docker Compose | by Prerana Blown Lama | Feb, 2026 | Medium](https://images.openai.com/static-rsc-4/FI23M8jxw3Wy6IbzWLc6Y57PyEF3TzX0nO0N7yn_Zfs0iGf0M2zF3C1x65Rn_YtCaq59jAfDqlUyUv1wXWLhOrKcW-sDkl3YeCKAa2qiW3cgE3zxMpCyyN2uq9ANKqb5UGkaHgBnqFw9sgwySYNeoFJlQofVtb2uVvxX0Wat1pU?purpose=inline)

[medium.com](https://medium.com/%40preranablama/deploy-a-simple-3-tier-application-using-docker-compose-6c7b706095f0?utm_source=chatgpt.com)

The application contains:

| Component  | Technology | Purpose                          |
| ---------- | ---------- | -------------------------------- |
| Frontend   | React      | User interface                   |
| Backend    | Node.js    | Business logic                   |
| Database   | MySQL      | Store products and users         |
| Cache      | Redis      | Improve performance              |
| Web Server | Nginx      | Serve frontend and reverse proxy |

Explain that each component can run inside its own container.

This is where Docker becomes interesting.

# **3. Your Docker teaching roadmap**

I would divide the course into six practical stages.

## **Docker learning journey**

1. **Stage 1 – Docker fundamentals**

   Beginner
   - What is Docker?
   - Why Docker?
   - Virtual Machines vs Containers
   - Docker architecture
   - Docker Engine
   - Docker Desktop
   - Images vs Containers
2. **Stage 2 – Docker commands**
   - docker pull
   - docker images
   - docker run
   - docker ps
   - docker stop
   - docker start
   - docker rm
   - docker logs
   - docker exec
   - Port mapping
3. **Stage 3 – Dockerfile**
   - What is a Dockerfile?
   - FROM
   - WORKDIR
   - COPY
   - RUN
   - EXPOSE
   - CMD vs ENTRYPOINT
   - Build custom images
   - Image optimization basics
4. **Stage 4 – Docker storage and networking**
   - Container filesystem
   - Volumes
   - Bind mounts
   - Bridge networking
   - Container-to-container communication
   - Persistent database storage
5. **Stage 5 – Docker Compose**
   - What is Docker Compose?
   - docker-compose.yml
   - Multiple containers
   - Environment variables
   - Service dependencies
   - Networks and volumes
6. **Stage 6 – Docker in production**
   - Docker Hub
   - Image tagging
   - Pushing and pulling images
   - Multi-stage builds
   - Container security basics
   - Deploy application on AWS EC2
   - Basic CI/CD integration

# **4. Practical demonstrations for every concept**

Here is how I would teach each topic using an actual use case.

## **Practical 1: Run your first container**

**Real-world scenario:** A company needs to run a web server without manually installing and configuring Nginx.

Ask students to execute:

```
docker pull nginx
```

Run the container:

```
docker run -d -p 8080:80 --name myweb nginx
```

Explain every parameter:

| Command    | Meaning                     |
| ---------- | --------------------------- |
| docker run | Create and run container    |
| -d         | Run in background           |
| -p 8080:80 | Host port to container port |
| --name     | Give container a name       |
| nginx      | Image name                  |

Open:

`http://localhost:8080`

[Exploring Microsoft Radius Application Platform - The New Stack](https://images.openai.com/static-rsc-4/TVh8NxOjrWasvQG3Ae95i_dL5bEu1nzCiftb6WYyr_LjVr4xiLzAtNVMkOMzC6ltoVuIbgWdRjISZ7WqIkfxo7zjjKHoeRP3LtK6wQOdnmlLpvhqERsg61q_SmMtQ8oMgSVNPldOcUffitxZS8h-BHqaUXWQmQKL24qPYpJdOz0?purpose=inline)

[thenewstack.io](https://thenewstack.io/exploring-microsoft-radius-application-platform/?utm_source=chatgpt.com)

**Student task:** Run two different Nginx containers on ports 8080 and 8081.

## **Practical 2: Understand Dockerfile**

**Real-world scenario:** Your development team has created a Node.js application. You need to package it so that it can run on any server with Docker.

Create a project:

```
mkdir docker-demo
cd docker-demo
```

Create `app.js`:

```
const http = require('http');

const server = http.createServer((req, res) => {
    res.end('Hello from Docker Container!');
});

server.listen(3000, '0.0.0.0', () => {
    console.log('Server running on port 3000');
});
```

Create `package.json`:

```
{
  "name": "docker-demo",
  "version": "1.0.0",
  "main": "app.js"
}
```

Create `Dockerfile`:

```
FROM node:20-alpine

WORKDIR /app

COPY package.json .

COPY app.js .

EXPOSE 3000

CMD ["node", "app.js"]
```

Build the image:

```
docker build -t my-node-app:v1 .
```

Run it:

```
docker run -d -p 3000:3000 my-node-app:v1
```

Open:

`http://localhost:3000`

[Day — 21 Learning DevOps \[DOCKER 🐳 — Build Docker image for a sample backend app (Node).\] WEEK 3️⃣: DAY 2️⃣) | by Muralidharan Vivekananthan | Medium](https://images.openai.com/static-rsc-4/meoCnPujEh6aLIwmkrRKROcbshoNzdBwqw4Ql5guurpiltc8gEBsfiRUN086mcEbkEt945DmPdsjKjZ-SsKwU3G8TpysDaPFArAlJfukjuq9jndtzChbn907pNasOfkIZZMFnw5ET89e6nk2qpttRm7qfcZiRVLfnujVjdor9fM?purpose=inline)

[medium.com](https://medium.com/%40muralidharan_vivekananthan/day-21-learning-devops-docker-build-docker-image-for-a-sample-backend-app-node-be47ebd45bb5?utm_source=chatgpt.com)

Now students understand the relationship:

**Application Source Code**

app.js + package.json

**Dockerfile**

Instructions to build the image

**Docker Image**

Packaged application

**Docker Container**

Running application instance

## **Practical 3: Docker Volumes**

**Real-world scenario:** A company runs a MySQL database inside a Docker container.

What happens if someone deletes the container?

Without persistent storage, the data stored in its writable container filesystem can be lost.

Demonstrate:

```
docker volume create mysql-data
```

Run MySQL:

```
docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=admin123 \
  -e MYSQL_DATABASE=company \
  -v mysql-data:/var/lib/mysql \
  -p 3306:3306 \
  mysql:8
```

Now explain:

- Container = Running database service.
- Volume = Persistent data storage.
- Deleting the container does not delete the named volume.

[How To Run MySQL in a Docker Container: A Step-by-Step Guide with Customization Tips](https://images.openai.com/static-rsc-4/O-O3xg3AWspmXUlBhixmSEbVgC2oQhcWq1CqGfF9_m5wRJJwoYxEgyPqmoyg8tIIfMdGnDx7NZWUjFzibX_p1qif2wc8US7PUMf0Qzr1akIBXaOsONcat3wXSj8EcGD5LhuR9PeX_EZ6taM6ui1U42owtT6JlDstt8eubHsmhNo?purpose=inline)

[mkabumattar.com](https://mkabumattar.com/blog/post/how-to-run-mysql-in-a-docker-container-a-step-by-step-guide-with-customization-tips/?utm_source=chatgpt.com)

Ask students to delete the container and recreate it using the same volume. Verify that the database remains intact.

## **Practical 4: Docker Networking**

**Real-world scenario:** Your company has a frontend and backend running in separate containers.

How will the frontend communicate with the backend?

Create a network:

```
docker network create app-network
```

Run backend:

```
docker run -d \
  --name backend \
  --network app-network \
  my-node-app:v1
```

Explain that containers connected to the same user-defined bridge network can communicate using container names.

For example:

```
http://backend:3000
```

This is an important concept for microservices architecture.

[Building a Multi-Tier Dockerized Application with MongoDB, Node.js, and React | by Olajide Salami | Medium](https://images.openai.com/static-rsc-4/YqIerMW21Nug2nVRvmRs6_fQ4li9k22BaCr-aIUZwD_t7Nst7at9sFcGDuvpHx7ZsFdg8fyZsJIjWbhKpz1t6Ws4fhsYDU9MLxLnRCNhj6lUWzAvpE80EmIrsuTAXebqHaRcJsE34lR5Wa6cqk7jwcx90k3Kd42ev-wjBYRsbbo?purpose=inline)

[medium.com](https://medium.com/%40olajidesolomon11/building-a-multi-tier-dockerized-application-with-mongodb-node-js-and-react-f261a12ae558?utm_source=chatgpt.com)

## **Practical 5: Docker Compose**

This should be one of the most important practicals in your training.

**Real-world scenario:** A company has three services:

- Node.js application.
- MySQL database.
- Redis cache.

Instead of starting each container separately, the company wants to manage the entire application using one configuration file.

Create `compose.yaml`:

```
services:

  app:
    image: my-node-app:v1
    ports:
      - "3000:3000"
    depends_on:
      - redis

  redis:
    image: redis:7-alpine
```

Start everything:

```
docker compose up -d
```

Check:

```
docker compose ps
```

Stop:

```
docker compose down
```

[Docker Compose - KodeKloud](https://images.openai.com/static-rsc-4/e7lsdDKXeNdUXGZYG5SygrXck7QZKdjAM6lRyM2xmPYHtYLxG-NxQ3rWUnhjzZs36sg434scKRzlghKpJkrPQMqsqMWWXRUmbazLZrDmUM70zgJEhnhIX41ffQ5PgOezyQzTT39bahoFDQkoWaldSsmubr3K4Fr_oZua9iujSuk?purpose=inline)

[notes.kodekloud.com](https://notes.kodekloud.com/docs/Docker-Certified-Associate-Exam-Course/Docker-Compose/Docker-Compose/page?utm_source=chatgpt.com)

Explain that Docker Compose is useful for managing multi-container applications, especially development and testing environments.

# **5. Final real-world project for students**

After teaching all the concepts, give them this project.

Final hands-on project

# **Deploy a complete e-commerce application using Docker**

[Building a Secure and Observable E-commerce Microservices Platform on AWS EKS - DEV Community](https://images.openai.com/static-rsc-4/HLR2kHURg6bfoOgebIeFV0Iq_qdt1MnREjv5VTIaGJQjLa3JqD2J2gu3K-F9VzQH6AaN3JwJTfGKcrC3jkaBCBRQDPTA58bGFkHDGz86zrPLGWplUiIv6Dm5pBlkDG6Px3Tbs3HRmJ-ESx114J9CNqCLwCu2FhsGpF8RiV23Jb8?purpose=inline)

[dev.to](https://dev.to/chris-amaechi/building-a-secure-and-observable-e-commerce-microservices-platform-on-aws-eks-2o18?utm_source=chatgpt.com)

**Architecture**

| Service       | Container |
| ------------- | --------- |
| Frontend      | React     |
| Backend       | Node.js   |
| Database      | MySQL     |
| Cache         | Redis     |
| Reverse Proxy | Nginx     |

**Requirements**

- Create Dockerfiles for frontend and backend.
- Run MySQL in a separate container.
- Connect backend with MySQL.
- Configure Docker networking.
- Configure persistent volumes.
- Use Docker Compose.
- Push custom images to Docker Hub.
- Deploy the application on an AWS EC2 instance.

**Expected outcome:** Every student should be able to deploy a multi-container application independently.

# **6. How I recommend conducting your classes**

Don't spend the entire class explaining theory. Follow this teaching ratio:

## **Recommended class structure**

# **30%**

**Theory and architecture**

# **50%**

**Live practical demonstration**

# **20%**

**Student assignments**

### **Suggested 8-class teaching plan**

| Class | Topic                          | Practical                   |
| ----- | ------------------------------ | --------------------------- |
| 1     | Docker fundamentals            | Run Nginx                   |
| 2     | Docker architecture & commands | Container lifecycle         |
| 3     | Dockerfile                     | Containerize Node.js        |
| 4     | Docker images & Docker Hub     | Push custom image           |
| 5     | Volumes                        | Persistent MySQL            |
| 6     | Networking                     | Connect containers          |
| 7     | Docker Compose                 | Multi-container application |
| 8     | Production deployment          | Deploy on AWS EC2           |

# **7. Important teaching tip: Show students where Docker is used in companies**

Connect Docker concepts to actual DevOps workflows.

[GitHub - khu-open-source/movie-server: KHU Open Source Movie Server 🎬 · GitHub](https://images.openai.com/static-rsc-4/I_PTM9VSW1cGdwpwO1PAhOuicWQzfJ04CCab-ZDKUWy_Z5BLKEIAxy-g5Yb7AE3Q6vB7lnAm3YmtdOzvc4R4jv-Zl7EyVdk00GrsDzaStb0Qcs2NlyN4qToc0CPZ7aU19I6gn3p-3QK-78hgQ7eI9ML62HCySXxwYRI44rB-JK0?purpose=inline)

[github.com](https://github.com/khu-open-source/movie-server?utm_source=chatgpt.com)

Explain this workflow:

1. Developer writes application code.
2. Developer pushes code to GitHub.
3. GitHub Actions builds a Docker image.
4. Image gets pushed to Docker Hub or Amazon ECR.
5. AWS EC2 pulls the image.
6. Docker runs the application container.
7. Users access the application.

This helps students understand why Docker is an essential DevOps skill.

# **My recommendation for your teaching/learning approach**

Docker as a story of a software company.

- First, show them the problem.
- Then introduce Docker as the solution.
- Build an application.
- Containerize it.
- Connect it to a database.
- Deploy it on a cloud server.
