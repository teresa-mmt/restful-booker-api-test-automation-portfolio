# RESTful Booker API Test Automation Portfolio

## Project Overview

This project is a professional API test automation portfolio built using Postman and Newman for the RESTful Booker API.

It covers:

* Authentication testing
* Booking CRUD positive flow
* Negative testing
* Contract validation using Postman Mock Server
* Newman CLI execution
* Real defect discovery and validation

The goal of this project is to demonstrate real QA engineering skills, not just basic Postman request execution.

---

## Tools Used

* Postman
* Newman
* JavaScript (Postman Test Scripts)
* Postman Mock Server
* JSON Schema Validation
* GitHub

---

## API Under Test

RESTful Booker API

Base URL:

https://restful-booker.herokuapp.com

This API simulates hotel booking operations and is commonly used for API automation practice.

---

## Collection Structure

### 01_Authentication

* Generate authentication token
* Validate token creation
* Save token dynamically for secured requests

---

### 02_Booking_CRUD_Positive

* Create Booking
* Get Newly Created Booking
* Update Booking
* Get Newly Updated Booking
* Delete Booking
* Confirm Deleted Booking

Validates full end-to-end booking lifecycle.

---

### 03_Booking_Negative_Tests

* Missing required field
* Invalid booking date logic
* Invalid data type
* Update without token
* Delete without token
* Non-existing booking ID

Focus:

Validation handling and business risk protection

---

### 04_Mock_Server_Tests

Using Postman Mock Server:

* Valid schema validation
* Invalid datatype detection
* Missing required field detection
* Extra property detection
* Update contract validation

This proves the automation can detect broken API contracts before production impact.

---

## Key Defects Found

### Defect 1 — Create Booking with Missing Required Field Returns 500 Instead of 400

**Affected Request Name:**
`Create Booking - Missing Required Field`

**Folder:**
`03_Booking_Negative_Tests → Create Booking`

**API Endpoint:**
`POST /booking`

**Test Scenario:**
Create booking request with missing required field (example: missing `firstname`)

**Expected Result:**
API should return `400 Bad Request` for invalid request payload with missing required fields.

**Actual Result:**
API returns `500 Internal Server Error`, which means backend crashes instead of handling validation safely.

**Business Risk:**
Invalid client requests can cause backend instability and unsafe production behavior.

**Proof:**
Newman negative test result:

Expected: 400
Actual: 500

---

### Defect 2 — API Accepts Invalid Booking Date Logic

**Affected Request Name:**
`Negative Create Booking — Invalid Date Logic`

**Folder:**
`03_Booking_Negative_Tests → Create Booking`

**API Endpoint:**
`POST /booking`

**Test Scenario:**
Create booking where checkout date is earlier than checkin date

Example:

* Checkin: `2025-12-10`
* Checkout: `2025-12-05`

**Expected Result:**
API should reject impossible booking dates with `400 Bad Request`.

**Actual Result:**
API returns `200 OK` and successfully creates impossible booking data.

**Business Risk:**
Invalid reservations affect hotel operations, reporting, billing, and customer trust.

**Proof:**
Newman negative test result:

Expected: 400
Actual: 200

---

### Defect 3 — Update Booking Accepts Invalid totalprice Datatype

**Affected Request Name:**
`Negative Update Booking - Invalid Data Type`

**Folder:**
`03_Booking_Negative_Tests → Update Booking`

**API Endpoint:**
`PUT /booking/{{bookingId}}`

**Test Scenario:**
Update booking using invalid datatype:

`"totalprice": "expensive"`

instead of numeric value.

**Expected Result:**
API should reject invalid datatype with `400 Bad Request`.

**Actual Result:**
API accepts invalid payload instead of proper validation handling.

**Business Risk:**
Invalid financial data can affect payment systems, billing, reporting, and customer trust.

**Proof:**
Negative update test confirms validation inconsistency during update flow.


---

## Newman Execution

### Real API Tests

```bash
newman run "RESTful Booker API Test Automation Portfolio.postman_collection.json" -e "RESTful Booker - QA Env.postman_environment.json" --folder "01_Authentication" --folder "02_Booking_CRUD_Positive" --folder "03_Booking_Negative_Tests"
```

### Mock Server Tests

```bash
newman run "RESTful Booker API Test Automation Portfolio.postman_collection.json" -e "RESTful Booker Contract Validation Mock Server.postman_environment.json" --folder "04_Mock_Server_Tests"
```

---

## Final Result

* Full CRUD flow automated
* Authentication handled dynamically
* Negative testing documented
* Contract validation implemented
* Defects identified and analyzed
* Newman execution verified
* Real API testing completed separately from contract validation testing using Postman Mock Server.

This project reflects production-focused QA thinking rather than simple API checking.
