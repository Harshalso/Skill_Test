Microservices Containerization Task

This document provides a step-by-step guide for containerizing four Node.js microservices and orchestrating them using Docker and Docker Compose. Additionally, it covers deploying the application on an AWS EC2 instance.

## Objective

# Containerize the Node.js microservices: User Service, Product Service, Order Service, and Gateway Service.

- Set up Docker Compose to run the services together.

- Deploy the containerized services on an EC2 instance.

- Test and document the setup process.

# Prerequisites

- Node.js installed locally.

- Docker and Docker Compose installed.

# Step 1: Creating Dockerfiles

1.1 User Service Dockerfile

# Use the Node.js base image
FROM node:alpine

# Set the working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json .
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the service port
EXPOSE 3000

# Command to run the service
CMD ["npm", "start"]

1.2 Product Service Dockerfile

# Use the Node.js base image
FROM node:alpine

# Set the working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json .
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the service port
EXPOSE 3001

# Command to run the service
CMD ["npm", "start"]

1.3 Order Service Dockerfile

# Use the Node.js base image
FROM node:alpine

# Set the working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json .
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the service port
EXPOSE 3002

# Command to run the service
CMD ["npm", "start"]

1.4 Gateway Service Dockerfile

# Use the Node.js base image
FROM node:alpine

# Set the working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json .
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the service port
EXPOSE 3003

# Command to run the service
CMD ["npm", "start"]

## Step 2: Creating Docker Compose Configuration

- docker-compose.yml file to define the services and their configurations.

version: '3'
services:
  user-service:
    build: ./user-service
    ports:
      - "3000:3000"
    networks:
      - app-network

  product-service:
    build: ./product-service
    ports:
      - "3001:3001"
    networks:
      - app-network

  order-service:
    build: ./order-service
    ports:
      - "3002:3002"
    networks:
      - app-network

  gateway-service:
    build: ./gateway-service
    ports:
      - "3003:3003"
    networks:
      - app-network

networks:
  app-network:
    driver: bridge

# Step 3: Deploying on EC2 Instance

- Launch an EC2 Instance

# install Docker and Docker Compose on EC2

# Update package list
sudo apt update

# Install Docker
sudo apt install -y docker.io

# Install Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# Add current user to the Docker group
sudo usermod -aG docker $USER

# Transfer Files to EC2

scp -r ./microservices-containerization ec2-user@<EC2_IP>:/home/ec2-user/

# Running the Application

SSH into the EC2 instance.



# Run the following command to start the services:

sudo docker-compose up --build

3.5 Verify the Services

Access each service using the EC2 public IP and the respective ports:

User Service: http://<EC2_IP>:3000

Product Service: http://<EC2_IP>:3001

Order Service: http://<EC2_IP>:3002

Gateway Service: http://<EC2_IP>:3003



