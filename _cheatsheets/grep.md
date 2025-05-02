---
layout: cheatsheet
title: "Grep"
---

## Basic Usage

| Command                          | Description                                 |
|----------------------------------|---------------------------------------------|
| `grep "pattern" file`            | Search for exact pattern in file            |
| `grep "pattern" *.log`           | Search across multiple files                |
| `grep "pattern" -r .`            | Recursive grep (search all files)           |
| `grep -i "pattern" file`         | Case-insensitive search                     |
| `grep -v "pattern" file`         | Invert match (exclude pattern)              |

---

## Useful Flags

| Flag        | Description                                |
|-------------|--------------------------------------------|
| `-n`        | Show line numbers                          |
| `-r`        | Recursive search through directories       |
| `-l`        | List only filenames with matches           |
| `-c`        | Count of matching lines per file           |
| `-o`        | Print only matched parts of line           |
| `-A NUM`    | Print NUM lines **after** match            |
| `-B NUM`    | Print NUM lines **before** match           |
| `-C NUM`    | Print NUM lines **before and after**       |

---

## Regex Power

| Regex Pattern        | Description                                  |
|----------------------|----------------------------------------------|
| `^pattern`           | Match lines starting with `pattern`          |
| `pattern$`           | Match lines ending with `pattern`            |
| `p.ttern`            | Match `pAttern`, `pOttern`, etc.             |
| `p.*n`               | Match from `p` to `n`, greedy                |
| `[abc]`              | Match one of: a, b, or c                     |
| `[^abc]`             | Match anything except a, b, or c             |
| `[0-9]`              | Match any digit                              |

---

## Combine with Other Tools

| Command Example                                         | Description                                  |
|----------------------------------------------------------|---------------------------------------------|
| `ps aux | grep nginx`                                   | Find running nginx processes                 |
| `cat file.txt | grep -i error`                          | Search for "error" ignoring case             |
| `curl -s site.com | grep "href"`                        | Scrape links from a page                     |
| `nmap -oG scan.gnmap | grep "/open/"`                   | Filter open ports from grepable Nmap output  |
| `find . -type f | xargs grep "password"`                | Search for "password" in all files           |

---

## Other Moves

| Command Example                                         | Purpose                                      |
|---------------------------------------------------------|----------------------------------------------|
| `grep -r "AKIA" .`                                      | Search for AWS access keys                   |
| `grep -r -i "password\|pass\|pwd" .`                    | Hunt for hardcoded credentials               |
| `grep -A2 "Authorization" logs.txt`                     | Get lines after any Authorization header     |
| `strings binary | grep -i "api"`                        | Find API keys in binary                      |
| `grep -E "user|admin|root"`                             | Extended regex (OR) match                    |

---

