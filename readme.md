# Bajaj Health Automation Challenge – Demo API Testing (Postman)

## 📌 Project Overview

This repository contains a **demo-safe API automation test suite** created for the **Bajaj Health Automation Challenge**.  
All requests, credentials, URLs, and payloads have been intentionally replaced with **non-production demo data** to ensure **safe sharing and public GitHub visibility**.

The test suite validates a **Create User API** using **Postman**, covering functional correctness, authorization checks, business rules, input validation, and HTTP protocol compliance.

---

## 🎯 Objective

The objectives of this demo project are to:

- Demonstrate structured **API test design**
- Implement **positive and negative test cases**
- Enforce mandatory **roll-number header validation**
- Showcase **enterprise QA practices** using Postman
- Provide a **safe, reproducible demo** without real user data

---

## 🧰 Tools & Technologies

- **Postman** – API testing and automation
- **REST APIs** – HTTP-based service validation
- **JSON** – Request and response payloads
- **Postman Environments** – Runtime configuration management

---

## 🌐 Demo API Details

> ⚠️ **Important:**  
> This repository uses **demo endpoints and demo credentials only**.  
> The API URL below is for demonstration and documentation purposes.

### Demo Base URL
https://example-api.test


### Endpoint Under Test
POST /automation-campus/disabled/create/user


### Mandatory Header
roll-number: DEMO_ROLL_0001


Any request executed without this header is expected to fail with an authorization error.

---

## 🔧 Environment Setup (Demo)

Create a **Postman Environment** with the following configuration:

### Environment Name
Bajaj-Health-Automation-DEMO


### Environment Variables
```json
{
  "baseUrl": "https://example-api.test",
  "rollNumber": "DEMO_ROLL_0001"
}
Ensure this environment is selected before running any request.

📂 Demo Test Data
All test cases use the following demo data:

Field	Demo Value
firstName	Demo
lastName	User
phoneNumber	9000000001
emailId	demo.user1@example.com
Additional demo values are derived from this baseline to validate duplicate and negative scenarios.

✅ Implemented Test Cases
The Postman collection implements 7 demo test cases, covering functional, negative, and protocol scenarios.

#	Test Case	Category
1	Happy Path – Create Valid User	Functional
2	Missing roll-number Header	Authorization
3	Duplicate Phone Number	Business Rule
4	Duplicate Email	Business Rule
5	Missing firstName	Mandatory Field
6	Invalid Email Format	Format Validation
7	GET Method Not Allowed	HTTP Protocol
🧪 Test Case Details (Demo)
1️⃣ Happy Path – Create Valid User
Request Body

{
  "firstName": "Demo",
  "lastName": "User",
  "phoneNumber": 9000000001,
  "emailId": "demo.user1@example.com"
}
Expected Result

HTTP 200 OK

User successfully created

2️⃣ Missing roll-number Header
Condition

roll-number header omitted

Request Body

{
  "firstName": "Demo",
  "lastName": "NoHeader",
  "phoneNumber": 9000000002,
  "emailId": "demo.noheader@example.com"
}
Expected Result

HTTP 401 Unauthorized

3️⃣ Duplicate Phone Number
Condition

Same phone number as Happy Path

Request Body

{
  "firstName": "Demo",
  "lastName": "DuplicatePhone",
  "phoneNumber": 9000000001,
  "emailId": "demo.duplicatephone@example.com"
}
Expected Result

HTTP 400 Bad Request

4️⃣ Duplicate Email
Condition

Same email as Happy Path

Request Body

{
  "firstName": "Demo",
  "lastName": "DuplicateEmail",
  "phoneNumber": 9000000003,
  "emailId": "demo.user1@example.com"
}
Expected Result

HTTP 400 Bad Request

5️⃣ Missing firstName
Condition

Mandatory field omitted

Request Body

{
  "lastName": "NoFirstName",
  "phoneNumber": 9000000004,
  "emailId": "demo.nofirstname@example.com"
}
Expected Result

HTTP 400 Bad Request

6️⃣ Invalid Email Format
Condition

Invalid email structure

Request Body

{
  "firstName": "Demo",
  "lastName": "InvalidEmail",
  "phoneNumber": 9000000005,
  "emailId": "invalidemail"
}
Expected Result

Validation error detected

Observed Response may be 500 Internal Server Error (demo backend behavior)

7️⃣ GET Method Not Allowed
Condition

GET request sent to POST-only endpoint

Request

GET /automation-campus/disabled/create/user
Expected / Observed Result

HTTP 404 Resource Not Found

This indicates that the GET route is not exposed at the routing layer.

▶️ Execution Instructions
Open Postman

Import the demo Postman collection JSON

Create and select the environment:

Bajaj-Health-Automation-DEMO
Execute requests sequentially from top to bottom

Sequential execution is required due to data dependencies.

