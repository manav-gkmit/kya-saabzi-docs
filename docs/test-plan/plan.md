# Kya Saabzi — Test Plan

---

## 1. Introduction
This document defines the testing strategy, scope, objectives, resources, and processes for the **Kya Saabzi** web application. The goal is to ensure reliability, correctness, security, and usability across both backend (FastAPI) and frontend (React PWA) components.

---

## 2. Project Overview
Kya Saabzi is a lightweight dish recommendation app that lets users log dishes they've cooked and receive heuristic-based recommendations. 
Tech stack includes:  
- **Backend:** FastAPI, SQLAlchemy, PostgreSQL, Alembic, JWT Auth, pytest  
- **Frontend:** React 18, Vite, Tailwind, Axios, PWA with service workers 

---

## 3. Scope of Testing
### In Scope
- Backend API logic and validation
- Authentication and JWT handling
- Authorization and access control
- CRUD operations for dishes and cooklogs
- Recommendation logic (recency + community popularity)
- Frontend UI/UX interactions
- API–Frontend integration
- Docker build and environment consistency
### Out of Scope
- Performance benchmarking beyond functional validation
- UI design polish unrelated to functionality

---

## 4. Testing Approach
### 4.1 Backend Tests
Tools: **pytest**, **pytest-asyncio**, **HTTPX**, **Postman**  

Types of testing:  

- **Unit tests** for:  
    - Pydantic schemas

    - Utility functions  

    - Database models and helpers  

- **Integration tests** for:  
    - User registration and login  
    - Dish CRUD  
    - Cooklog CRUD + soft deletes  
    - Recommendation endpoint behavior 

- **API contract tests** to ensure response shapes and codes remain stable

---

### 4.2 Frontend Tests
Tools: **Vitest**, **React Testing Library**, **Playwright**

- Component rendering tests
- Form validation tests
- API interaction tests
- Page routing tests
- State management tests
- PWA behavior tests

---

### 4.3 End-to-End (E2E) Tests

E2E flows include:
- User registration → Login → Dashboard access

- Add cooklog → Confirm list update → View history

- Dish search interactions

- Recommendation flow

- Unauthorized access prevention

---

### 4.4 Non-Functional Testing

#### Performance

- API response latency < 200 ms for core routes

- Database queries optimized with proper indexing

#### Security

- JWT validation

- Token expiration handling

- Prevent access to other users' cooklogs 

- SQL injection safety 

- CORS validation

#### Reliability

- Soft deletes behave as expected


---

### 4.5 Test Folder Structure
Tests will be organized mirroring the application's source code structure.

- **Backend Tests:**
    - `backend/tests/test_util`: For unit tests of individual utility functions.
    - `backend/tests/routers/`: For API contract tests.

- **Frontend Tests:**
    - `frontend/src/__tests__/unit/`: For component rendering, utility functions, and state management unit tests.
    - `frontend/src/__tests__/e2e/`: For end-to-end tests using Playwright/Cypress.

---

## 5. Test Items

### Backend Endpoints

- `POST /auth/register`

- `POST /auth/login`

- `GET /cooklogs`

- `GET /recommend/`

- `POST /dishes`

- `DELETE /cooklogs/{cooklog_id}`

- `GET /health`

### Frontend Components

- Login / Register pages

- Dashboard

- Add Dish page

- Cooklog history list

- Recommendations page

---

## 6. Test Environment

### Backend

- Python 3.11

- FastAPI app running locally or via Docker

- PostgreSQL test database

- Alembic migrations applied

### Frontend

- Node.js (v20.x) environment (Vite dev server)

- React (v18.x)

- Browser: Chromium / Firefox / WebKit (for E2E)

- Service worker enabled for PWA testing

### Tools Summary

- pytest 

- HTTPX 

- SQLAlchemy test DB 

- Vitest 

- React Testing Library 

- Postman


---

## 7. Test Data

### Example Users

- `user1@example.com`

- `user2@example.com`

### Example Dishes

- "Palak Paneer"

- "Aloo Gobi"

- "Dal Tadka"

### Cooklogs

- Logs with varying timestamps to test recency-based recommendations.

---

## 8. Test Cases Overview

### Authentication

- **Successful registration:**
    - **Acceptance Criteria:** A new user account is created, and a valid JWT is returned.
    - **Negative Scenario:** Attempting to register with an existing email or invalid credentials should return an appropriate error (e.g., 409 Conflict, 400 Bad Request) and not create a user.

- **Login success / failure:**
    - **Acceptance Criteria:** Valid credentials return a JWT; invalid credentials return a 401 Unauthorized error.
    - **Negative Scenario:** Login with incorrect password or non-existent user should fail with 401.

- **JWT expiration and invalid token handling:**
    - **Acceptance Criteria:** Expired or invalid tokens result in 401 Unauthorized responses for protected routes.
    - **Negative Scenario:** Accessing protected routes with an expired/invalid token should be denied.

### Dishes

- **Create dish:**
    - **Acceptance Criteria:** A new dish is successfully added to the database.
    - **Negative Scenario:** Attempting to create a dish with invalid data (e.g., missing name) should return a 422 Unprocessable Content.

### Cooklogs

- **Add new cooklog:**
    - **Acceptance Criteria:** A new cooklog entry is created for the authenticated user.
    - **Negative Scenario:** Adding a cooklog for a non-existent dish or without authentication should fail.

- **Retrieve cooklog list:**
    - **Acceptance Criteria:** The authenticated user's cooklogs are returned, ordered by recency.
    - **Negative Scenario:** Unauthorized access to another user's cooklogs should be blocked (403 Forbidden).

- **Soft delete and confirm hiding:**
    - **Acceptance Criteria:** A cooklog is marked as deleted and no longer appears in retrieval queries for the user, but remains in the database.
    - **Negative Scenario:** Attempting to delete a non-existent cooklog should return 404 Not Found.

- **Unauthorized cooklog deletion blocked:**
    - **Acceptance Criteria:** A user cannot delete another user's cooklog (403 Forbidden).

### Recommendations

- **Recommend dishes not cooked recently:**
    - **Acceptance Criteria:** The system suggests dishes that the user has not cooked recently, based on defined heuristics.
    - **Negative Scenario:** Recommendations should not include dishes cooked very recently.

- **Recommendations adjust based on community logs:**
    - **Acceptance Criteria:** Recommendations incorporate popularity from other users' cooklogs.

- **No recommendations for empty history → fallback behavior:**
    - **Acceptance Criteria:** If a user has no cooklogs, a default set of popular dishes is recommended.

### Frontend

- **User can log in / out:**
    - **Acceptance Criteria:** Users can successfully navigate through login and logout flows, and their authentication status is correctly reflected in the UI.
    - **Negative Scenario:** Invalid login credentials display an error message without logging in.

- **Forms validate input:**
    - **Acceptance Criteria:** All forms (e.g., registration, add dish) provide real-time validation feedback and prevent submission of invalid data.
    - **Negative Scenario:** Submitting a form with invalid data should show validation errors and prevent API calls.

- **Recommendations page loads correct data:**
    - **Acceptance Criteria:** The recommendations page displays a list of dishes based on the backend's recommendation logic.
  
- **UI handles API errors correctly:**
    - **Acceptance Criteria:** The UI displays user-friendly error messages for various API failure scenarios (e.g., network error, 401, 500).
    - **Negative Scenario:** API errors should not crash the application; appropriate error states should be displayed.

---

## 9. Risks & Mitigations
| Risk | Impact | Mitigation |
|------|--------|------------|
| Incorrect recommendation results | High | Add heuristic-focused tests |
| Token misuse or leakage | High | Strict JWT validation tests |
| Soft deletes cause inconsistent results | Medium | Add soft-delete integration tests |

---

## 10. Acceptance Criteria

- All critical user flows pass E2E tests.
- Backend unit test coverage: >90%
- Frontend unit/component test coverage: >80%
- No unauthorized data access possible.
- Recommendation outputs validated against heuristic logic.

---

## 11. CI Integration Steps
Continuous Integration (CI) will be used to automate testing and ensure code quality with every push to the repository.

- **Automated Test Execution:**
    - Unit and API contract tests (backend) will run on every push to `dev` and `main` branches.
    - Unit and component tests (frontend) will run on every push to `dev` and `main` branches.

- **Code Quality Checks:**
    - Linting (ESLint for frontend, Flake8/Black for backend) will be enforced.
    - Type checking (TypeScript for frontend, MyPy for backend) will be performed.

---

## 12. Conclusion

This test plan ensures Kya Saabzi meets functional and non-functional standards across the entire stack, providing confidence in quality and reliability before deployment.