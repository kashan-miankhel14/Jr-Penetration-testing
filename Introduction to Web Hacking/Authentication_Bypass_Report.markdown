# TryHackMe Jr Penetration Tester: Authentication Bypass Report

## Overview
This room explores techniques to bypass authentication mechanisms in web applications, focusing on vulnerabilities like weak credentials, session mishandling, or flawedBOSE

## Problems Solved and Methods Used
1. **Testing Default or Weak Credentials**:
   - **Problem**: Gain access to a login page using common or default credentials.
   - **Solution**:
     - Identified the login page of the target application (e.g., `http://<MACHINE_IP>/login`).
     - Tested common username/password combinations (e.g., `admin:admin`, `guest:guest`).
     - Checked for hints in HTML comments or error messages revealing valid usernames or weak passwords.
   - **Commands/Techniques**:
     - Browser: Navigate to `http://<MACHINE_IP>/login` and test credentials.
     - Developer tools: `F12 > Elements tab` to inspect login page source for hints.
     - Manual testing: Try credentials like `admin:password`, `user:user`.

2. **Bypassing Authentication via Parameter Manipulation**:
   - **Problem**: Manipulate URL or form parameters to bypass authentication checks.
   - **Solution**:
     - Intercepted a login request using Burp Suite’s proxy to analyze parameters.
     - Modified parameters (e.g., `role=guest` to `role=admin` or `user_id=1`) in the intercepted `POST` or `GET` request.
     - Forwarded the modified request to check if access was granted to restricted areas.
   - **Commands/Techniques**:
     - Burp Suite: `Proxy > Intercept > Toggle Intercept On`.
     - Modify request: Change parameters in the intercepted request (e.g., `role=guest` to `role=admin`).
     - Forward request: Click "Forward" in Burp’s Intercept tab.

3. **Exploiting Session Handling Flaws**:
   - **Problem**: Bypass authentication by manipulating session cookies or tokens.
   - **Solution**:
     - Used Burp Suite to capture the session cookie after logging in with a low-privilege account.
     - Analyzed the cookie for predictable patterns (e.g., sequential IDs or encoded roles).
     - Modified the cookie value (e.g., incrementing a user ID or changing a role identifier) using Burp’s "Repeater" or browser developer tools.
     - Sent the modified request to access restricted resources.
   - **Commands/Techniques**:
     - Burp Suite: `Proxy > HTTP history > Select login request > View Response for cookie`.
     - Modify cookie: `Repeater > Change cookie value` or use browser tools (`F12 > Application > Cookies`).
     - Test modified request: Send via Burp Repeater or refresh the page with altered cookie.

## Tools Used
- Browser: For manual credential testing and cookie manipulation.
- Burp Suite Community Edition: For intercepting and modifying HTTP requests and cookies.
- Developer Tools: For inspecting and altering session cookies.