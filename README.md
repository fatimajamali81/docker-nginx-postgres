# Multi-Container Docker Compose, nginx & postgres Project

This project demonstrates a multi-container application using Docker Compose, including a web application served by Nginx and a PostgreSQL database. The application, running in a Python Flask container, interacts with the PostgreSQL database. Nginx serves as a reverse proxy to the Flask application.

## Prerequisites

- Docker
- Docker Compose

## Setup

1. Clone the repository:
   ```sh
   git clone <repository_url>
   cd my_docker_compose_project
   ```
Build and run the containers:

```sh
docker-compose up --build
```
Access the web application at `http://localhost`.


## Purpose and Actions of Each File

### 1. `docker-compose.yml`

Defines the multi-container setup:

- **web**: 
  - Builds the application container from the `app` directory.
  - Sets the `DATABASE_URL` environment variable.
  - Maps port `5000` on the host to port `5000` in the container.

- **nginx**: 
  - Builds the Nginx container from the `nginx` directory.
  - Maps port `80` on the host to port `80` in the container.
  - Forwards requests to the `web` service on port `5000`.

- **db**: 
  - Builds the PostgreSQL container from the `postgres` directory.
  - Sets environment variables for PostgreSQL (`POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB`).
  - Maps port `5432` on the host to port `5432` in the container.

### 2. nginx/Dockerfile

Builds the Nginx image:

- Uses the official Nginx image.
- Copies the Nginx configuration file and static HTML files into the container.

### 3. nginx/default.conf

Configures Nginx to proxy requests to the Flask application:

- Forwards requests from port `80` to the `web` service on port `5000`.

### 4. nginx/html/index.html

A simple static HTML page served by Nginx:

- Displays a welcome message indicating that the application is connected to a PostgreSQL database.

### 5. app/Dockerfile

Builds the Flask application container:

- Uses the Python 3.9 slim image.
- Installs dependencies from `requirements.txt`.
- Runs the Flask application.

### 6. app/requirements.txt

Lists the Python packages needed for the application:

- `flask` for the web framework.
- `psycopg2-binary` for PostgreSQL database connectivity.

### 7. app/app.py

A simple Flask application:

- Connects to PostgreSQL using `psycopg2`.
- Exposes an endpoint that retrieves and returns data from the `users` table in PostgreSQL.

### 8. postgres/Dockerfile

Builds the PostgreSQL image:

- Uses the official PostgreSQL image.
- Copies the initialization SQL script into the container.

### 9. postgres/init.sql

Initial SQL script for PostgreSQL:

- Creates a `users` table.
- Inserts sample data into the table.


### Conclusion

This project provides a practical example of using Docker Compose to set up a multi-container application with Nginx, a Flask application, and PostgreSQL. It demonstrates how to configure and connect these components in a development environment.


### Summary

- **Nginx**: Serves as the reverse proxy for the Flask application.
- **Flask App**: Connects to the PostgreSQL database and provides an endpoint to retrieve data.
- **PostgreSQL**: Stores data and is initialized with a sample dataset.

### License
This project is licensed under the MIT License.
