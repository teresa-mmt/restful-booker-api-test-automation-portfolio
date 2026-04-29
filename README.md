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

### Defect 1

Create Booking with missing required field returns 500 instead of expected 400

Risk:

Backend crashes instead of safe validation handling

---

### Defect 2

API accepts invalid booking date logic

Example:

checkout date earlier than checkin date

Risk:

Impossible business bookings are allowed

---

### Defect 3

Update Booking accepts invalid totalprice datatype instead of rejecting request

Risk:

Invalid business data enters production

---

## Newman Execution

### Real API Tests

```bash
newman run "RESTful Booker API Test Automation Portfolio.postman_collection.json" -e "RESTful Booker - QA Env.postman_environment.json"
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

This project reflects production-focused QA thinking rather than simple API checking.
