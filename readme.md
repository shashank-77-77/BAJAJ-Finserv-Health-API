# Bajaj Health Automation Challenge – API Testing (Postman)

## 📌 Project Overview

This repository contains a **comprehensive API automation test suite** created for the **Bajaj Health Automation Challenge**.  
The solution validates the **Create User API** using **Postman**, with strong emphasis on **business rules**, **authorization enforcement**, **negative testing**, and **HTTP contract validation**.

The implementation reflects **enterprise QA practices**, including:
- Environment-based configuration
- Header-driven authorization
- Data-driven negative scenarios
- Clear test intent and traceability

---

## 🎯 Objective

The primary objectives of this project are to:

- Validate the **Create User** API functionality
- Implement **as many test cases as possible**, beyond the provided hints
- Ensure **roll-number header enforcement** for evaluator credit
- Demonstrate **real-world API testing maturity**

---

## 🧰 Tools & Technologies

- **Postman** – API testing and automation
- **REST APIs** – HTTP-based service testing
- **JSON** – Request and response payloads
- **Postman Environments** – Configuration abstraction

---

## 🌐 API Details

### Base URL
https://xxxxxxxxxxxxxxx


### Endpoint Under Test
POST /autxxxxxxxxxx-cxxxxxxxs/disaxxxxxx


### Mandatory Header
roll-number: 2xxxxxxxxxxx


> ⚠️ Any request executed **without this header** is considered invalid and does **not receive evaluation credit**.

---

## 🔧 Environment Setup (Demo Configuration)

Create a **Postman Environment** with the following values:

### Environment Name
Bajaj-Health-Automation-NEW


### Environment Variables (Demo Data)
```json
{
  "baseUrl": "https://crxxxxxxxxxxx",
  "rollNumber": "25xxxxxxxxxx"
}
Select this environment before executing any request.

📂 Test Data (Demo Data Used)
The following demo data is used consistently across test cases to ensure reproducibility:

Field	Demo Value
firstName	Shxxxxxx
lastName	Maxxxx
phoneNumber	7770xx
emailId	shxxxxxxhxxxxxxxxxxx@gmail.com
Additional demo values are derived from this baseline to test duplicates and validation failures.

✅ Implemented Test Cases
A total of 7 test cases have been implemented, covering functional, negative, and edge scenarios.

#	Test Case	Category
1	Happy Path – Create Valid User	Functional
2	Missing roll-number Header	Authorization
3	Duplicate Phone Number	Business Rule
4	Duplicate Email	Business Rule
5	Missing firstName	Mandatory Field
6	Invalid Email Format	Format Validation
7	GET Method Not Allowed	HTTP Protocol
🧪 Test Case Details with Demo Data
1️⃣ Happy Path – Create Valid User
Request Body

{
  "firstName": "Sxxxxxxxxxxk",
  "lastName": "Maxxxxxr",
  "phoneNumber": 7770xxxxxxxxxxxx01,
  "emailId": "shaxxxxxshxxxxxxxxxxxx845xxxxxxxxx82@gmail.com"
}
Expected Result

HTTP 200 OK

User created successfully

2️⃣ Missing roll-number Header
Condition

roll-number header is intentionally removed

Request Body

{
  "firstName": "NoRoll",
  "lastName": "User",
  "phoneNumber": 7770010002,
  "emailId": "noroll@gmail.com"
}
Expected Result

HTTP 401 Unauthorized

3️⃣ Duplicate Phone Number
Condition

Same phone number as Happy Path

Request Body

{
  "firstName": "Duplicate",
  "lastName": "Phone",
  "phoneNumber": 7770010001,
  "emailId": "duplicatephone@gmail.com"
}
Expected Result

HTTP 400 Bad Request

Message: phone number already used

4️⃣ Duplicate Email
Condition

Same email as Happy Path

Request Body

{
  "firstName": "Duplicate",
  "lastName": "Email",
  "phoneNumber": 7770010003,
  "emailId": "shashank250845920082@gmail.com"
}
Expected Result

HTTP 400 Bad Request

Message: email already used

5️⃣ Missing firstName
Condition

Mandatory field omitted

Request Body

{
  "lastName": "NoFirstName",
  "phoneNumber": 7770010004,
  "emailId": "nofirst@gmail.com"
}
Expected Result

HTTP 400 Bad Request

Validation error for required field

6️⃣ Invalid Email Format
Condition

Invalid email structure

Request Body

{
  "firstName": "Invalid",
  "lastName": "Email",
  "phoneNumber": 7770010005,
  "emailId": "invalidemail"
}
Expected Result

Validation failure detected

Observed Response: 500 Internal Server Error

QA Insight

Validation exists, but error is incorrectly mapped to 500 instead of 400. This is a backend exception-handling issue, not a test failure.

7️⃣ GET Method Not Allowed
Condition

GET request sent to POST-only endpoint

Request

GET /automation-campus/disabled/create/user
Expected / Observed Result

HTTP 404 Resource Not Found

Explanation

The backend does not expose a GET route for this endpoint, so routing fails before method validation.

▶️ Execution Instructions
Open Postman

Import the Postman collection JSON

Create and select the environment:

Bajaj-Health-Automation-NEW
Execute requests sequentially from top to bottom

Sequential execution is required due to data dependencies.
