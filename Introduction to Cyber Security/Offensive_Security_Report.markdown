# TryHackMe Jr Penetration Tester: Offensive Security Report

## Overview
This room introduces offensive security concepts, focusing on the role of an ethical hacker in identifying and exploiting vulnerabilities in a safe, legal environment. It includes a practical exercise to hack a simulated web application (FakeBank) to demonstrate basic penetration testing techniques.[](https://iritt.medium.com/offensive-security-intro-jr-penetration-tester-introduction-to-cyber-security-tryhackme-7590404f2e46)

## Problems Solved and Methods Used
1. **Understanding Offensive Security**:
   - **Problem**: Define offensive security and its role in cybersecurity.
   - **Solution**:
     - Learned that offensive security involves proactively identifying and exploiting vulnerabilities to simulate attacker behavior, helping organizations strengthen their defenses.
     - Reviewed the room’s theoretical content on ethical hacking, including the importance of permission and scope in penetration testing.
     - Answered questions about offensive security roles (e.g., identifying the type of hacker who legally tests systems).
   - **Commands/Techniques**:
     - No commands required; theoretical answers submitted via TryHackMe’s interface.
     - Read and understood content: Reviewed definitions and roles (e.g., ethical hacker as a White Hat).
     - Browser: Used TryHackMe’s interface to submit answers to questions like “What type of hacker legally tests systems?” (Answer: White Hat).

2. **Enumerating Hidden Pages**:
   - **Problem**: Find hidden pages on the FakeBank web application to identify vulnerabilities.
   - **Solution**:
     - Started the provided virtual machine (FakeBank) via the “Start Machine” button, accessing it in split view.
     - Used browser developer tools to inspect the FakeBank website’s HTML and JavaScript for references to hidden pages.
     - Manually tested URLs (e.g., `http://<MACHINE_IP>/admin`) to discover unlinked pages.
   - **Commands/Techniques**:
     - Browser: `F12 > Elements tab` to inspect HTML for hidden links or comments.
     - Manual enumeration: Tested URLs like `http://<MACHINE_IP>/hidden`, `/admin`, or `/secret`.
     - Command: `curl http://<MACHINE_IP>/robots.txt` to check for disallowed paths that might reveal hidden pages.

3. **Exploiting a Vulnerability to Transfer Funds**:
   - **Problem**: Exploit a vulnerability in FakeBank to transfer money to an account.
   - **Solution**:
     - Identified a vulnerable form or endpoint in FakeBank (e.g., a transfer form lacking proper validation).
     - Used Burp Suite or browser tools to intercept and modify a `POST` request, altering parameters (e.g., `amount` or `account_id`) to perform an unauthorized transfer.
     - Confirmed the transfer by checking the account balance or server response.
   - **Commands/Techniques**:
     - Burp Suite: `Proxy > Intercept > Toggle Intercept On` to capture the transfer request.
     - Modify request: Changed parameters (e.g., `amount=1000` to `amount=10000`) in the intercepted `POST` request.
     - Command: `curl -X POST http://<MACHINE_IP>/transfer -d "account_id=123&amount=10000"` to test the endpoint.
     - Browser: Refreshed the FakeBank page to verify the transfer.

## Tools Used
- **Browser (Firefox/Chrome)**: For accessing FakeBank and inspecting HTML.
- **Burp Suite Community Edition**: For intercepting and modifying HTTP requests.
- **curl**: For testing endpoints and retrieving `robots.txt`.
- **TryHackMe Virtual Machine (FakeBank)**: For practical exploitation.