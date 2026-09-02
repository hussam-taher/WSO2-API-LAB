# Enterprise API Gateway & Security Lab (WSO2 APIM)

A practical implementation of an Enterprise API Gateway setup using **WSO2 API Manager 4.x** and **Docker Compose**. This lab demonstrates API lifecycle management, token-based authentication via **OAuth 2.0 / JWT**, and rate limiting on containerized microservices.

## Architecture & Traffic Flow
`Client (Postman)` ➔ `WSO2 API Gateway (:8243)` ➔ `Token Validation (JWT/OAuth2)` ➔ `Pass-through (Synapse NIO Engine)` ➔ `Backend Service (:8080)`

## Features Implemented
* **Lifecycle Management:** Designed, published, and deployed REST APIs through WSO2 Publisher Portal.
* **API Security:** Enforced mandatory Bearer Token validation using OAuth 2.0 / JWT tokens.
* **Traffic Management:** Configured rate limiting (throttling tiers) via Subscription Business Plans (Bronze tier).
* **Developer Portal Workflow:** Generated application client credentials and subscribed to managed APIs.
* **Automated Integration Testing:** Validated status codes (401 Unauthorized vs 200 OK) using Postman.

## How to Run Locally

1. Clone the repository and run the containers:
   \`\`\`bash
   docker compose up -d
   \`\`\`
2. Access the portals:
   * **Publisher:** `https://localhost:9443/publisher`
   * **DevPortal:** `https://localhost:9443/devportal`
   * **Gateway Endpoint:** `https://localhost:8243/services/1.0.0/get`

## Verification & Testing
Import `./postman/wso2_tests.json` into Postman:
* **Test 1 (Unauthorized):** Sending a request without credentials triggers HTTP `401 Unauthorized` (`900901 Invalid Credentials`).
* **Test 2 (Authorized):** Supplying a valid JWT Bearer token allows the Gateway to route traffic to the backend, returning HTTP `200 OK` from `Synapse-PT-HttpComponents-NIO`.
