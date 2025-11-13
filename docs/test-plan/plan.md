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
- PWA offline behavior
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
Tools: **Playwright** or **Cypress**

E2E flows include:
- User registration → Login → Dashboard access

- Add cooklog → Confirm list update → View history

- Dish search interactions

- Recommendation flow

- Unauthorized access prevention

- PWA offline-access test

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

- Database rollback tests

---

## 5. Test Items

### Backend Endpoints

- `POST /auth/register`

- `POST /auth/login`

- `GET /dishes`

- `GET /dishes/search`

- `POST /cooklogs`

- `DELETE /cooklogs/{dish_id}`

- `GET /recommendations`

### Frontend Components

- Login / Register pages

- Dashboard

- Add Dish

- Cooklog history list

- Dish search UI

- Recommendations page

- Offline PWA screen

---

## 6. Test Environment

### Backend

- Python 3.11

- FastAPI app running locally or via Docker

- PostgreSQL test database

- Alembic migrations applied

### Frontend

- Node.js environment (Vite dev server)

- Browser: Chromium / Firefox / WebKit (for E2E)

- Service worker enabled for PWA testing

### Tools Summary

- pytest 

- HTTPX 

- SQLAlchemy test DB 

- Vitest 

- React Testing Library 

- Playwright


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

- Successful registration
- Duplicate registration blocked
- Login success / failure
- JWT expiration and invalid token handling

### Dishes

- Create dish
- Search dish
- Handle dish not found
- Duplicate dish prevention 

### Cooklogs

- Add new cooklog
- Retrieve cooklog list
- Soft delete and confirm hiding
- Unauthorized cooklog deletion blocked

### Recommendations

- Recommend dishes not cooked recently
- Recommendations adjust based on community logs
- No recommendations for empty history → fallback behavior

### Frontend

- User can log in / out
- Forms validate input
- Recommendations page loads correct data
- PWA offline fallback works
- UI handles API errors correctly

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
- 90%+ backend test coverage.
- No unauthorized data access possible.
- PWA works offline for main pages.
- Recommendation outputs validated against heuristic logic.

---

## 11. Conclusion

This test plan ensures Kya Saabzi meets functional and non-functional standards across the entire stack, providing confidence in quality and reliability before deployment.