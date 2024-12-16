# Task Manager API

A RESTful API built with NestJS, PostgreSQL, Prisma, and Docker for managing tasks.

## Project Description

This Task Manager API allows you to:
- Create, Read, Update, and Delete tasks
- Manage task status (PENDING, IN_PROGRESS, COMPLETED)
- Store task data in PostgreSQL database
- Run the entire application using Docker

## Technologies Used

- NestJS (Backend Framework)
- PostgreSQL (Database)
- Prisma (ORM)
- Docker & Docker Compose
- Node.js (>=18.18)

## Prerequisites

Before running this application, make sure you have:
- Docker and Docker Compose installed
- Node.js (version 18.18 or higher)
- npm (Node Package Manager)

## Installation & Setup

1. Clone the repository:
```bash
git clone <your-repository-url>
cd task-manager-api
```

2. Create `.env` file in the root directory:
```env
DATABASE_URL="postgresql://postgres:postgres@postgres:5432/taskdb?schema=public"
```

3. Start the application using Docker:
```bash
docker-compose up -d
```

The API will be available at `http://localhost:3300`

## API Endpoints

### Tasks
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /tasks | Create a new task |
| GET | /tasks | Get all tasks |
| GET | /tasks/:id | Get a specific task |
| PUT | /tasks/:id | Update a task |
| DELETE | /tasks/:id | Delete a task |

### Request Body Examples

Create/Update Task:
```json
{
  "title": "Complete Project",
  "description": "Finish the NestJS task manager",
  "status": "PENDING"
}
```

### Status Options
- `PENDING`
- `IN_PROGRESS`
- `COMPLETED`

## Testing the API

You can test the endpoints using curl:

```bash
# Create a task
curl -X POST http://localhost:3300/tasks \
-H "Content-Type: application/json" \
-d '{
  "title": "Test Task",
  "description": "Testing the API",
  "status": "PENDING"
}'

# Get all tasks
curl http://localhost:3300/tasks

# Get specific task (replace <id> with actual task id)
curl http://localhost:3300/tasks/<id>

# Update task
curl -X PUT http://localhost:3300/tasks/<id> \
-H "Content-Type: application/json" \
-d '{
  "status": "IN_PROGRESS"
}'

# Delete task
curl -X DELETE http://localhost:3300/tasks/<id>
```

## Development

If you want to run the application in development mode:

1. Install dependencies:
```bash
npm install
```

2. Generate Prisma client:
```bash
npx prisma generate
```

3. Run migrations:
```bash
npx prisma migrate dev
```

4. Start the development server:
```bash
npm run start:dev
```

## Docker Commands

```bash
# Start containers
docker-compose up -d

# Stop containers
docker-compose down

# View logs
docker-compose logs

# Rebuild containers
docker-compose up -d --build
```

## Database Management

- Access PostgreSQL database:
```bash
docker exec -it task-manager-api-postgres-1 psql -U postgres -d taskdb
```

- View Prisma Studio (database GUI):
```bash
npx prisma studio
```

## Project Structure
```
task-manager-api/
├── src/
│   ├── tasks/
│   │   ├── dto/
│   │   │   ├── create-task.dto.ts
│   │   │   └── update-task.dto.ts
│   │   ├── tasks.controller.ts
│   │   ├── tasks.module.ts
│   │   └── tasks.service.ts
│   ├── prisma/
│   │   └── prisma.service.ts
│   ├── app.module.ts
│   └── main.ts
├── prisma/
│   └── schema.prisma
├── docker-compose.yml
├── Dockerfile
└── README.md
```

## Error Handling

The API includes error handling for common scenarios:
- Invalid task ID
- Missing required fields
- Invalid status values
- Database connection issues

## License

[MIT](LICENSE)
