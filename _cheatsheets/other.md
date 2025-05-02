---
layout: cheatsheet
title: "Awk vs Sed"
---

## 🧠 Use This, Not That: Sed vs Awk

| Task                           | Use Sed                                 | Use Awk                                     |
|--------------------------------|------------------------------------------|----------------------------------------------|
| Replace text inline            | `sed 's/old/new/g' file`                | `awk '{gsub(/old/, "new"); print}' file`     |
| Delete lines with a pattern    | `sed '/pattern/d' file`                 | `awk '!/pattern/' file`                      |
| Print specific lines           | `sed -n '5,10p' file`                   | `awk 'NR>=5 && NR<=10' file`                 |
| Print column(s) from delimited file | ❌                                        | ✅ `awk -F ',' '{print $1, $3}' file.csv`     |
| Math on fields                 | ❌                                        | ✅ `awk '{sum+=$2} END {print sum}'`          |
| Pattern + Action               | ❌                                        | ✅ `awk '$3 > 1000 {print $1}'`               |
| Regex filtering                | ✅ `sed -n '/regex/p'`                  | ✅ `awk '/regex/'`                            |
| Output formatting              | Meh                                      | God-tier `awk '{printf "%.2f\n", $1 * 0.85}'` |

---

## When to Use What

- **Use `sed`** when you:
  - Want a quick substitution
  - Need in-place editing (`-i`)
  - Are dealing with simple text edits, line deletes, or search/replace

- **Use `awk`** when you:
  - Need to work with **fields/columns**
  - Want to do **math**, logic, or **custom output**
  - Need control flow (`if`, `for`, `while`)

---

## TL;DR Cheat

```bash
# sed: string surgery
sed 's/foo/bar/g' file

# awk: field slicing + logic
awk -F ',' '$3 > 1000 {print $1}' data.csv


---

Next up — the **script combo fusion**, the *grep-awk-jq-curl killchain*:

---

## `curl | grep | awk | jq` Cheat Fusion

```markdown
---
layout: cheatsheet
title: "Curl Grep Awk Jq Combo"
---

## Combine the Big 4: `curl`, `grep`, `awk`, `jq`

### API Recon

| Task                               | One-Liner                                                                 |
|------------------------------------|---------------------------------------------------------------------------|
| Fetch & filter JSON                | `curl -s https://api.example.com | jq '.data[] | select(.active)'`       |
| Grab all IPs from webpage          | `curl -s http://site.com | grep -Eo '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+'`     |
| Extract link text from HTML        | `curl -s http://site | grep '<a' | awk -F'[<>]' '{print $3}'`              |

---

### Log & Data Parsing

| Task                               | One-Liner                                                                 |
|------------------------------------|---------------------------------------------------------------------------|
| Find top 10 IPs from logs          | `cat access.log | awk '{print $1}' | sort | uniq -c | sort -nr | head`   |
| Filter status codes from JSON logs | `cat logs.json | jq '.[] | .status' | sort | uniq -c`                     |
| Clean up CSVs                      | `cat file.csv | awk -F',' '{print $1, $3}'`                               |

---

### Recon Stack

| Goal                       | Stack                                                                   |
|----------------------------|-------------------------------------------------------------------------|
| Subdomain check            | `amass enum -passive -d target.com | grep sub | awk '{print $1}'`      |
| Port scrape from nmap      | `nmap -oG scan.gnmap | grep open | awk '{print $2,$3,$4}'`             |
| Shodan recon + jq          | `curl -s 'https://api.shodan.io/host/1.2.3.4?key=KEY' | jq .data[]`    |

---

### 🛠 Format it Pretty

```bash
# Curl JSON & show user IDs
curl -s https://api.site.com/users | jq '.[] | {id: .id, email: .email}'

# Extract only HTTP links from HTML
curl -s https://target | grep -Eo 'http[s]?://[^"]+'
