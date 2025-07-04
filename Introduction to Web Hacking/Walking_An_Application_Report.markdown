# TryHackMe Jr Penetration Tester: Walking An Application Report

## Overview
This room focuses on manual reconnaissance of a web application using browser developer tools, emphasizing exploration of the application's structure to identify vulnerabilities without external tools or scripts.

## Problems Solved and Methods Used
1. **Identifying Hidden HTML Comments**:
   - **Problem**: Find sensitive information, such as developer notes or hidden data, embedded in HTML comments.
   - **Solution**: 
     - Opened the target web application in a browser (e.g., Chrome or Firefox).
     - Accessed developer tools by right-clicking and selecting "Inspect" or pressing `F12`.
     - Navigated to the "Elements" tab to view the HTML source code.
     - Searched for HTML comments using `Ctrl+F` with the query `<!--` to locate comments containing sensitive information, such as developer notes or hints about hidden functionality.
   - **Commands/Techniques**:
     - Browser: `Right-click > Inspect > Elements tab`.
     - Search: `Ctrl+F` with query `<!--` to find comments.
     - Manual inspection for keywords like "TODO", "secret", or "hidden".

2. **Discovering Hidden Links or Pages**:
   - **Problem**: Locate unlinked or hidden pages within the application.
   - **Solution**:
     - Inspected HTML and JavaScript files in the "Sources" tab of developer tools for references to unlisted URLs or endpoints.
     - Used the "Network" tab to monitor HTTP requests during page interactions (e.g., clicking buttons or links) to identify hidden resources.
     - Manually navigated to suspected URLs (e.g., `http://<MACHINE_IP>/secret`) by entering them in the browser address bar.
   - **Commands/Techniques**:
     - Browser: `F12 > Sources tab > Expand JavaScript files`.
     - Network monitoring: `F12 > Network tab > Interact with page`.
     - Manual URL enumeration: Test URLs like `/hidden`, `/admin`, or `/secret`.

3. **Checking for Directory Listings**:
   - **Problem**: Identify exposed directories due to server misconfigurations.
   - **Solution**:
     - Appended common directory paths to the base URL (e.g., `http://<MACHINE_IP>/data`, `/files`).
     - Checked for directory listings where the server displays file indexes due to misconfigurations (e.g., `autoindex on` in Apache).
     - Identified sensitive files or directories by accessing exposed paths.
   - **Commands/Techniques**:
     - Browser: Enter URLs like `http://<MACHINE_IP>/data/`.
     - Manual enumeration: Test paths like `/backup`, `/config`, `/uploads`.
     - Observe server responses for file listings.

## Tools Used
- Browser Developer Tools (Chrome/Firefox): For inspecting HTML, JavaScript, and network activity.