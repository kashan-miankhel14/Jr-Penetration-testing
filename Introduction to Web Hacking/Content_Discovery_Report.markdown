# TryHackMe Jr Penetration Tester: Content Discovery Report

## Overview
This room introduces techniques for discovering hidden or unlinked content on a web server, including files, directories, and endpoints, using both manual and automated methods.

## Problems Solved and Methods Used
1. **Manual Content Discovery**:
   - **Problem**: Identify hidden files or directories without automated tools.
   - **Solution**:
     - Manually tested common file and directory names by appending them to the base URL (e.g., `http://<MACHINE_IP>/admin`, `/backup.zip`).
     - Used browser developer tools to inspect HTML and JavaScript for references to hidden resources.
     - Checked the `robots.txt` file (`http://<MACHINE_IP>/robots.txt`) for disallowed paths that might reveal sensitive endpoints.
   - **Commands/Techniques**:
     - Browser: Navigate to `http://<MACHINE_IP>/robots.txt`.
     - Manual enumeration: Test URLs like `/admin`, `/backup`, `/config.php`.
     - Developer tools: `F12 > Elements or Sources tab` to find referenced files.

2. **Automated Content Discovery with dirb**:
   - **Problem**: Use an automated tool to enumerate files and directories.
   - **Solution**:
     - Used the `dirb` tool to perform directory brute-forcing against the target server.
     - Ran `dirb` with a common wordlist to discover hidden directories and files.
     - Analyzed the output to identify accessible endpoints, such as configuration files or admin panels.
   - **Commands/Techniques**:
     - Command: `dirb http://<MACHINE_IP> /usr/share/wordlists/dirb/common.txt`.
     - Optional: Customize wordlist with `-w <wordlist_path>` or adjust extensions with `-X .php,.txt`.
     - Review output for HTTP status codes (e.g., `200 OK` for accessible resources).

3. **Identifying Sensitive Files**:
   - **Problem**: Locate sensitive files exposed on the server.
   - **Solution**:
     - Used `dirb` results to identify files like `config.php`, `backup.sql`, or `.env`.
     - Manually verified discovered files by accessing them in the browser to check for sensitive data (e.g., credentials or database details).
   - **Commands/Techniques**:
     - Browser: Navigate to discovered URLs (e.g., `http://<MACHINE_IP>/config.php`).
     - Command: `curl http://<MACHINE_IP>/<discovered_file>` to fetch file contents.
     - Manual inspection of file contents for sensitive information.

## Tools Used
- Browser: For manual enumeration and inspecting `robots.txt`.
- dirb: For automated directory and file enumeration.
- curl: To fetch and verify discovered files.