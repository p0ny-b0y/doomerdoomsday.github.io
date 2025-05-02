---
layout: cheatsheet
title: "Sed"
---

## Basic Usage

| Command                             | Description                                  |
|-------------------------------------|----------------------------------------------|
| `sed 's/foo/bar/' file`             | Replace first "foo" with "bar" per line      |
| `sed 's/foo/bar/g' file`            | Replace **all** "foo" with "bar" per line    |
| `sed -i 's/foo/bar/g' file`         | In-place edit (modifies original file)       |
| `sed '2s/foo/bar/' file`            | Replace "foo" with "bar" only on line 2      |
| `sed -n '5p' file`                  | Print line 5 only                            |
| `sed -n '5,10p' file`               | Print lines 5 to 10                          |
| `sed '5d' file`                     | Delete line 5                                |

---

## Pattern Matching

| Command                                  | Description                                  |
|------------------------------------------|----------------------------------------------|
| `sed '/pattern/d' file`                  | Delete lines matching pattern                |
| `sed -n '/pattern/p' file`               | Print lines that match pattern               |
| `sed 's/[0-9]/#/g' file`                 | Replace all digits with `#`                  |
| `sed -E 's/(pass)[0-9]+/\1***/g' file`   | Regex group match and replace                |

---

## In-Place Editing

| OS        | Command Example                              | Note                                       |
|-----------|----------------------------------------------|--------------------------------------------|
| Linux     | `sed -i 's/foo/bar/g' file`                  | Works as-is                                |
| macOS     | `sed -i '' 's/foo/bar/g' file`               | macOS needs empty string after `-i`        |

---

## Insert / Append / Delete

| Command                        | Description                                  |
|--------------------------------|----------------------------------------------|
| `sed '1i\New line' file`       | Insert before line 1                         |
| `sed '$a\New line' file`       | Append after last line                       |
| `sed '3d' file`                | Delete line 3                                |
| `sed '/pattern/d' file`        | Delete lines matching pattern                |

---

## Multi-Command Chains

| Command                                  | Description                                  |
|------------------------------------------|----------------------------------------------|
| `sed -e 's/foo/bar/' -e 's/baz/qux/'`    | Run multiple expressions in sequence         |
| `sed -n -e '/start/,/end/p'`             | Print range of lines between matches         |

---

## Hacker Moves

| Command Example                                           | Use Case                                  |
|-----------------------------------------------------------|-------------------------------------------|
| `cat config.yaml | sed 's/api_key:.*/api_key: REDACTED/'` | Mask keys in config                       |
| `strings dump.bin | sed -n '/BEGIN/,/END/p'`              | Extract PEM block from binary             |
| `nmap -oG scan.gnmap | sed -n '/open/p'`                  | Filter open port lines                    |
| `sed -i '/^#/d' .env`                                     | Strip out all comment lines               |
| `sed 's/\x1b\[[0-9;]*m//g'`                               | Remove ANSI color codes                   |

---

