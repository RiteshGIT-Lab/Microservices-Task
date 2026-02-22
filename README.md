# Microservices-Task

## Overview
This document provides details on testing various services after running the `docker-compose` file. These services include User, Product, Order, and Gateway Services. Each service has its own endpoints for testing purposes.

---

## Services and Endpoints

### **User Service**
- **Base URL:** `http://localhost:3000`
- **Endpoints:**
  - **List Users:**  
    ```
    curl http://localhost:3000/users
    ```
    Or open in your browser: [http://localhost:3000/users](http://localhost:3000/users)

---

### **Product Service**
- **Base URL:** `http://localhost:3001`
- **Endpoints:**
  - **List Products:**  
    ```
    curl http://localhost:3001/products
    ```
    Or open in your browser: [http://localhost:3001/products](http://localhost:3001/products)

---

### **Order Service**
- **Base URL:** `http://localhost:3002`
- **Endpoints:**
  - **List Orders:**  
    ```
    curl http://localhost:3002/orders
    ```
    Or open in your browser: [http://localhost:3002/orders](http://localhost:3002/orders)

---

### **Gateway Service**
- **Base URL:** `http://localhost:3003/api`
- **Endpoints:**
  - **Users:**  
    ```
    curl http://localhost:3003/api/users
    ```
  - **Products:**  
    ```
    curl http://localhost:3003/api/products
    ```
  - **Orders:**  
    ```
    curl http://localhost:3003/api/orders
    ```

---

## Foke Git Repo snapshot 

![Forkrepo snapshot](https://github.com/user-attachments/assets/17c892ff-72a9-42c8-b64e-615fdf18b731)


## Instructions
1. Start all services using the `docker-compose` file:
   ```
   docker-compose up
   ```
2. Once the services are running, use the above endpoints to verify the functionality.

Happy testing!


## Folder Structure

Microservices-Task/
├── Microservices/
│   ├── user-service/
│   │   └── Dockerfile
│   ├── product-service/
│   │   └── Dockerfile
│   ├── order-service/
│   │   └── Dockerfile
│   ├── gateway-service/
│   │   └── Dockerfile
│   └── docker-compose.yml
└── README.md
## ## Services Used in This Project
User Service | 3000 | Provides user data |
| Product Service | 3001 | Provides product data |
| Order Service | 3002 | Provides order data |
| Gateway Service | 3003 | Routes requests to backend services |

## Step 1: Understanding the Code Structure

- Each service is a separate Node.js application
- Each service contains:
  - `package.json`
  - An entry file such as `app.js`
- Ports are predefined in the application code

- ## Step 2: Create Dockerfiles

For each service (user, product, order, gateway), a Dockerfile was written that:

Uses Node.js base image

Sets working directory

Installs dependencies

Copies code

Exposes correct port

Runs the service entry file (app.js)
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
## Step 3: Build Local Docker Images

Local Docker images were built for each service using:
docker build -t user-service .
docker build -t product-service .
docker build -t order-service .
docker build -t gateway-service .

## Step 4: Docker Compose

Docker Compose was used to run all services together on the same Docker network so they can communicate.

docker-compose.yml includes all services:

version: "3.8"

services:
  user-service:
    image: user-service
    ports:
      - "3000:3000"

  product-service:
    image: product-service
    ports:
      - "3001:3001"

  order-service:
    image: order-service
    ports:
      - "3002:3002"

  gateway-service:
    image: gateway-service
    ports:
      - "3003:3003"
    depends_on:
      - user-service
      - product-service
      - order-service
      
## Testing Endpoints

Direct Services

User Service: http://localhost:3000/users

Product Service: http://localhost:3001/products

Order Service: http://localhost:3002/orders

![localhost-3000](https://github.com/user-attachments/assets/96ee1a2e-4a0a-4d29-a37f-b2cb9fba9b4d)
![localhost-3001](https://github.com/user-attachments/assets/574a1119-7eef-4881-88ec-491f77a5cf03)
![localhost-3002](https://github.com/user-attachments/assets/41e33409-5689-46df-a880-615d3c07c2cd)

## Gateway APIs

http://localhost:3003/api/users
http://localhost:3003/api/products
http://localhost:3003/api/orders

![Docker build snapshot](https://github.com/user-attachments/assets/73399569-5bf5-4ebc-9081-43c36e6f795d)
![microservices dir snapshot](https://github.com/user-attachments/assets/80852cea-9dc1-497c-a0fa-9887b378ae58)
![docker compose](https://github.com/user-attachments/assets/f2cd46b5-35ac-4d2d-a35b-73f15d7dfe45)
![product services runing snapshot](https://github.com/user-attachments/assets/45a6d6ce-df02-4fd3-93e6-1ee8c3ef8853)
![docker image configuration snapshot](https://github.com/user-attachments/assets/8a18d39c-e679-47e0-bf1e-3c096be936ec)
![Final project snapshot](https://github.com/user-attachments/assets/a2bc5186-ea39-4617-acf9-466c77c39639)


## Remarks

This solution successfully shows:
✔ Dockerfiles for each service
✔ Local Docker images built
✔ Docker Compose orchestration
✔ Gateway communicating with backend services

## This project demonstrates a complete microservices containerization and orchestration workflow using Docker and Docker Compose.




      

  

