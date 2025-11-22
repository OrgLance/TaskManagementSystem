# Task Management System

## Business Requirements

Create a backend system for managing tasks and projects with the following features:

### 1. User Management
- Users can register and authenticate
- Support for two roles: `USER` and `ADMIN`
- Users belong to one or more teams

### 2. Project Management
- Projects have a name, description, start date, and end date
- Projects are assigned to teams
- Only team members can view project tasks

### 3. Task Management
- Tasks belong to projects
- Each task has: title, description, priority (LOW, MEDIUM, HIGH), status (TODO, IN_PROGRESS, DONE), assignee, due date
- Tasks can have comments
- Track task status change history

### 4. Business Rules
- Users can only view/modify tasks in projects their team is assigned to
- Admins can view all projects and tasks
- Tasks cannot be assigned to users not in the project's team
- Email notification should be sent when a task is assigned (implement interface, actual sending not required)

---

## Technical Requirements

### Mandatory Technology Stack
- **Java 17 or higher**
- **Spring Boot 3.x**
- **Spring Data JPA**
- **Spring Security** (JWT-based authentication)
- **Database:** H2 (embedded) or PostgreSQL
- **Build Tool:** Maven or Gradle

### Expected Implementation

#### 1. REST API Endpoints

Implement the following endpoints:

**Authentication:**
```
POST /api/auth/register - Register new user
POST /api/auth/login - Login and receive JWT token
```

**Projects:**
```
GET    /api/projects - List all projects (filtered by user's teams)
POST   /api/projects - Create new project (ADMIN only)
GET    /api/projects/{id} - Get project details
PUT    /api/projects/{id} - Update project
DELETE /api/projects/{id} - Delete project (ADMIN only)
```

**Tasks:**
```
GET    /api/projects/{projectId}/tasks - List all tasks in a project
POST   /api/projects/{projectId}/tasks - Create new task
GET    /api/tasks/{id} - Get task details
PUT    /api/tasks/{id} - Update task
DELETE /api/tasks/{id} - Delete task
PATCH  /api/tasks/{id}/status - Update task status
POST   /api/tasks/{id}/comments - Add comment to task
GET    /api/tasks/{id}/history - Get task status change history
```

**Teams:**
```
GET    /api/teams - List all teams
POST   /api/teams - Create team (ADMIN only)
POST   /api/teams/{id}/members - Add member to team (ADMIN only)
```

#### 2. Database Design
- Design normalized database schema
- Use appropriate relationships (OneToMany, ManyToMany, etc.)
- Implement soft delete for tasks (deleted flag)
- Create proper indexes for performance

#### 3. Security
- Implement JWT-based authentication
- Use method-level security annotations where appropriate
- Password encryption using BCrypt
- Implement authorization checks based on team membership

#### 4. Exception Handling
- Global exception handler using @ControllerAdvice
- Custom exceptions for business logic violations
- Proper HTTP status codes
- Consistent error response format

#### 5. Validation
- Input validation using Bean Validation (javax.validation)
- Custom validators where needed
- Meaningful error messages

#### 6. Testing
- Unit tests for service layer (minimum 70% coverage)
- Integration tests for at least 2 REST endpoints
- Use JUnit 5 and Mockito

#### 7. Documentation
- Swagger/OpenAPI documentation
- README with setup instructions
- Brief architecture overview


---

## Bonus Points (Optional)

Implement any of the following for additional credit:

1. **Caching:** Implement Redis/Caffeine cache for frequently accessed data
2. **Search:** Full-text search for tasks using specifications or Querydsl
3. **Pagination & Sorting:** Implement for list endpoints
4. **Audit Trail:** Track who created/modified entities and when
5. **Docker:** Provide Dockerfile and docker-compose.yml
6. **Async Processing:** Use @Async for notification sending
7. **Rate Limiting:** Implement API rate limiting
8. **Soft Delete:** Implement soft delete pattern properly
9. **Custom Queries:** Use native queries or JPQL for complex scenarios
10. **Performance:** Solve N+1 query problems using entity graphs or fetch joins

---

## Deliverables

### Required
1. **Source Code:** Complete Spring Boot project
2. **README.md:** Setup instructions, how to run, credentials
3. **Database Schema:** ER diagram or SQL script
4. **Postman Collection:** Or any API testing collection
5. **Test Results:** Screenshot showing test execution results

### Submission Format
- GitHub repository (preferred) or ZIP file
- Include `.gitignore` (exclude IDE files, target/, etc.)
- Include sample data script if possible


---

## Questions?

If you have questions about requirements, make reasonable assumptions and document them in your README. We want to see your decision-making process.

---

## Good Luck!

We're excited to see your implementation. Focus on writing production-quality code that you'd be proud to show in a code review. Quality over quantity - a well-implemented subset is better than a poorly implemented complete solution.
