# Web Application Security Lab – OWASP Juice Shop (Windows)

## Lab Overview

This lab demonstrates a hands-on web application security testing lab using OWASP Juice Shop, Docker, and Burp Suite Community Edition.

The objective of this lab was to simulate a basic web application security assessment by intercepting HTTP traffic, analyzing requests, and testing for common web vulnerabilities.

---
# Vulnerability Mapping to OWASP Top 10

| Test Performed | OWASP Category | Description | Tool Used | Evidence |
|---|---|---|---|---|
| SQL Injection Testing | A03:2021 – Injection | Manipulated login request parameters to test backend query handling | Burp Repeater | screenshots/04-sql-injection-test.png |
| Broken Access Control | A01:2021 – Broken Access Control | Modified object identifiers to test authorization enforcement | Burp Repeater | screenshots/05-broken-access-control.png |
| Cross-Site Scripting (XSS) | A03:2021 – Injection | Injected JavaScript payload to test input sanitization | Browser + Burp | screenshots/06-xss-test.png |
| Authentication Testing | A07:2021 – Identification and Authentication Failures | Evaluated login behavior using Burp Intruder payload testing | Burp Intruder | screenshots/07-authentication-testing.png |

# Attack Flow 

User Browser
     ↓
Burp Suite Proxy
     ↓
HTTP Request Interception
     ↓
Parameter Manipulation
     ↓
Server Response Analysis

# Security Testing Methodology

The following testing methodology was used during this lab:

1. **Application Reconnaissance**
   - Explored application functionality
   - Identified authentication features
   - Observed API requests and parameters

2. **Traffic Interception**
   - Configured Burp Suite proxy
   - Captured HTTP requests and responses
   - Analyzed authentication requests

3. **Request Manipulation**
   - Sent requests to Burp Repeater
   - Modified parameters and payloads
   - Observed server behavior and responses

4. **Authorization Testing**
   - Manipulated object identifiers
   - Tested access to unauthorized resources

5. **Input Validation Testing**
   - Injected test payloads into input fields
   - Checked for script execution and input reflection

6. **Authentication Testing**
   - Used Burp Intruder to test login behavior
   - Evaluated rate limiting and response patterns
  
---

# Step 1 – Run OWASP Juice Shop

Start the vulnerable application using Docker.

Command used:
docker run --rm -p 3000:3000 bkimminich/juice-shop

This launches the Juice Shop container and exposes the application on: http://localhost:3000

## Juice Shop Home Page  ![description](screenshots/01-juice-shop-home.png)

# Step 2 – Configure Burp Suite Proxy

Burp Suite was used to intercept and analyze HTTP traffic between the browser and the application.

Proxy listener configuration:

127.0.0.1:8080

Browser proxy settings were configured in Windows LAN settings.  

# Step 3 - Capture Login Request

After creating a test account and logging in, Burp intercepted the authentication request.

Example intercepted request:

POST /rest/user/login HTTP/1.1
Host: localhost:3000
Content-Type: application/json

Example request body:

{
 "email":"test1@test.com",
 "password":"Test123!"
}
## Intercepted Login Request  ![description](screenshots/02-login-request-intercept.png)

# Step 4 – Send Request to Repeater

The captured login request was sent to Burp Repeater to allow manual manipulation and repeated testing.

Process:

Right click intercepted request

Select Send to Repeater

Modify parameters and resend requests

## Normal Login Request in Repeater  ![description](screenshots/03-repeater-normal-request.png)

# Step 5 – SQL Injection Testing

The password field was modified to test for possible SQL injection behavior.

Original request:

"password":"Test123!"

Test payload used:

"password":"' OR 1=1--"

The modified request was sent using Burp Repeater to observe server responses.

## SQL Injection Test ![description](screenshots/04-sql-injection-test.png)

# Step 6 – Broken Access Control Testing

Authorization testing was performed by modifying object identifiers in intercepted requests.

Example request:

GET /rest/basket/6

Modified request:

GET /rest/basket/2

This type of test checks whether the server validates ownership of objects.

## Broken Access Control Test ![description](screenshots/05-broken-access-control.png)

# Step 7 – Cross-Site Scripting (XSS) Testing

Input fields were tested for script injection.

Example payload used:

<script>alert(1)</script>

This payload checks whether the application properly sanitizes user input before rendering it in the browser.

## XSS Test  ![description](screenshots/06-xss-test.png)

# Step 8 – Authentication Testing Using Burp Intruder

The login request was sent to Burp Intruder to test authentication behavior.

Steps:

Capture login request

Send to Intruder

Mark password field as payload position

Test multiple password attempts

Example payload list:

password
123456
admin
test123

## Authentication Testing  ![description](screenshots/07-authentication-testing.png)



