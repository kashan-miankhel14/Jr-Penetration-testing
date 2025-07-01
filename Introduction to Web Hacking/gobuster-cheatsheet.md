# Gobuster Cheatsheet

Gobuster is a tool used to brute-force URIs (directories and files), DNS subdomains, and Virtual Host names on web servers.

## Modes

Gobuster has several modes, the most common for web application testing are:

-   `dir`: Directory/file brute-forcing
-   `dns`: DNS subdomain enumeration
-   `vhost`: Virtual host brute-forcing (finding other websites on the same IP)

## Common `dir` Mode Commands

This is the most frequently used mode for finding hidden content.

**Basic Syntax:**
```bash
gobuster dir -u <target_url> -w <wordlist_path>
```

**Examples:**

-   **Simple Directory Scan:**
    ```bash
    gobuster dir -u http://example.com -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt
    ```

-   **Scan for Specific File Extensions:**
    Use the `-x` flag to specify extensions.
    ```bash
    gobuster dir -u http://example.com -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -x php,html,txt
    ```

-   **Increase Threads for Faster Scanning:**
    Use the `-t` flag to set the number of concurrent threads (default is 10).
    ```bash
    gobuster dir -u http://example.com -w /path/to/wordlist.txt -t 50
    ```

-   **Save Output to a File:**
    Use the `-o` flag to specify an output file.
    ```bash
    gobuster dir -u http://example.com -w /path/to/wordlist.txt -o gobuster_results.txt
    ```

-   **Show Full URLs:**
    Use the `--no-error` flag to suppress errors and `-q` for quiet mode, often combined with `-o`.
    ```bash
    gobuster dir -u http://example.com -w /path/to/wordlist.txt -q -o results.txt
    ```

-   **Exclude Specific Status Codes:**
    Use the `-b` flag to exclude status codes you don't want to see.
    ```bash
    gobuster dir -u http://example.com -w /path/to/wordlist.txt -b 403,404,500
    ```

## `dns` Mode for Subdomain Enumeration

**Basic Syntax:**
```bash
gobuster dns -d <target_domain> -w <wordlist_path>
```

**Example:**
```bash
gobuster dns -d example.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```

## `vhost` Mode for Virtual Host Discovery

This is useful when multiple websites are hosted on a single IP address.

**Basic Syntax:**
```bash
gobuster vhost -u http://<target_ip_or_domain> -w <wordlist_path>
```

**Example:**
```bash
# The wordlist should contain potential virtual host names (e.g., admin, dev, internal)
gobuster vhost -u http://example.com -w /path/to/vhost_wordlist.txt
```

## Tips

-   Always use a good wordlist. **SecLists** is the standard.
-   Adjust the number of threads (`-t`) based on the target server's responsiveness and your network connection.
-   Use the `-k` flag to skip SSL certificate verification if you encounter errors with HTTPS sites.
