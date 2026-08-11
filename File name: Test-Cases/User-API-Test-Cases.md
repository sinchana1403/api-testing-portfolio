# User API — Test Cases

**Application:** E-commerce Web Application  
**Module:** User Management API  
**Prepared By:** Sinchana  
**Date:** August 2026  
**Base URL:** https://api.ecommerce-test.com  
**Tool Used:** Postman

---

## API Endpoints Covered

| Method | Endpoint | Description |
|---|---|---|
| GET | /api/users | Get all users |
| GET | /api/users/{id} | Get specific user |
| POST | /api/users/register | Register new user |
| PUT | /api/users/{id} | Update entire user profile |
| PATCH | /api/users/{id} | Update specific user field |
| DELETE | /api/users/{id} | Delete user account |

---

## GET — Retrieve Users

---

### TC_API_001
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_001 |
| **Title** | Verify GET all users returns 200 and list of users |
| **Method** | GET |
| **URL** | /api/users |
| **Headers** | Content-Type: application/json |
| **Request Body** | None |
| **Expected Status Code** | 200 OK |
| **Expected Response** | JSON array of user objects each containing id, name, email, city fields |
| **Expected Response Time** | Under 2000ms |
| **Priority** | High |

---

### TC_API_002
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_002 |
| **Title** | Verify GET single user returns correct user details |
| **Method** | GET |
| **URL** | /api/users/1 |
| **Headers** | Content-Type: application/json |
| **Request Body** | None |
| **Expected Status Code** | 200 OK |
| **Expected Response** | Single user object with id: 1, correct name, email, and city |
| **Expected Response Time** | Under 2000ms |
| **Priority** | High |

---

### TC_API_003
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_003 |
| **Title** | Verify GET user with non-existent ID returns 404 |
| **Method** | GET |
| **URL** | /api/users/9999 |
| **Headers** | Content-Type: application/json |
| **Request Body** | None |
| **Expected Status Code** | 404 Not Found |
| **Expected Response** | {"error": "User not found"} |
| **Expected Response Time** | Under 2000ms |
| **Priority** | High |

---

### TC_API_004
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_004 |
| **Title** | Verify GET user with invalid ID format returns 400 |
| **Method** | GET |
| **URL** | /api/users/abc |
| **Headers** | Content-Type: application/json |
| **Request Body** | None |
| **Expected Status Code** | 400 Bad Request |
| **Expected Response** | {"error": "Invalid user ID format"} |
| **Priority** | Medium |

---

## POST — Register New User

---

### TC_API_005
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_005 |
| **Title** | Verify POST register returns 201 with valid details |
| **Method** | POST |
| **URL** | /api/users/register |
| **Headers** | Content-Type: application/json |
| **Request Body** | {"name": "Rahul Kumar", "email": "rahul@gmail.com", "password": "Rahul@123", "mobile": "9876543210"} |
| **Expected Status Code** | 201 Created |
| **Expected Response** | {"message": "User registered successfully", "userId": 101} |
| **Expected Response Time** | Under 3000ms |
| **Priority** | High |

---

### TC_API_006
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_006 |
| **Title** | Verify POST register returns 400 when email is missing |
| **Method** | POST |
| **URL** | /api/users/register |
| **Headers** | Content-Type: application/json |
| **Request Body** | {"name": "Rahul Kumar", "password": "Rahul@123", "mobile": "9876543210"} |
| **Expected Status Code** | 400 Bad Request |
| **Expected Response** | {"error": "Email is required"} |
| **Priority** | High |

---

### TC_API_007
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_007 |
| **Title** | Verify POST register returns 400 with invalid email format |
| **Method** | POST |
| **URL** | /api/users/register |
| **Headers** | Content-Type: application/json |
| **Request Body** | {"name": "Rahul Kumar", "email": "rahulgmail.com", "password": "Rahul@123", "mobile": "9876543210"} |
| **Expected Status Code** | 400 Bad Request |
| **Expected Response** | {"error": "Invalid email format"} |
| **Priority** | High |

---

### TC_API_008
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_008 |
| **Title** | Verify POST register returns 409 with duplicate email |
| **Method** | POST |
| **URL** | /api/users/register |
| **Headers** | Content-Type: application/json |
| **Request Body** | {"name": "Rahul Kumar", "email": "rahul@gmail.com", "password": "Rahul@123", "mobile": "9876543210"} |
| **Expected Status Code** | 409 Conflict |
| **Expected Response** | {"error": "Email already exists"} |
| **Priority** | High |

---

### TC_API_009 — BVA Applied
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_009 |
| **Title** | Verify POST register returns 400 with password below minimum length |
| **Method** | POST |
| **URL** | /api/users/register |
| **Headers** | Content-Type: application/json |
| **Request Body** | {"name": "Rahul Kumar", "email": "rahul@gmail.com", "password": "Rah1", "mobile": "9876543210"} |
| **Expected Status Code** | 400 Bad Request |
| **Expected Response** | {"error": "Password must be at least 8 characters"} |
| **Priority** | High |

---

### TC_API_010
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_010 |
| **Title** | Verify POST register returns 400 with empty request body |
| **Method** | POST |
| **URL** | /api/users/register |
| **Headers** | Content-Type: application/json |
| **Request Body** | {} |
| **Expected Status Code** | 400 Bad Request |
| **Expected Response** | {"error": "Request body cannot be empty"} |
| **Priority** | High |

---

## PUT — Update Entire User Profile

---

### TC_API_011
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_011 |
| **Title** | Verify PUT updates entire user profile successfully |
| **Method** | PUT |
| **URL** | /api/users/1 |
| **Headers** | Content-Type: application/json, Authorization: Bearer token |
| **Request Body** | {"name": "Rahul Kumar Updated", "email": "rahul.updated@gmail.com", "mobile": "9876543211", "city": "Mumbai"} |
| **Expected Status Code** | 200 OK |
| **Expected Response** | Updated user object with all new values |
| **Priority** | High |

---

### TC_API_012
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_012 |
| **Title** | Verify PUT without authorization token returns 401 |
| **Method** | PUT |
| **URL** | /api/users/1 |
| **Headers** | Content-Type: application/json |
| **Request Body** | {"name": "Rahul Kumar Updated"} |
| **Expected Status Code** | 401 Unauthorized |
| **Expected Response** | {"error": "Authentication required"} |
| **Priority** | High |

---

## PATCH — Update Specific Field

---

### TC_API_013
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_013 |
| **Title** | Verify PATCH updates only specified field without affecting others |
| **Method** | PATCH |
| **URL** | /api/users/1 |
| **Headers** | Content-Type: application/json, Authorization: Bearer token |
| **Request Body** | {"mobile": "9999999999"} |
| **Expected Status Code** | 200 OK |
| **Expected Response** | User object with updated mobile number. All other fields (name, email, city) remain unchanged. |
| **Priority** | High |

---

### TC_API_014
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_014 |
| **Title** | Verify PATCH by one user on another user's account returns 403 |
| **Method** | PATCH |
| **URL** | /api/users/2 |
| **Headers** | Content-Type: application/json, Authorization: Bearer token (user 1's token) |
| **Request Body** | {"mobile": "9999999999"} |
| **Expected Status Code** | 403 Forbidden |
| **Expected Response** | {"error": "You do not have permission to update this account"} |
| **Priority** | Critical |

---

## DELETE — Remove User

---

### TC_API_015
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_015 |
| **Title** | Verify DELETE removes user successfully |
| **Method** | DELETE |
| **URL** | /api/users/1 |
| **Headers** | Authorization: Bearer token |
| **Request Body** | None |
| **Expected Status Code** | 200 OK or 204 No Content |
| **Expected Response** | {"message": "User deleted successfully"} or empty body |
| **Priority** | High |

---

### TC_API_016
| Field | Details |
|---|---|
| **Test Case ID** | TC_API_016 |
| **Title** | Verify DELETE on non-existent user returns 404 |
| **Method** | DELETE |
| **URL** | /api/users/9999 |
| **Headers** | Authorization: Bearer token |
| **Request Body** | None |
| **Expected Status Code** | 404 Not Found |
| **Expected Response** | {"error": "User not found"} |
| **Priority** | Medium |

---

## API Response Validation Checklist

For every API test case verify:

- [ ] Status code matches expected value
- [ ] Response body contains all required fields
- [ ] Field values are correct and accurate
- [ ] Data types are correct (string, number, boolean)
- [ ] Response time is within acceptable limit (under 2000ms)
- [ ] Error messages are clear and specific
- [ ] No sensitive data exposed in response (passwords, tokens)
- [ ] Content-Type header in response is application/json

---

## Common API Bugs Found During Testing

| Bug | Status Code Seen | Expected Status Code |
|---|---|---|
| Duplicate email accepted | 201 | 409 Conflict |
| Missing field accepted | 201 | 400 Bad Request |
| Another user's data accessible | 200 | 403 Forbidden |
| Invalid ID format accepted | 200 | 400 Bad Request |
| Empty body accepted | 201 | 400 Bad Request |
| Deleted user still accessible | 200 | 404 Not Found |
