# curl

## 1. What is `curl`?

`curl` (**C**lient **URL**) is a **command-line tool** for transferring data between your computer and a server.
It supports many protocols, including **HTTP, HTTPS, FTP, SFTP**, and more.

Typical use cases:

-   Test web APIs
-   Send HTTP requests (GET / POST)
-   Download or upload files
-   Debug web services

------

## 2. Check if `curl` is installed

Most Linux distributions include `curl` by default.

```bash
curl --version
```

If not installed:

### Ubuntu / Debian

```bash
sudo apt update
sudo apt install curl
```

### CentOS / Rocky / AlmaLinux

```bash
sudo yum install curl
```

------

## 3. Basic usage

### Fetch a web page (GET request)

```bash
curl https://example.com
```

The HTML content is printed directly to the terminal.

------

### Save output to a file

```bash
curl -O https://example.com/file.zip
```

(`-O` keeps the original filename)

```bash
curl -o myfile.zip https://example.com/file.zip
```

(`-o` lets you rename the file)

------

## 4. Show download progress

```bash
curl -O https://example.com/file.zip
```

By default, `curl` shows a progress bar.

Silent mode:

```bash
curl -s https://example.com
```

------

## 5. Follow redirects

Many URLs redirect automatically.

```bash
curl -L https://example.com
```

(`-L` follows HTTP 301 / 302 redirects)

------

## 6. View HTTP response details

### Show response headers

```bash
curl -I https://example.com
```

------

### Show full request + response (debug)

```bash
curl -v https://example.com
```

------

## 7. Work with APIs (very common!)

### Send GET request with query parameters

```bash
curl "https://api.example.com/search?q=linux&page=1"
```

------

### Send POST request

```bash
curl -X POST https://api.example.com/login
```

------

### Send JSON data

```bash
curl -X POST https://api.example.com/login \
     -H "Content-Type: application/json" \
     -d '{"username":"user","password":"123456"}'
```

------

## 8. Use authentication

### HTTP Basic Auth

```bash
curl -u username:password https://example.com/protected
```

⚠️ Passwords may be saved in shell history.

------

## 9. Upload files

```bash
curl -F "file=@test.txt" https://example.com/upload
```

------

## 10. Limit download speed

```bash
curl --limit-rate 500k -O https://example.com/file.iso
```

------

## 11. Common options summary

| Option | Meaning                 |
| ------ | ----------------------- |
| `-o`   | Output to file (rename) |
| `-O`   | Save with original name |
| `-L`   | Follow redirects        |
| `-I`   | Headers only            |
| `-X`   | HTTP method             |
| `-H`   | Add HTTP header         |
| `-d`   | Send data               |
| `-u`   | Authentication          |
| `-v`   | Verbose mode            |

------

## 12. `curl` vs `wget`

| `curl`                  | `wget`                  |
| ----------------------- | ----------------------- |
| Best for APIs           | Best for file downloads |
| Supports many protocols | Focused on downloads    |
| Fine-grained control    | Recursive downloads     |

👉 **Rule of thumb**:
Use **`curl`** for APIs and debugging, **`wget`** for bulk downloads.

------

## 13. Practical examples

```bash
curl https://example.com
curl -I https://example.com
curl -L -O https://example.com/app.tar.gz
curl -X POST -d "name=tom&age=18" https://example.com/form
```

------

## 14. Get help

```bash
curl --help
man curl
```

------

## ✅ Summary

-   `curl` is a powerful tool for interacting with web services
-   Essential for API testing and debugging
-   Widely used in DevOps, backend, and scripting