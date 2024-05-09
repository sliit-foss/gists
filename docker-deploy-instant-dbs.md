# Running database Servers Instantly with Docker Compose

Running multiple database containers with Docker Compose allows you to easily deploy and manage various databases for development, testing, or production environments. Below are the prerequisites, setup steps, and usage instructions.

## Prerequisites

1. **Docker and Docker Compose**: Ensure Docker and Docker Compose are installed on your system. You can download and install Docker Desktop, which includes Docker Compose, from the [official Docker website](https://www.docker.com/products/docker-desktop).

## Setup

1. **Create a Docker Compose File**

   Save the following configuration in a file named `docker-compose.yml`

   ```yaml
   version: '3.8'

   services:
     # MySQL Database
     mysql:
       image: mysql:latest
       restart: always
       environment:
         MYSQL_ROOT_PASSWORD: mysecretpassword
       ports:
         - "3306:3306"
       
     # PostgreSQL Database
     postgres:
       image: postgres:latest
       restart: always
       environment:
         POSTGRES_PASSWORD: mysecretpassword
       ports:
         - "5432:5432"
       
     # MongoDB Database
     mongodb:
       image: mongo:latest
       restart: always
       ports:
         - "27017:27017"
       
     # Redis Database
     redis:
       image: redis:latest
       restart: always
       ports:
         - "6379:6379"
       
     # Couchbase Database
     couchbase:
       image: couchbase:latest
       restart: always
       environment:
         - COUCHBASE_ADMINISTRATOR_USERNAME=admin
         - COUCHBASE_ADMINISTRATOR_PASSWORD=password
       ports:
         - "8091-8096:8091-8096"
         - "11210:11210"
   ```

2. **Adjust Settings (Optional)**

   - Modify environment variables and ports as needed for each database service.

## Usage

1. **Start Containers**

   Run the following command in the directory containing the `docker-compose.yml` file
   ```bash
   docker-compose up -d { mysql | postgres | mongodb | redis | couchbase }
   ```


2. **Access Databases**

   - Connect to the databases using their default connection parameters (e.g., `localhost:3306` for MySQL, `localhost:5432` for PostgreSQL, etc.).
   - Use database management tools or command-line clients to interact with the databases.

3. **Stop Containers (Optional)**

   To stop and remove the containers, run:

   ```bash
   docker-compose down
   ```

---
---
