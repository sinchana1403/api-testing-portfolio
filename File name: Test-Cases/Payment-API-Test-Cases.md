# Payment API — Test Cases

**Application:** E-commerce Web Application  
**Module:** Payment API  
**Prepared By:** Sinchana  
**Date:** August 2026  
**Base URL:** https://api.ecommerce-test.com  
**Tool Used:** Postman

---

## API Endpoints Covered

| Method | Endpoint | Description |
|---|---|---|
| POST | /api/payments/initiate | Initiate a payment |
| GET | /api/payments/{id} | Get payment status |
| POST | /api/payments/verify | Verify payment completion |
| POST | /api/refunds | Initiate refund |
| GET | /api/refunds/{id} | Get refund status |

---

## POST — Initiate Payment

---

### TC_PAY_001
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_001 |
| **Title** | Verify POST initiate payment returns 201 with valid UPI details |
| **Method** | POST |
| **URL** | /api/payments/initiate |
| **Headers** | Content-Type: application/json, Authorization: Bearer token |
| **Request Body** | {"order_id": 101, "amount": 999, "payment_method": "UPI", "upi_id": "rahul@oksbi"} |
| **Expected Status Code** | 201 Created |
| **Expected Response** | {"payment_id": "PAY001", "status": "Initiated", "amount": 999} |
| **Expected Response Time** | Under 3000ms |
| **Priority** | High |

---

### TC_PAY_002
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_002 |
| **Title** | Verify POST payment returns 400 with invalid UPI ID format |
| **Method** | POST |
| **URL** | /api/payments/initiate |
| **Headers** | Content-Type: application/json, Authorization: Bearer token |
| **Request Body** | {"order_id": 101, "amount": 999, "payment_method": "UPI", "upi_id": "abc123"} |
| **Expected Status Code** | 400 Bad Request |
| **Expected Response** | {"error": "Invalid UPI ID format"} |
| **Priority** | High |

---

### TC_PAY_003
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_003 |
| **Title** | Verify POST payment returns 400 when amount is zero |
| **Method** | POST |
| **URL** | /api/payments/initiate |
| **Headers** | Content-Type: application/json, Authorization: Bearer token |
| **Request Body** | {"order_id": 101, "amount": 0, "payment_method": "UPI", "upi_id": "rahul@oksbi"} |
| **Expected Status Code** | 400 Bad Request |
| **Expected Response** | {"error": "Payment amount must be greater than zero"} |
| **Priority** | High |

---

### TC_PAY_004 — BVA Applied
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_004 |
| **Title** | Verify POST payment returns 400 when amount is negative |
| **Method** | POST |
| **URL** | /api/payments/initiate |
| **Headers** | Content-Type: application/json, Authorization: Bearer token |
| **Request Body** | {"order_id": 101, "amount": -100, "payment_method": "UPI", "upi_id": "rahul@oksbi"} |
| **Expected Status Code** | 400 Bad Request |
| **Expected Response** | {"error": "Payment amount must be greater than zero"} |
| **Priority** | High |

---

### TC_PAY_005
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_005 |
| **Title** | Verify POST payment returns 400 when order ID is missing |
| **Method** | POST |
| **URL** | /api/payments/initiate |
| **Headers** | Content-Type: application/json, Authorization: Bearer token |
| **Request Body** | {"amount": 999, "payment_method": "UPI", "upi_id": "rahul@oksbi"} |
| **Expected Status Code** | 400 Bad Request |
| **Expected Response** | {"error": "Order ID is required"} |
| **Priority** | High |

---

### TC_PAY_006
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_006 |
| **Title** | Verify POST payment returns 401 without authorization token |
| **Method** | POST |
| **URL** | /api/payments/initiate |
| **Headers** | Content-Type: application/json |
| **Request Body** | {"order_id": 101, "amount": 999, "payment_method": "UPI", "upi_id": "rahul@oksbi"} |
| **Expected Status Code** | 401 Unauthorized |
| **Expected Response** | {"error": "Authentication required"} |
| **Priority** | Critical |

---

### TC_PAY_007 — Error Guessing Applied
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_007 |
| **Title** | Verify duplicate payment request for same order returns 409 |
| **Method** | POST |
| **URL** | /api/payments/initiate |
| **Headers** | Content-Type: application/json, Authorization: Bearer token |
| **Request Body** | {"order_id": 101, "amount": 999, "payment_method": "UPI", "upi_id": "rahul@oksbi"} |
| **Expected Status Code** | 409 Conflict |
| **Expected Response** | {"error": "Payment already initiated for this order"} |
| **Priority** | Critical |
| **Note** | Send same request twice rapidly — second request should be rejected |

---

## GET — Payment Status

---

### TC_PAY_008
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_008 |
| **Title** | Verify GET payment status returns correct status after successful payment |
| **Method** | GET |
| **URL** | /api/payments/PAY001 |
| **Headers** | Authorization: Bearer token |
| **Request Body** | None |
| **Expected Status Code** | 200 OK |
| **Expected Response** | {"payment_id": "PAY001", "status": "Success", "amount": 999, "order_id": 101} |
| **Priority** | High |

---

### TC_PAY_009
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_009 |
| **Title** | Verify GET payment status returns 404 for non-existent payment ID |
| **Method** | GET |
| **URL** | /api/payments/INVALID123 |
| **Headers** | Authorization: Bearer token |
| **Request Body** | None |
| **Expected Status Code** | 404 Not Found |
| **Expected Response** | {"error": "Payment not found"} |
| **Priority** | Medium |

---

## POST — Verify Payment

---

### TC_PAY_010
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_010 |
| **Title** | Verify POST payment verification confirms successful transaction |
| **Method** | POST |
| **URL** | /api/payments/verify |
| **Headers** | Content-Type: application/json, Authorization: Bearer token |
| **Request Body** | {"payment_id": "PAY001", "order_id": 101} |
| **Expected Status Code** | 200 OK |
| **Expected Response** | {"verified": true, "order_status": "Confirmed", "amount_debited": 999} |
| **Priority** | Critical |

---

### TC_PAY_011 — Critical Bug Scenario
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_011 |
| **Title** | Verify payment showing Success but amount not debited returns correct error |
| **Method** | POST |
| **URL** | /api/payments/verify |
| **Headers** | Content-Type: application/json, Authorization: Bearer token |
| **Request Body** | {"payment_id": "PAY001", "order_id": 101} |
| **Expected Status Code** | 200 OK |
| **Expected Response** | verified: true AND amount_debited must equal order amount AND order_status must be Confirmed — all three must match simultaneously |
| **Priority** | Critical |
| **Note** | If UI shows Success but verification API returns amount_debited: 0 — Critical bug found |

---

## POST — Initiate Refund

---

### TC_PAY_012
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_012 |
| **Title** | Verify POST refund initiated successfully for cancelled order |
| **Method** | POST |
| **URL** | /api/refunds |
| **Headers** | Content-Type: application/json, Authorization: Bearer token |
| **Request Body** | {"order_id": 101, "payment_id": "PAY001", "reason": "Order cancelled by customer"} |
| **Expected Status Code** | 201 Created |
| **Expected Response** | {"refund_id": "REF001", "status": "Initiated", "amount": 999, "expected_days": 5} |
| **Priority** | High |

---

### TC_PAY_013
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_013 |
| **Title** | Verify POST refund returns 400 for order that was not paid |
| **Method** | POST |
| **URL** | /api/refunds |
| **Headers** | Content-Type: application/json, Authorization: Bearer token |
| **Request Body** | {"order_id": 999, "payment_id": "PAY999", "reason": "Order cancelled"} |
| **Expected Status Code** | 400 Bad Request |
| **Expected Response** | {"error": "No payment found for this order"} |
| **Priority** | High |

---

## GET — Refund Status

---

### TC_PAY_014
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_014 |
| **Title** | Verify GET refund status returns correct refund details |
| **Method** | GET |
| **URL** | /api/refunds/REF001 |
| **Headers** | Authorization: Bearer token |
| **Request Body** | None |
| **Expected Status Code** | 200 OK |
| **Expected Response** | {"refund_id": "REF001", "status": "Processed", "amount": 999} |
| **Priority** | High |

---

## Critical API Security Test Cases

---

### TC_PAY_015 — Security Testing
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_015 |
| **Title** | Verify payment API does not expose sensitive card or UPI details in response |
| **Method** | POST |
| **URL** | /api/payments/initiate |
| **Headers** | Content-Type: application/json, Authorization: Bearer token |
| **Request Body** | {"order_id": 101, "amount": 999, "payment_method": "UPI", "upi_id": "rahul@oksbi"} |
| **Expected Status Code** | 201 Created |
| **Expected Response** | Response body must NOT contain full UPI ID, PIN, or any sensitive payment credentials |
| **Priority** | Critical |

---

### TC_PAY_016 — Security Testing
| Field | Details |
|---|---|
| **Test Case ID** | TC_PAY_016 |
| **Title** | Verify payment API is served over HTTPS only |
| **Method** | POST |
| **URL** | http://api.ecommerce-test.com/api/payments/initiate (HTTP not HTTPS) |
| **Headers** | Content-Type: application/json |
| **Request Body** | {"order_id": 101, "amount": 999, "payment_method": "UPI", "upi_id": "rahul@oksbi"} |
| **Expected Status Code** | 301 Moved Permanently or connection refused |
| **Expected Response** | Request redirected to HTTPS or rejected — plain HTTP payment requests must never succeed |
| **Priority** | Critical |

---

## API Testing Summary

| Total Test Cases | 16 |
|---|---|
| Critical Priority | 5 |
| High Priority | 10 |
| Medium Priority | 1 |
| Methods Covered | POST, GET |
| Security Cases | 2 |
| BVA Cases | 1 |
| Error Guessing Cases | 1 |

---

## Postman Testing Checklist

For every API request in Postman verify:

- [ ] Correct HTTP method selected
- [ ] Correct URL entered
- [ ] Required headers added
- [ ] Authorization token added where required
- [ ] Request body in correct JSON format
- [ ] Status code matches expected
- [ ] Response body contains required fields
- [ ] Response time under acceptable limit
- [ ] Error responses contain clear error messages
- [ ] Sensitive data not exposed in response
