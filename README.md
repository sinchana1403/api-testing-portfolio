# API Testing Portfolio — Sinchana

**Prepared By:** Sinchana  
**Date:** August 2026  
**Tools Used:** Postman, JSONPlaceholder API  
**Purpose:** API test cases and testing scenarios
demonstrating REST API testing skills

---

## About This Repository

This repository contains API test cases, testing
scenarios, and Postman collection documentation
written from a QA Engineer's perspective.

---

## Repository Structure
api-testing-portfolio/
├── Test-Cases/
│ ├── User-API-Test-Cases.md
│ └── Payment-API-Test-Cases.md
└── Postman-Collections/
└── How-To-Import.md
---

## API Testing Concepts Covered

- HTTP Methods — GET, POST, PUT, PATCH, DELETE
- Status Codes — 2xx, 4xx, 5xx
- Request Headers and Authorization
- Request Body — JSON format
- Response Validation
- Positive and Negative Test Scenarios
- Boundary and Error Guessing scenarios

---

## HTTP Methods Reference

| Method | Purpose | Expected Status |
|---|---|---|
| GET | Retrieve data | 200 OK |
| POST | Create new resource | 201 Created |
| PUT | Update entire resource | 200 OK |
| PATCH | Update partial resource | 200 OK |
| DELETE | Remove resource | 200 / 204 |

---

## Status Codes Reference

| Code | Meaning | When You See It |
|---|---|---|
| 200 | OK | Successful GET, PUT, PATCH, DELETE |
| 201 | Created | Successful POST |
| 204 | No Content | Successful DELETE with no body |
| 400 | Bad Request | Invalid request format or data |
| 401 | Unauthorized | Missing or invalid token |
| 403 | Forbidden | Valid token but no permission |
| 404 | Not Found | Resource does not exist |
| 409 | Conflict | Resource already exists |
| 422 | Unprocessable Entity | Valid format but invalid data |
| 500 | Internal Server Error | Server side crash |





