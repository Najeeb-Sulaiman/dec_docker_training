# Docker Practice Projects

This document contains hands-on Docker projects designed to help you practice containerization concepts. The projects involve packaging Python applications into Docker images, managing multi-container applications with Docker Compose, and deploying applications with dependencies like PostgreSQL. Each project includes step-by-step instructions and deliverables to reinforce practical learning. 🚀

---

# Docker Practice Project 1: Containerizing a Streamlit Application

## Project Overview
You have developed a Streamlit application with the following functionalities:
- A user interface to upload CSV files.
- Once a CSV file is uploaded, the application displays:
  - The first five rows of the dataset.
  - Summary statistics of numerical columns.

Your manager has tasked you with containerizing this application using Docker so it can be easily deployed in a production environment. Additionally, you need to publish the Docker image on **Docker Hub** to allow other team members to pull and run it on their machines.

---

## Task Instructions

### 1. Setup Project Environment
1. **Create a new project directory** on your local machine and navigate into it:
   ```sh
   mkdir docker_practice_project && cd docker_practice_project
   ```
2. **Clone this repository** into the project folder:
   ```sh
   git clone <repo_url>
   cd <repo_name>
   ```

---

### 2. Write a Dockerfile
Create a **Dockerfile** in the project directory to package the application into a Docker image. The Dockerfile should meet the following requirements:

✅ Use a **lightweight Python base image**.  
✅ Copy and install application dependencies from `requirements.txt`.  
✅ Copy the application code into the image.  
✅ Expose port **8501** to allow access to the Streamlit app.  
✅ Set the container's entrypoint to run the application using:
   ```sh
   streamlit run <path/filename.py>
   ```
✅ Follow **Docker build best practices** to leverage **Docker’s build cache** for efficient image creation.

---

### 3. Build and Run the Docker Image
1. **Build the Docker image**, naming it appropriately:
   
2. **Run a container** from the image, mapping port `8501` from the container to the host:
   
3. **Verify the application is running**:
   - Open your browser and navigate to:
     ```
     http://localhost:8501
     ```
   - Upload the **student.csv** file (available in the repository) to confirm that the application processes data as expected.

---

### 4. Publish the Image to Docker Hub
1. **Log in to Docker Hub** (if not already logged in):
   
2. **Tag the image** to match your Docker Hub repository:

3. **Push the image to Docker Hub**

---

## Deliverables
To complete the task, submit the following:
1. Your **Dockerfile**.
2. A link to your **Docker Hub repository** containing the published image.

Happy Dockerizing! 🚀

---
<br/>

<br/>

<br/>

<br/>

# Docker Practice Project 2: Creating a Multi-container Application

## Project Overview

You have developed a Streamlit application with the following functionalities:

- A user interface for CSV file upload.
- Once a CSV file is uploaded, the application loads it into a PostgreSQL database table for persistence.
- The application reads the loaded data from the PostgreSQL database table.
- The application displays the first 5 rows and the summary statistics of the numerical columns in the table.

The application is implemented in the `data_process_db.py` script in this repository.

Since this application requires a PostgreSQL database, you need to run a PostgreSQL container and connect to it from the container running your application. To achieve this, you will create a multi-container application using Docker Compose.

---

## Task

Your manager has tasked you with:

- Packaging this application and its dependencies into a Docker image for easy deployment.
- Pushing the application image to Docker Hub so team members can easily download and run it.
- Creating a multi-container setup using Docker Compose.

---

## Step-by-Step Instructions

1. **Set Up Your Project**

   - Create a new folder on your PC and navigate into it.
   - Clone this repository into the new folder.

---

2. **Create and Write a Dockerfile**

   - Package the application into a Docker image.
   - Use a lightweight Python image as the base image.
   - Copy and install the application dependencies (`requirements.txt`).
   - Copy the application code into the image.
   - Expose port `8501` for the application.
   - Set the container's entrypoint to run the application using:
     ```sh
     streamlit run <path/filename.py>
     ```
   - Ensure the Dockerfile follows best practices to leverage Docker build caching.

---

3. **Create Docker Compose Configuration**

   - Create a `compose.yml` file.
   - Define services to run the multi-container application:
     - **Application Service**
       - Uses the build key to refrence the Dockerfile you created.
       - Binds host port `8501` to container port `8501`.
       - Defines the following environment variables:
         ```yaml
         environment:
           POSTGRES_HOST: app-db
           POSTGRES_USER: postgres
           POSTGRES_PASSWORD: postgres
           POSTGRES_DB: postgres
           POSTGRES_PORT: 5432
         ```
       - Depends on the database service.
     - **Database Service**
       - Uses a lightweight PostgreSQL image.
       - Defines the following environment variable:
         ```yaml
         environment:
           POSTGRES_PASSWORD: postgres
         ```
       - Persists database data using Docker volumes.

---

4. **Run the Multi-Container Application**

   - Start your application using Docker Compose

---

5. **Access the Web Application**

   - Open your browser and navigate to [http://localhost:8501](http://localhost:8501).
   - Upload the `student.csv` file available in this repo.
   - Confirm the application works as expected.

---

6. **Verify Database Persistence**

   - Execute into your database container:
     ```sh
     docker exec -it <database_container_id> psql -U postgres
     ```
   - Run the following SQL command to confirm the uploaded data is present:
     ```sql
     SELECT * FROM student;
     ```

---

7. **Push Your Application Image to Docker Hub**

   - Tag and push your Docker image to Docker Hub

---

## Deliverables

- Submit your `Dockerfile` and `compose.yml` file.
- Provide a link to your Docker image on Docker Hub.

---

Happy Dockerizing! 🚀