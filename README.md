# 🧪 Postman Collection – Reqres API Tests

This repository contains **two Postman collections** for testing the [Reqres](https://reqres.in) public API. These collections are used to simulate API testing and basic UI logic using Postman’s built-in scripting features.

---

## 📁 Collections Included

### 1. **Reqres API Tests**

Basic API requests with automated tests for:

- ✅ GET list of users
- ✅ POST create user
- ❌ GET invalid endpoint (negative test)

#### Requests:

- **GET /users?page=2**
  - Checks if the status code is 200.
  - Verifies that the `data` array contains at least one user.

- **POST /users**
  - Sends a new user with name `Test` and job `QA`.
  - Asserts status code 201.
  - Validates that the name and job in the response match the request.

- **GET /invalid-endpoint**
  - Simulates a failed request.
  - Checks for a 404 Not Found status code.

---

### 2. **Reqres API + UI Tests**

Extended collection that includes:

- ✅ Simulated UI rendering using response data
- ✅ Token handling for login
- ✅ Use of environment variables for UI testing

#### Requests:

- **POST /users** (Create User)
  - Sends a user named `Andrei` with job `QA Tester`.
  - Checks response status is 201.
  - Verifies `name` and `job` fields.
  - Simulates a UI string like:  
    `"User Andrei has job QA Tester"`  
    and logs it to the console.

- **POST /login** (Test Login)
  - Logs in with valid credentials.
  - Extracts `token` from response and stores it in the Postman environment as `auth_token`.

- **GET /users/2** (Simulated UI Check)
  - Reads environment variables `created_name` and `created_job`.
  - Simulates UI display:  
    `"👤 [Name] works as [Job]"`
  - Tests if both variables are present.

> 📝 **Note:** This request simulates UI testing logic by using environment variables, so it assumes that earlier requests (like user creation) have run successfully and saved values.

---

## 🧪 Testing Details

Each request includes tests in the `Tests` tab using the Postman scripting API. Common test examples:

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

const json = pm.response.json();
pm.expect(json.name).to.eql("Test");
