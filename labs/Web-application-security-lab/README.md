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

# Step 2 – Configure Burp Suite Proxy

Burp Suite was used to intercept and analyze HTTP traffic between the browser and the application.

Proxy listener configuration:

127.0.0.1:8080

Browser proxy settings were configured in Windows LAN settings.  
