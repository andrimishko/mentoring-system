# mentoring-system

REST API for a mentoring platform. Mentees find mentors, send requests, chat in real time and leave reviews.

## Features

- Registration, login, logout and password restore by email, with JWT authentication
- Mentor and mentee profiles with questionnaires, specializations, ranks and photos
- Mentoring requests: send, accept, reject and cancel
- Real-time chat over WebSocket (STOMP)
- User reviews
- Photo storage on AWS S3
- OpenAPI documentation with Swagger UI

## Tech stack

| Layer | Technology |
| --- | --- |
| Language | Java 17 |
| Framework | Spring Boot 3, Spring Security, Spring Data JPA |
| Database | PostgreSQL |
| Cache and token store | Redis |
| Real time | WebSocket, STOMP, SockJS |
| Storage | AWS S3 |
| Docs | springdoc OpenAPI |
| Build and deploy | Maven, Docker |

## Database

![Database diagram](database/db-diagram.png)

Table definitions are in [`database/tables`](database/tables).

## API overview

The full specification is in [`openapi.yaml`](src/main/resources/static/openapi.yaml). Swagger UI is served by the application.

| Area | Base path |
| --- | --- |
| Authentication | `/api/v1/auth` |
| Users, mentors, mentees | `/api/v1/users` |
| Questionnaires | `/api/v1/questionnaires` |
| Mentoring requests | `/api/v1/mentoring-requests` |
| Reviews | `/api/v1/reviews` |
| Chats | `/api/v1/chats` |
| Ranks and specializations | `/api/v1/ranks`, `/api/v1/specializations` |

## Running

Requires Java 17, a PostgreSQL database, Redis and an AWS S3 account.

Provide configuration through environment variables:

```
SPRING_DATASOURCE_URL=jdbc:postgresql://localhost:5432/mentoring_system
SPRING_DATASOURCE_USERNAME=...
SPRING_DATASOURCE_PASSWORD=...
SPRING_MAIL_USERNAME=...
SPRING_MAIL_PASSWORD=...
S3_ACCESS_KEY=...
S3_SECRET_KEY=...
JWT_SECRET=...
```

Redis connection settings are defined in `RedisConfig.java`.

Build and run:

```
./mvnw clean package
java -jar target/mentoring-system-0.0.1.jar
```

Or with Docker:

```
docker build -t mentoring-system .
docker run -p 8080:8080 --env-file .env mentoring-system
```

The API is available at http://localhost:8080.
