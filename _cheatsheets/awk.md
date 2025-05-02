---
layout: cheatsheet
title: "Awk"
---

## Basics

| Command                                | Description                                      |
|----------------------------------------|--------------------------------------------------|
| `awk '{print}' file`                   | Print every line                                 |
| `awk '{print $1}' file`                | Print first field of each line                   |
| `awk '{print $1, $3}' file`            | Print fields 1 and 3                             |
| `awk -F ':' '{print $1}' /etc/passwd`  | Use `:` as field separator                       |

---

## Conditions & Matching

| Command                                  | Description                                     |
|------------------------------------------|-------------------------------------------------|
| `awk '/pattern/ {print}' file`           | Print lines matching pattern                    |
| `awk '$3 > 1000 {print $1}' file`        | Print field 1 if field 3 > 1000                 |
| `awk '$1 ~ /admin/ {print $2}' file`     | Match field 1 with regex                        |
| `awk 'NR==1 {print}' file`               | Print only first line                           |

---

## Built-in Vars

| Variable  | Description                                  |
|-----------|----------------------------------------------|
| `$0`      | Entire line                                  |
| `$1...$n` | Fields in the line                           |
| `NR`      | Current record (line) number                 |
| `NF`      | Number of fields in current record           |
| `FS`      | Field separator (default: space/tab)         |
| `OFS`     | Output field separator (default: space)      |

---

## Loops & Blocks

| Command Example                                              | Description                                      |
|--------------------------------------------------------------|--------------------------------------------------|
| `awk '{sum += $2} END {print sum}' file`                     | Sum all values in field 2                        |
| `awk 'BEGIN {print "Start"} {print} END {print "End"}' file` | Pre/Post-processing blocks                       |
| `awk 'NF > 0' file`                                          | Print only non-empty lines                       |

---

## Field Slicing

| Command Example                                     | Description                                      |
|-----------------------------------------------------|--------------------------------------------------|
| `awk -F ',' '{print $1,$NF}' data.csv`              | First and last column in CSV                     |
| `awk '{print $(NF-1)}' file`                        | Second to last field                             |
| `awk '{print length($0)}' file`                     | Print length of each line                        |

---

## Other Moves

| Command Example                                                 | Use Case                                  |
|-----------------------------------------------------------------|-------------------------------------------|
| `who | awk '{print $1}' | sort | uniq`                          | List unique logged-in users               |
| `ps aux | awk '$3 > 50 {print $1, $3, $11}'`                    | High CPU usage processes                  |
| `netstat -tunap | awk '/ESTABLISHED/ {print $5}'`               | Show established remote IPs               |
| `cat access.log | awk '{print $1}' | sort | uniq -c | sort -nr` | Top source IPs from logs                  |
| `awk -F: '$3 >= 1000 {print $1}' /etc/passwd`                   | List real users (non-system accounts)     |

---

## One-Liners from Hell

| Task                               | One-Liner                                            |
|------------------------------------|------------------------------------------------------|
| Count lines                        | `awk 'END {print NR}' file`                          |
| Average from column                | `awk '{total += $1} END {print total/NR}' file`      |
| CSV to TSV                         | `awk 'BEGIN {FS=","; OFS="\t"} {print}' file.csv`    |
| Delete trailing whitespace         | `awk '{$1=$1; print}' file`                          |

---
