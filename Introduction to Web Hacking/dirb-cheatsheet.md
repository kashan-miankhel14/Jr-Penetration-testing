# Dirb Cheatsheet

Dirb is a classic, simple, and easy-to-use command-line tool for scanning web servers for hidden files and directories.

## Basic Usage

Dirb's simplicity is one of its key features. The basic syntax is straightforward.

**Basic Syntax:**
```bash
dirb <target_url> [wordlist_path]
```

If you don't provide a wordlist, Dirb will use its default built-in wordlist.

**Examples:**

-   **Simple Scan with Default Wordlist:**
    ```bash
    dirb http://example.com
    ```

-   **Scan with a Specific Wordlist:**
    ```bash
    dirb http://example.com /usr/share/wordlists/dirb/common.txt
    ```

-   **Save Output to a File:**
    Use the `-o` flag.
    ```bash
    dirb http://example.com -o dirb_results.txt
    ```

-   **Scan for Specific File Extensions:**
    Use the `-X` flag.
    ```bash
    dirb http://example.com -X .php,.html,.txt
    ```

-   **Recursive Scanning:**
    Dirb does this by default, but you can control the depth with the `-r` flag (though it's often not necessary to change).

-   **Suppress "Not Found" Messages:**
    Use the `-S` flag for a cleaner output.
    ```bash
    dirb http://example.com -S
    ```

-   **Change User-Agent:**
    Use the `-a` flag to set a custom User-Agent string.
    ```bash
    dirb http://example.com -a "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36"
    ```

## When to Use Dirb

-   **Simplicity:** When you need a quick and easy scan without complex configurations.
-   **Reliability:** Dirb is a well-tested and reliable tool that has been around for a long time.
-   **Default Wordlists:** It comes with its own set of wordlists that are effective for finding common directories and files.

While tools like Gobuster and FFUF are faster and more flexible, Dirb is still a valuable tool for its simplicity and ease of use, especially for beginners.
