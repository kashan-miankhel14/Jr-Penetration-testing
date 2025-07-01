# Content Discovery

Content discovery is the process of finding hidden or unlinked files, directories, and endpoints on a web server. This is a crucial step in web application penetration testing as it can reveal sensitive information, administrative interfaces, or vulnerable files that are not meant to be public.

## Manual Techniques

Before using automated tools, it's always a good idea to perform some manual checks.

### `robots.txt`

Web developers use the `robots.txt` file to tell search engine crawlers which pages or files they should not index. This file is always located at the root of the web server (e.g., `http://example.com/robots.txt`) and can often reveal the locations of hidden directories.

**Example `robots.txt`:**
```
User-agent: *
Disallow: /admin/
Disallow: /private/
Disallow: /backups/
```
This file suggests that the directories `/admin/`, `/private/`, and `/backups/` exist on the server.

### `sitemap.xml`

A `sitemap.xml` file is the opposite of `robots.txt`; it lists all the pages that the website owner *wants* search engines to index. Reviewing this file can give you a good overview of the intended structure of the website.

### Favicon Hashing

Sometimes, you can identify the web framework or technologies used by a web application by looking at the hash of its `favicon.ico` file. Many frameworks have a default favicon. You can get the hash of the favicon and search for it in databases to identify the technology.

### Manual Exploration

Simply browsing the website and paying attention to the URL structure, comments in the HTML source code (`Ctrl+U` in most browsers), and JavaScript files can reveal clues about the application's structure and potential hidden endpoints.

## Automated Discovery (Brute-Forcing)

Automated tools use wordlists to rapidly guess the names of directories and files on a web server. This is also known as brute-forcing or directory busting.

### Key Tools

1.  **Gobuster:** A fast and versatile tool written in Go. It's a command-line tool used for brute-forcing URIs (directories and files), DNS subdomains, and Virtual Host names.

    **Common Gobuster Command Structure:**
    ```bash
    # Directory/File brute-forcing
    gobuster dir -u http://<target-ip> -w /path/to/wordlist.txt

    # To search for specific file extensions
    gobuster dir -u http://<target-ip> -w /path/to/wordlist.txt -x php,txt,html

    # To discover virtual hosts (subdomains on the same IP)
    gobuster vhost -u http://<target-ip> -w /path/to/vhost_wordlist.txt
    ```

2.  **FFUF (Fuzz Faster U Fool):** Another extremely fast tool, also written in Go. It's highly flexible and allows for complex fuzzing.

    **Common FFUF Command Structure:**
    ```bash
    # Directory/File brute-forcing (FUZZ is the keyword for the payload)
    ffuf -u http://<target-ip>/FUZZ -w /path/to/wordlist.txt

    # Filter out specific status codes (e.g., 404)
    ffuf -u http://<target-ip>/FUZZ -w /path/to/wordlist.txt -fs 404

    # Fuzz for file extensions
    ffuf -u http://<target-ip>/FUZZ.php -w /path/to/wordlist.txt
    ```

3.  **Dirb:** A classic, simple-to-use command-line tool for web content scanning.

    **Common Dirb Command Structure:**
    ```bash
    dirb http://<target-ip> /path/to/wordlist.txt
    ```

### Wordlists

The effectiveness of automated tools depends heavily on the quality of the wordlist used. **SecLists** is one of the most comprehensive collections of wordlists for all types of security testing.

A good starting point within SecLists for directory busting is:
`/usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt`

## Important Considerations

- **User-Agent:** Some web servers may block requests from common security tools. It's good practice to change your user-agent string to mimic a common browser to avoid being blocked.
- **Recursive Scanning:** Once you find a directory, it's important to run a discovery scan on that new directory as well, as it may contain its own set of hidden files and subdirectories.
- **Throttling/Rate Limiting:** Be mindful of the number of requests you are sending per second. Overwhelming a server can crash it or get your IP address blocked. Most tools have options to control the request rate.
