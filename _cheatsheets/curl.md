---
layout: cheatsheet
title: "Curl Commands"
---

## Options

| Command                 | Description                                      |
|-------------------------|--------------------------------------------------|
| `curl -o [file]`        | --output: write to file                          |
| `curl -O [URL]`         | Save with original filename (`-O` not `-o`)      |
| `curl -u user:pass`     | --user: authentication                           |
| `curl -v`               | --verbose output                                 |
| `curl -vv`              | extra verbose output                             |
| `curl -s`               | --silent: no progress or errors shown            |
| `curl -S`               | --show-error: shows errors with `-s`             |
| `curl -i`               | --include: include HTTP headers in output        |
| `curl -I`               | --head: fetch headers only                       |

---

## Request

| Command             | Description                              |
|---------------------|------------------------------------------|
| `curl -X POST`      | --request: specify request type          |
| `curl -L`           | --location: follow redirects             |
| `curl -F`           | --form: send multipart form data         |

---

## Data

| Command                | Description                                      |
|------------------------|--------------------------------------------------|
| `curl -d 'data'`       | --data: send POST data, URL encoded              |
| `curl -d @file`        | --data: read POST data from file                 |
| `curl -G`              | --get: send data with GET instead of POST        |

---

## Headers

| Command                      | Description                      |
|------------------------------|----------------------------------|
| `curl -A [string]`           | --user-agent                     |
| `curl -b name=val`           | --cookie: set cookie inline      |
| `curl -b FILE`               | --cookie: load cookies from file |
| `curl -H "X-Foo: y"`         | --header: custom header          |
| `curl --referer [url]`       | Set referer                      |
| `curl --compressed`          | use gzip                         |

---

## SSL/TLS

| Command                                       | Description                                  |
|-----------------------------------------------|----------------------------------------------|
| `curl -E [cert] --cert-type [type]`           | --cert: client certificate (der/pem/eng)     |
| `curl -k`                                     | --insecure: ignore cert warnings             |
| `curl --cacert [file]`                        | use specified CA certificate file            |
| `curl --capath [directory]`                   | use CA certificates from directory           |

---

## Uploads & Downloads

| Command                                 | Description                                  |
|-----------------------------------------|----------------------------------------------|
| `curl -T file ftp://host/path/`         | Upload file via FTP                          |
| `curl --ftp-create-dirs`                | Create directories on FTP server             |

---

## Authentication Types

| Command                                | Description                                  |
|----------------------------------------|----------------------------------------------|
| `curl --ntlm -u user:pass [URL]`       | NTLM authentication                          |
| `curl --digest -u user:pass [URL]`     | HTTP Digest authentication                   |
| `curl --negotiate -u : [URL]`          | GSS-Negotiate (Kerberos/SPNEGO)              |

---

## Debugging & Testing

| Command                            | Description                                  |
|------------------------------------|----------------------------------------------|
| `curl --trace-ascii file`          | Debug output to file                         |
| `curl --trace-time`                | Add timestamps to trace                      |
| `curl -w "%{http_code}\n"`         | Print HTTP status code only                  |
| `curl -w "@format.txt"`            | Use custom output format from file           |

---

## Proxies & Networking

| Command                                | Description                                  |
|----------------------------------------|----------------------------------------------|
| `curl -x http://proxy:port`            | Use an HTTP proxy                            |
| `curl -x socks5://127.0.0.1:9050`      | Use a SOCKS5 proxy (Tor)                     |
| `curl --ipv4` / `--ipv6`               | Force IPv4 or IPv6                           |
| `curl --max-time 5`                    | Timeout after 5 seconds                      |
| `curl --connect-timeout 3`             | Timeout for connection phase                 |

---

## JSON & API Usage

| Command                                                  | Description                              |
|----------------------------------------------------------|------------------------------------------|
| `curl -H "Content-Type: application/json"`               | Set JSON header                          |
| `curl -d '{"name":"qolt"}' -H "Content-Type: application/json"` | Send JSON payload                |
| `curl -X PATCH -d @data.json -H "Content-Type: application/json"` | PATCH with JSON from file     |

---

## Misc Tricks

| Command                                | Description                                  |
|----------------------------------------|----------------------------------------------|
| `curl --limit-rate 100k`               | Throttle bandwidth usage                     |
| `curl --retry 3`                       | Retry failed connections                     |
| `curl -z file http://host`             | Only download if newer than `file`           |
| `curl -e https://google.com`           | Set referer header manually                  |
