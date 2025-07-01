# FFUF (Fuzz Faster U Fool) Cheatsheet

FFUF is a fast, flexible, and powerful command-line tool for web fuzzing. It's known for its speed and versatility.

## Basic Concepts

-   **FUZZ Keyword:** FFUF uses the `FUZZ` keyword as a placeholder for the payload from the wordlist.
-   **Flexibility:** It can be used for much more than just directory brute-forcing, including parameter fuzzing, header fuzzing, and more.

## Common Commands

**Basic Syntax:**
```bash
ffuf -u <target_url>/FUZZ -w <wordlist_path>
```

**Examples:**

-   **Simple Directory/File Fuzzing:**
    ```bash
    ffuf -u http://example.com/FUZZ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt
    ```

-   **Fuzzing for File Extensions:**
    Use the `-e` flag to specify extensions.
    ```bash
    ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -e .php,.html,.txt
    ```
    Alternatively, you can place `FUZZ` where the extension should be:
    ```bash
    ffuf -u http://example.com/indexFUZZ -w /path/to/extensions.txt
    ```

-   **Increase Threads:**
    Use the `-t` flag (default is 40).
    ```bash
    ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -t 100
    ```

-   **Save Output to a File:**
    Use the `-o` flag and specify the format (e.g., `json`, `csv`, `html`).
    ```bash
    ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -o ffuf_results.json
    ```

-   **Filtering Results:**
    FFUF has powerful filtering options.
    -   `-mc <status_codes>`: Match (show only) specific status codes.
    -   `-fs <size>`: Filter (hide) responses of a specific size.
    -   `-fc <status_codes>`: Filter (hide) specific status codes.

    **Example (show only 200, 301, 302):**
    ```bash
    ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -mc 200,301,302
    ```

    **Example (hide 404):**
    ```bash
    ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -fc 404
    ```

-   **Recursive Scanning:**
    Use the `-recursion` flag to automatically scan directories that are discovered.
    ```bash
    ffuf -u http://example.com/FUZZ -w /path/to/wordlist.txt -recursion
    ```

-   **Fuzzing HTTP Headers:**
    Use the `-H` flag to add or fuzz headers.
    ```bash
    # Fuzz for a virtual host
    ffuf -u http://<target_ip> -w /path/to/vhost_wordlist.txt -H "Host: FUZZ.example.com"
    ```

-   **Fuzzing POST Data:**
    Use the `-X` flag for the request method and `-d` for the data.
    ```bash
    ffuf -u http://example.com/login -X POST -d 'username=FUZZ&password=password' -w /path/to/usernames.txt
    ```

## Tips

-   FFUF is incredibly fast. Be careful not to overwhelm the target server.
-   The filtering options are very powerful. Learn to use them to reduce noise in your results.
-   FFUF can be used for a wide range of fuzzing tasks beyond simple directory discovery. Experiment with fuzzing different parts of the HTTP request.
