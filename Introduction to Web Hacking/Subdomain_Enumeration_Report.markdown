# TryHackMe Jr Penetration Tester: Subdomain Enumeration Report

## Overview
This room teaches subdomain enumeration to discover hidden subdomains of a target web application, which may reveal additional attack surfaces or sensitive services.

## Problems Solved and Methods Used
1. **Manual Subdomain Guessing**:
   - **Problem**: Identify subdomains using manual techniques.
   - **Solution**:
     - Tested common subdomain names (e.g., `admin.<MACHINE_IP>`, `api.<MACHINE_IP>`) by entering them in the browser.
     - Checked DNS records using online tools or browser-based lookups to identify potential subdomains.
   - **Commands/Techniques**:
     - Browser: Navigate to `http://admin.<MACHINE_IP>` or `https://api.<MACHINE_IP>`.
     - Manual enumeration: Test subdomains like `dev`, `test`, `staging`.

2. **Automated Subdomain Enumeration with gobuster**:
   - **Problem**: Use a tool to enumerate subdomains efficiently.
   - **Solution**:
     - Used `gobuster` with a subdomain-specific wordlist to brute-force subdomains.
     - Configured `gobuster` to query DNS records for the target domain.
     - Analyzed output to identify valid subdomains returning HTTP responses.
   - **Commands/Techniques**:
     - Command: `gobuster dns -d <MACHINE_IP> -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt`.
     - Optional: Use `-t 50` for threading to speed up enumeration.
     - Verify subdomains: Navigate to `http://<discovered_subdomain>.<MACHINE_IP>`.

3. **Exploring Subdomain Content**:
   - **Problem**: Investigate discovered subdomains for vulnerabilities or sensitive data.
   - **Solution**:
     - Accessed identified subdomains in the browser to explore their content.
     - Used developer tools to inspect HTML, JavaScript, or network activity for sensitive information.
     - Tested subdomains for misconfigurations, such as exposed admin panels or directory listings.
   - **Commands/Techniques**:
     - Browser: Navigate to `http://<discovered_subdomain>.<MACHINE_IP>`.
     - Developer tools: `F12 > Elements or Network tab` to analyze responses.
     - Manual testing: Check for endpoints like `/admin` or `/login` on subdomains.

## Tools Used
- Browser: For manual subdomain testing and content inspection.
- gobuster: For automated subdomain enumeration.
- Wordlists: Seclists DNS wordlist for subdomain brute-forcing.