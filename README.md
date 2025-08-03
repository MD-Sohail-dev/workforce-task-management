# Workforce Management - Backend Engineer Assignment ✅

This is a Spring Boot application developed as part of the Backend Engineer take-home assignment.

---

## 💻 How to Run

1. Ensure you have **Java 17** and **Gradle** installed.
2. Open this project in your IDE (IntelliJ / VS Code).
3. Run the main class:
   ```
   com.railse.hiring.workforcemgmt.WorkforcemgmtApplication
   ```
4. The application runs at:
   ```
   http://localhost:8080
   ```

---

## 📦 Project Structure

```
src/main/java/com/railse/hiring/workforcemgmt/
├── WorkforcemgmtApplication.java
├── common/
│   ├── exception/
│   │   ├── CustomExceptionHandler.java
│   │   ├── ResourceNotFoundException.java
│   │   └── StatusCode.java
│   └── model/
│       ├── enums/
│       │   └── ReferenceType.java
│       └── response/
│           ├── Pagination.java
│           ├── Response.java
│           └── ResponseStatus.java
├── controller/
│   └── TaskManagementController.java
├── dto/
│   ├── AssignByReferenceRequest.java
│   ├── TaskCreateRequest.java
│   ├── TaskFetchByDateRequest.java
│   ├── TaskManagementDto.java
│   └── UpdateTaskRequest.java
├── mapper/
│   └── ITaskManagementMapper.java
├── model/
│   ├── TaskManagement.java
│   ├── Comment.java
│   ├── ActivityLog.java
│   └── enums/
│       ├── Priority.java
│       ├── Task.java
│       └── TaskStatus.java
├── repository/
│   ├── InMemoryTaskRepository.java
│   └── TaskRepository.java
├── service/
│   ├── TaskManagementService.java
│   └── impl/
│       └── TaskManagementServiceImpl.java
```

---

## 🚀 API Endpoints

### ✅ Get a single task
```bash
curl --location 'http://localhost:8080/task-mgmt/1'
```

### ✅ Create a new task
```bash
curl --location 'http://localhost:8080/task-mgmt/create' \
--header 'Content-Type: application/json' \
--data '{
   "requests": [
       {
           "reference_id": 105,
           "reference_type": "ORDER",
           "task": "CREATE_INVOICE",
           "assignee_id": 1,
           "priority": "HIGH",
           "task_deadline_time": 1728192000000
       }
   ]
}'
```

### ✅ Update a task's status
```bash
curl --location 'http://localhost:8080/task-mgmt/update' \
--header 'Content-Type: application/json' \
--data '{
   "requests": [
       {
           "task_id": 1,
           "task_status": "STARTED",
           "description": "Work has been started on this invoice."
       }
   ]
}'
```

---

### 🔁 Assign tasks by reference (Bug #1 Fixed)
```bash
curl --location 'http://localhost:8080/task-mgmt/assign-by-ref' \
--header 'Content-Type: application/json' \
--data '{
   "reference_id": 201,
   "reference_type": "ENTITY",
   "assignee_id": 5
}'
```
✔️ **Fix:** Old tasks are now marked as `CANCELLED` instead of being duplicated.

---

### 📅 Fetch tasks by date (Bug #2 Fixed)
```bash
curl --location 'http://localhost:8080/task-mgmt/fetch-by-date/v2' \
--header 'Content-Type: application/json' \
--data '{
   "start_date": 1672531200000,
   "end_date": 1735689599000,
   "assignee_ids": [1, 2]
}'
```
✔️ **Fix:** Only tasks that are not `CANCELLED` are returned.

---

## ✨ Features Implemented

### ✅ Bug Fixes
- **Bug #1:** Task reassignment now cancels the old task instead of duplicating it.
- **Bug #2:** Cancelled tasks are excluded from date-based fetches.

### ✅ Feature 1: Smart Daily Task View
- Shows:
    - Tasks that start within the date range
    - Tasks started before the range but still active (not completed)

### ✅ Feature 2: Task Priority

- **Change priority:**
```bash
curl --location --request PUT 'http://localhost:8080/task-mgmt/1/priority?priority=MEDIUM'
```

- **Fetch by priority:**
```bash
curl --location 'http://localhost:8080/task-mgmt/priority/HIGH'
```

### ✅ Feature 3: Comments & Activity History

- **Add comment:**
```bash
curl --location --request POST 'http://localhost:8080/task-mgmt/1/comment?author=John&message=Updated deadline due to delay.'
```

- **View task details with history:**
```bash
curl --location 'http://localhost:8080/task-mgmt/1'
```

Response includes:
- Task info
- All comments
- Auto-logged activity history (e.g., assignment, status change)

---

## 🧾 Reference Types

- `ENTITY`
- `ORDER`
- `ENQUIRY`

## 📌 Task Types

- `ASSIGN_CUSTOMER_TO_SALES_PERSON`
- `CREATE_INVOICE`
- `ARRANGE_PICKUP`
- `COLLECT_PAYMENT`

## 📌 Task Status

- `ASSIGNED`
- `STARTED`
- `COMPLETED`
- `CANCELLED`

## 📌 Priority Levels

- `HIGH`
- `MEDIUM`
- `LOW`

---

## 👤 Author

**MD Sohail Ansari**  
B.Tech Graduate, Electronics & Communication Engineering  
Asansol Engineering College  
📧 sohail9749037725@gmail.com  
🌐 GitHub: https://github.com/MD-Sohail-dev  
🔗 LinkedIn: https://www.linkedin.com/in/md-sohail-ansari-7a8778240/

---

## ✅ Done

- ✅ Project setup & structure
- ✅ Bug Fixes
- ✅ New Features
- ✅ Clean, testable code
- ✅ Final README documentation
