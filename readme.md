

# Notes Application

A full-stack Dockerized Notes application built using Node.js, Express, PostgreSQL, Nginx, and Docker Compose. The application allows users to create, view, and delete notes, with persistent database storage and a reverse proxy configuration.

---

## Project Structure
```yaml
.
├── FrontEnd/
│   ├── index.html
│   ├── app.conf
│
├── Backend/
│   ├── server.js
│   ├── package.json
│   ├── init.sql
│   ├── Dockerfile
│
├── docker-compose.yml
└── README.md
```
---

## Features

- Create notes
- View all notes
- Delete notes
- REST API
- PostgreSQL persistent storage
- Rate limiting middleware
- Reverse proxy using Nginx
- Fully containerized environment

---

## Technologies Used

- Node.js
- Express.js
- PostgreSQL
- Nginx
- Docker
- Docker Compose

---

## Running the Application

### Build and Start

`` docker compose up --build ``

### Access the Application

Open in browser:

`` http://localhost ``

---

## Services Overview

Frontend:
- Runs Nginx
- Serves static files
- Proxies API requests to backend
- Port: 80

Backend:
- Node.js + Express API
- Port: 3001
- Connects to PostgreSQL via service name `db`

Database:
- PostgreSQL 15
- User: app
- Password: secret
- Database: myapp
- Data stored in Docker named volume

---

## API Endpoints

Health Check  
``GET /api/health``

Get All Notes  
``GET /api/items``

Create Note  
POST ``/api/items``  
Body:
{
  "name": "Example Note"
}

Delete Note  
``DELETE /api/items/:id``

---

## Environment Variables

Backend uses:

``DATABASE_URL=postgresql://app:secret@db:5432/myapp``  
``PORT=3001``

---

## Database Access (Inside Container)
```yaml
docker exec -it notes-db psql -U app -d myapp

Useful commands:

\dt  
SELECT * FROM items;

---

## Stopping Containers

Stop containers:

docker compose down

Stop containers and remove volumes (this deletes database data):

docker compose down -v

---
```
## Architecture Notes

- Frontend communicates with backend through relative path `/api`
- Nginx proxies `/api` requests to the backend container
- Backend connects to PostgreSQL using Docker service name `db`
- PostgreSQL data is persisted using a named Docker volume
- All services communicate through Docker networks
