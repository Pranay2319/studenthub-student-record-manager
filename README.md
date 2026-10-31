# StudentHub - Student Record Manager

A MERN stack web application to add, view, update, delete and search student records.

## Description
StudentHub stores student details (name, roll number, course, email, phone, marks) in MongoDB.
The React frontend shows records in a table with search, and the Express/Mongoose backend exposes a
REST API with validation and duplicate-roll-number protection.

## Technologies Used
- React (Vite) with `useState()` and `useEffect()`
- Node.js and Express.js
- MongoDB and Mongoose
- Axios
- Visual Studio Code, Git and GitHub

## Features
- Add, view, update and delete student records (full CRUD)
- Search by name, roll number, course, email or phone
- Frontend and backend validation (required fields, no spaces-only text, email format, 10-digit phone, marks 0-100)
- Duplicate roll numbers rejected with a clear message (HTTP 409)
- Confirmation dialog before deleting
- Success and error messages for every action

## Project Structure
```
studenthub/
  backend/    Express API, Mongoose model, routes, error handler
  frontend/   React app (Vite)
```

## How to Run

### Prerequisites
Node.js 18+, and MongoDB running locally (or a MongoDB Atlas connection string).

### 1. Backend
```bash
cd backend
npm install
cp .env.example .env      # Windows: copy .env.example .env
npm run seed              # optional: load sample students
npm run dev               # starts on http://localhost:5000
```

### 2. Frontend
```bash
cd frontend
npm install
npm run dev               # opens on http://localhost:5173
```
The Vite dev server proxies `/api` to `http://localhost:5000`, so no extra setup is needed.

## API Endpoints
| Method | URL | Purpose |
|--------|-----|---------|
| GET | `/api/students?search=term` | List / search students |
| GET | `/api/students/:id` | Get one student |
| POST | `/api/students` | Add a student |
| PUT | `/api/students/:id` | Update a student |
| DELETE | `/api/students/:id` | Delete a student |

Sample POST body:
```json
{
  "name": "Ritesh Chaubey",
  "rollNo": "T005",
  "course": "B.Sc.IT",
  "email": "ritesh@example.com",
  "phone": "9876543210",
  "marks": 82
}
```

## Validation Rules
| Field | Rule |
|-------|------|
| name | Required, 2-60 chars, letters/spaces/. ' - only, spaces-only rejected |
| rollNo | Required, unique, 3-15 chars (letters, digits, hyphen), stored in UPPERCASE |
| course | Required, one of B.Sc.IT, B.Sc.CS, B.Com, BMS, BAF, BA |
| email | Required, valid format, stored in lowercase |
| phone | Required, 10 digits starting with 6-9 |
| marks | Required, number between 0 and 100 |

## Testing Checklist
1. Add valid student -> appears in table and in MongoDB Compass
2. Edit a student -> changes saved
3. Delete -> confirmation shown, record removed
4. Search "T00" or "B.Sc.IT" -> table filters
5. Submit empty form -> field error messages shown
6. Enter marks 150 or phone 12345 -> validation errors
7. Add roll number T005 twice -> "already exists" error
8. Test GET, POST, PUT, DELETE in Postman
9. Stop the backend -> frontend shows an error message

## Author
Ritesh Chaubey, T005, TYIT
