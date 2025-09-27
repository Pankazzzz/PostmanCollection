# 📬 Postman API Test Collection – Comprehensive API Testing Suite

This repository contains a **Postman Collection** that demonstrates testing of various types of APIs including:

- RESTful endpoints
- Auth-protected endpoints
- Public/open APIs
- JSON and XML responses
- Mock APIs (for error and edge case testing)

The collection is designed to showcase **all major types of API testing**, making it perfect for learning, practice, or even as a framework starter for professional API test automation.

---

## 🚀 What’s Included?

🔹 **Types of APIs Covered:**

- User Management API (CRUD)
- Auth APIs (Token, API Key, OAuth 2.0)
- E-commerce APIs (Cart, Orders, Checkout)
- File Upload API
- Query Parameter & Path Param APIs
- Public APIs (e.g., GitHub, JSONPlaceholder)

🔹 **Types of Tests Included:**

| Test Type                  | Description                                                 |
|---------------------------|-------------------------------------------------------------|
| Functional Testing         | Verify API works as intended                                |
| Response Code Checks       | Validate 200/201/400/401/403/500 codes                      |
| Schema Validation          | JSON schema assertions using [tv4] or [Ajv]                 |
| Authentication Testing     | API Key, Bearer Token, OAuth 2.0                            |
| Negative Testing           | Missing headers, wrong params, bad requests                |
| Edge Case Testing          | Empty payloads, invalid data types, max values              |
| Data-Driven Testing        | Using Collection Runner + JSON/CSV files                    |
| Assertions and Tests       | Chai-based tests in "Tests" tab of Postman                 |
| Environment Support        | Dev / QA / Prod via Postman Environments                    |

---

## 🧱 Project Structure

```
postman-api-test-suite/
├── collections/
│   └── Complete-API-Test-Suite.postman_collection.json
├── environments/
│   ├── dev.postman_environment.json
│   ├── qa.postman_environment.json
│   └── prod.postman_environment.json
├── data/
│   ├── user_data.json
│   └── invalid_login_cases.csv
├── README.md
```

---

## 🔧 Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/postman-api-test-suite.git
cd postman-api-test-suite
```

### 2. Import into Postman

- Open [Postman](https://www.postman.com/)
- Click on `Import` → Upload the `.postman_collection.json` file from `collections/`
- Also import the relevant environment from the `environments/` folder

---

## ▶️ Run the Collection

### Option 1: Manually via Postman App

- Open the collection
- Select an environment (`dev`, `qa`, `prod`)
- Hit **Run** to execute the full collection or folder-wise

### Option 2: Run via CLI using [Newman](https://www.npmjs.com/package/newman)

Install Newman:

```bash
npm install -g newman
```

Run the collection:

```bash
newman run collections/Complete-API-Test-Suite.postman_collection.json \
  -e environments/qa.postman_environment.json \
  -d data/user_data.json \
  --reporters cli,html,json \
  --reporter-html-export reports/htmlReport.html
```

---

## ✅ Sample Test Snippets in Postman

### 1. Status Code Validation

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

### 2. Response Body Validation

```javascript
pm.test("Response has user id", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("userId");
});
```

### 3. JSON Schema Validation

```javascript
const schema = {
    "type": "object",
    "properties": {
        "id": { "type": "number" },
        "email": { "type": "string" }
    },
    "required": ["id", "email"]
};

pm.test("Schema is valid", function () {
    pm.response.to.have.jsonSchema(schema);
});
```

---

## 🧪 Test Coverage Overview

- [x] GET, POST, PUT, DELETE endpoints
- [x] Auth mechanisms: API Key, Bearer Token, OAuth2
- [x] Chained API tests (using variables from previous requests)
- [x] Error and boundary testing
- [x] Positive + negative test cases
- [x] Environment-based config
- [x] JSON Schema validations
- [x] Data-driven testing with CSV and JSON

---

## 📊 Reports & CI Integration

You can integrate this test suite with:
- 🧪 **Jenkins** via Newman CLI
- 💻 **GitHub Actions**
- 📦 **Dockerized test runners**
- 📈 **Allure Reports** (via Newman reporters)

Let me know if you want a sample Jenkinsfile or GitHub Actions workflow.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE)
