---
layout: cheatsheet
title: "Regular Expressions"
---

## Regex Basics

| Pattern      | Meaning                                  |
|--------------|------------------------------------------|
| `.`          | Any character except newline              |
| `*`          | 0 or more of previous character           |
| `+`          | 1 or more of previous character           |
| `?`          | 0 or 1 of previous character              |
| `^`          | Start of line                             |
| `$`          | End of line                               |
| `\`          | Escape special character                  |

---

## Character Classes

| Pattern      | Matches                                     |
|--------------|---------------------------------------------|
| `[abc]`      | a, b, or c                                  |
| `[^abc]`     | Any character except a, b, or c             |
| `[a-z]`      | Any lowercase letter                        |
| `[A-Z]`      | Any uppercase letter                        |
| `[0-9]`      | Any digit                                   |
| `[a-zA-Z0-9_]` | Any letter, digit, or underscore          |
| `\d`         | Digit (`[0-9]`)                             |
| `\D`         | Non-digit                                   |
| `\w`         | Word character (`[a-zA-Z0-9_]`)             |
| `\W`         | Non-word character                          |
| `\s`         | Whitespace                                  |
| `\S`         | Non-whitespace                              |

---

## Quantifiers

| Pattern      | Meaning                                   |
|--------------|-------------------------------------------|
| `a*`         | 0 or more of `a`                          |
| `a+`         | 1 or more of `a`                          |
| `a?`         | 0 or 1 of `a`                             |
| `a{3}`       | Exactly 3 of `a`                          |
| `a{3,}`      | 3 or more of `a`                          |
| `a{3,5}`     | Between 3 and 5 of `a`                    |

---

## Grouping & Alternation

| Pattern         | Meaning                                 |
|-----------------|-----------------------------------------|
| `(abc)`         | Group `abc` as a single unit            |
| `(a|b)`         | Match either `a` or `b`                 |
| `(https?)`      | Match `http` or `https`                 |
| `(?:...)`       | Non-capturing group                     |

---

## Lookaheads / Lookbehinds (advanced)

| Pattern                        | Description                                 |
|--------------------------------|---------------------------------------------|
| `(?=foo)`                      | Positive lookahead for "foo"                |
| `(?!foo)`                      | Negative lookahead for "foo"                |
| `(?<=bar)`                     | Positive lookbehind for "bar"               |
| `(?<!bar)`                     | Negative lookbehind for "bar"               |

---

## Common Use Cases

| Task                         | Pattern                                            |
|------------------------------|----------------------------------------------------|
| Email                        | `[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}`   |
| IPv4                         | `\b\d{1,3}(\.\d{1,3}){3}\b`                        |
| URL                          | `https?://[^\s"]+`                                 |
| Hex color                    | `#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})`                |
| Password (min 8, 1 num)      | `^(?=.*\d).{8,}$`                                  |
| HTML tags                    | `<[^>]+>`                                          |
| File extension               | `\.\w{2,5}$`                                       |

---

## Tools That Use Regex

| Tool        | Notes                                              |
|-------------|----------------------------------------------------|
| `grep`      | POSIX regex, use `-E` for extended                 |
| `sed`       | Basic regex, needs escaping                        |
| `awk`       | Regex support in patterns (`/regex/`)              |
| `jq`        | Supports regex filters (`test`, `match`, `capture`)|
| `python`    | Full regex via `re` module                         |
| `burp`      | Supports Java-style regex                          |
| `VSCode`    | Built-in regex find/replace                        |

---
---
layout: cheatsheet
title: "Regex for Hackers"
---

## Exploit & Payload Patterns

| Task                          | Pattern                                               |
|-------------------------------|-------------------------------------------------------|
| Match common SQLi payloads    | `(?i)(union|select|insert|drop|or\s+1=1)`             |
| Match JS-based XSS payloads   | `<script[^>]*>.*?</script>`                           |
| Basic XSS tag detection       | `<[a-z]+.*?>`                                         |
| Match basic LFI attempts      | `\.\./\.\.`                                           |
| Match path traversal strings  | `(\.\./)+`                                            |
| PHP shell upload detection    | `(?i)(php.*base64_decode|shell_exec|eval)`            |
| Match encoded tags            | `%3C[^%]+%3E`                                         |
| Obfuscated alert() XSS        | `(?i)al.{0,2}ert\s*\(`                                |

---

## Recon & Enumeration

| Target                         | Pattern                                                |
|--------------------------------|--------------------------------------------------------|
| IP address                     | `\b(?:[0-9]{1,3}\.){3}[0-9]{1,3}\b`                    |
| Email addresses                | `[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}`       |
| Subdomains (basic)             | `\b([a-z0-9]+)\.example\.com\b`                        |
| URLs                           | `https?://[^\s"'<>]+`                                  |
| AWS keys (ID + secret)         | `AKIA[0-9A-Z]{16}` and `(?i)aws(.{0,20})?(secret|key)` |
| JWT token                      | `[A-Za-z0-9-_]+\.[A-Za-z0-9-_]+\.[A-Za-z0-9-_]+`       |

---

## Log Scraping

| Goal                              | Pattern                                                |
|-----------------------------------|--------------------------------------------------------|
| HTTP status codes                 | `"\s(200|301|404|500)\s`                               |
| User-agent strings                | `"User-Agent:\s.*?"`                                   |
| Authorization headers             | `Authorization:\s*(Bearer|Basic)\s+[^\s]`              |
| Cookie headers                    | `Cookie:\s[^;]+`                                       |
| Referrers                         | `Referer:\shttps?://[^"]+`                             |
| URL params (basic)                | `[\?&](\w+)=([^&#]+)`                                  |

---

## Chaining with Tools

| Stack Example                                                   | Purpose                         |
|-----------------------------------------------------------------|---------------------------------|
| `cat access.log \| grep -Eo '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+'`   | Extract IPs                     |
| `strings dump.bin \| grep -Ei 'apikey|secret|token'`            | Extract sensitive info          |
| `curl -s site \| grep -Eo '<a href="[^"]+"'`                    | Extract links from HTML         |
| `jq -r '.[] | select(.email | test("@")) | .email'`             | Extract email fields from JSON  |

---

## Red Team Signatures

| Task                               | Pattern                                               |
|------------------------------------|-------------------------------------------------------|
| Reverse shell IPs                  | `\b\d{1,3}(\.\d{1,3}){3}\b:\d{2,5}`                   |
| Bash one-liners                    | `bash -[cil]`                                         |
| Python reverse shell               | `python.*socket.*connect`                             |
| Powershell encoded command         | `powershell.*-enc`                                    |
| Base64 blobs over 100 chars        | `[A-Za-z0-9+/]{100,}={0,2}`                           |

---

## WAF Evasion Techniques

| Evasion Type               | Regex Pattern                                                |
|----------------------------|--------------------------------------------------------------|
| Basic obfuscated XSS       | `(?i)<[^>]*script[^>]*>`                                     |
| Tag-mutation XSS           | `(?i)<[^>]*on\w+\s*=`                                        |
| `javascript:` URI scheme   | `(?i)javascript\s*:`                                         |
| Bypass via whitespace      | `(?i)<\s*script\s*>`                                         |
| Bypass via comments        | `(?i)<\s*script\s*/?\s*.*?>`                                 |
| SQLi with inline comments  | `(?i)(union|select).+--`                                     |
| SQLi with case manipulation| `(?i)(s)(e)(l)(e)(c)(t)`                                     |
| Null byte injection        | `%00`                                                        |
| Hex-encoded payloads       | `%3[cC]` (matches encoded `<`)                               |
| Parameter pollution        | `(\w+=.*&)+\1` (repeating keys)                              |

---

## Phishing URL Red Flags

| Pattern Purpose              | Regex Pattern                                               |
|------------------------------|-------------------------------------------------------------|
| Suspicious TLDs              | `\.(tk|ml|ga|cf|gq)(\/|$)`                                  |
| Homoglyph abuse              | `[а-я]+\.com` (Cyrillic chars in `.com`)                    |
| Subdomain overload           | `(\w+\.){3,}\w+\.\w+`                                       |
| IP-based URLs                | `http[s]?:\/\/(?:\d{1,3}\.){3}\d{1,3}`                      |
| Misleading login path        | `login[^\/]*\/[^\/]*\.php`                                  |
| URL with too many params     | `\?.*(&.*){4,}`                                             |
| URL-encoded redirector       | `%2[fF]%2[fF]`                                              |
| URL contains `@`             | `http[s]?:\/\/[^\/]+@`                                      |

---

## Use Cases

| Tool      | Example Pattern Use                                         |
|-----------|-------------------------------------------------------------|
| Burp      | Custom match & replace rules to detect encoded exploits     |
| IDS/IPS   | Snort, Suricata regex-based signature triggers              |
| Web Proxy | Match & log suspicious params, redirects, encodings         |
| API Logs  | Detect endpoint misuse with obfuscated methods              |

---

## Auth & Identity Abuse

| Goal                           | Regex Pattern                                               |
|--------------------------------|-------------------------------------------------------------|
| Repeated failed logins         | `Failed password for.*from (\d{1,3}\.){3}\d{1,3}`           |
| User enumeration attempts      | `invalid user \w+ from`                                     |
| Suspicious user creation       | `useradd.*-u\s+[0-9]+`                                      |
| Logins from unknown geos       | `Accepted password for.*from (\d{1,3}\.){3}\d{1,3}`         |

---

## Malware & Exploits in Logs

| Goal                         | Regex Pattern                                              |
|------------------------------|------------------------------------------------------------|
| Shell command injection      | `(\||;|&&|wget|curl|nc|bash|python|perl)`                  |
| Base64 over logs             | `[A-Za-z0-9+/]{20,}={0,2}`                                 |
| Reverse shell patterns       | `bash.*\/dev\/tcp\/\d{1,3}(\.\d{1,3}){3}`                  |
| Suspicious encoded URL       | `(?i)%2[fF]%2[fF]`                                         |
| Inline script or eval abuse  | `(?i)(eval|new Function|setTimeout)\s*\(`                  |

---

## Web & API Abuse

| Goal                              | Regex Pattern                                              |
|-----------------------------------|------------------------------------------------------------|
| Directory brute force             | `GET \/.*(\/\.\.\/|\/\.git|\/wp-admin|\.env)`              |
| Path traversal                    | `\.\.\/`                                                   |
| Header injection                  | `(?i)\n(?:Set-Cookie|Location|Refresh):`                   |
| Repeated failed requests (DoS)    | `HTTP\/1\.[01]"\s(404|403|500)`                            |
| User-agent anomalies              | `User-Agent:\s*\S{0,5}` (empty or too short)               |

---

## Combine With Tools

| Tool                   | What to do                                             |
|------------------------|--------------------------------------------------------|
| Elastic/Kibana         | Apply these regex in field filters or scripted fields  |
| SIEMs (QRadar, Splunk) | Use in regex-based correlation rules                   |
| Logstash               | Apply regex via grok filters or mutate/conditional     |

---
# Burp Suite – Regex Payload Library
---

## XSS Detection

| Payload Type           | Regex Pattern                                  |
|------------------------|------------------------------------------------|
| Simple script tag      | `<script[^>]*>.*?</script>`                    |
| Event handlers         | `on\w+\s*=`                                    |
| Encoded XSS            | `%3Cscript%3E|&#x3C;script`                    |
| JS URI schemes         | `javascript\s*:`                               |
| Attribute injection    | `["'][\s]*on\w+\s*=`                           |

---

## SQLi Detection

| Payload Type           | Regex Pattern                                  |
|------------------------|------------------------------------------------|
| UNION SELECT           | `(?i)(union\s+select)`                         |
| Tautology bypass       | `(?i)(or\s+1=1|1=1--|')`                       |
| Encoded quotes         | `%27|%2D%2D`                                   |
| DB-specific patterns   | `information_schema|pg_.*|dual`                |

---

## RCE / Shells

| Payload Type           | Regex Pattern                                  |
|------------------------|------------------------------------------------|
| Bash injection         | `\|\s*(bash|sh|nc|curl|wget|python)`           |
| PHP evals              | `php.*(base64_decode|eval|system)`             |
| NodeJS evals           | `require\(|child_process`                      |

---

## Burp Use

- Paste into **Match & Replace**, **Content Discovery**, or **Intruder Payloads**
- Works great with **Grep Match** in **Scanner/Repeater**

---
# Regex – Cloud Log Detection"
---

## AWS CloudTrail

| Event Type             | Regex Pattern                                      |
|------------------------|----------------------------------------------------|
| Root login             | `"userIdentity":\s*{[^}]*"type":\s*"Root"`         |
| Console login attempt  | `"eventName":\s*"ConsoleLogin"`                    |
| IAM user creation      | `"eventName":\s*"CreateUser"`                      |
| API key usage          | `"accessKeyId":\s*".*?"`                           |

---

## GCP Audit Logs

| Event Type             | Regex Pattern                                      |
|------------------------|----------------------------------------------------|
| Service account use    | `"principalEmail":\s*".*?gserviceaccount.com"`     |
| SSH key creation       | `"methodName":\s*"compute.instances.setMetadata"`  |
| Unusual region access  | `"zone":\s*"us-central1-.*?"`                      |

---

## Azure Activity Logs

| Event Type             | Regex Pattern                                      |
|------------------------|----------------------------------------------------|
| Role assignment        | `"operationName":\s*"Add role assignment"`         |
| Identity misconfig     | `"authorization":\s*{[^}]*"action":\s*"Microsoft.Authorization"` |
| Unauthorized access    | `"status":\s*"Failed"`                             |


---
# Regex for CVE Signature Detection
---

## Python CVEs

| CVE ID             | Regex Pattern                                      |
|--------------------|-----------------------------------------------------|
| CVE-2023-24329 (urllib) | `(?i)(http|https):\/\/.*@.*`                   |
| CVE-2019-9636 (urllib path norm) | `(?i)(\.\./|%2e%2e\/)`             |

---

## Log4Shell (CVE-2021-44228)

| Target                   | Regex Pattern                                  |
|--------------------------|-------------------------------------------------|
| JNDI Lookup              | `\$\{jndi:[^\}]+\}`                            |
| Obfuscated variant       | `\$\{j[nN]d[iI]:(ldap|rmi|dns):.*?\}`         |

---

## Struts RCE / ShellShock / Heartbleed

| Exploit Type            | Regex Pattern                                  |
|-------------------------|-------------------------------------------------|
| Struts (OGNL)           | `%24{.*?}`                                     |
| ShellShock              | `()\s*{.*;.*}`                                  |
| Heartbleed              | `\x18\x03\x02\x00.*`                            |

---

## Use With

- IDS/IPS (Snort, Suricata)
- WAF Signature Rules
- SIEM Alerting
- Passive/inline network recon

---
# Regex – Email Filtering & Phishing Defense"
---

## Header Filtering

| Rule                         | Regex Pattern                                   |
|------------------------------|--------------------------------------------------|
| Spoofed sender               | `From:.*@(mail\.ru|outlook\.com)`              |
| Empty or forged From         | `From:\s*(\"\"|<>)`                             |
| Suspicious reply-to          | `Reply-To:.*@(protonmail|gmx|qq)\.com`         |

---

## Payload & Content Detection

| Type                         | Regex Pattern                                   |
|------------------------------|--------------------------------------------------|
| URL redirection              | `http[s]?:\/\/[^\/]+@`                          |
| Hidden iframe / tracking     | `<iframe[^>]*style=".*?display:\s*none`         |
| Login bait links             | `\/(signin|login|verify|update)\.php`          |
| Mismatched link text         | `<a[^>]+href="https?:\/\/(?!\1).*?">.*?</a>`    |

---

## Domain Abuse

| Detection                   | Regex Pattern                                   |
|-----------------------------|--------------------------------------------------|
| IP as domain                | `http[s]?:\/\/\d{1,3}(\.\d{1,3}){3}`            |
| Homoglyph domains           | `[а-яА-ЯёЁ]{2,}\.com` (Cyrillic .com)           |
| Misspelled brands           | `g00gle\.com|faceb00k\.com|paypa1\.com`         |

---

## Use in

- Mail server filters (Postfix, Exim)
- Email gateways (Proofpoint, Mimecast, MS Defender)
- SIEM alerts on mail logs
---

## Pro Tips

- **Escape backslashes**: `\\d` for digit in some shells
- **Group smart**: use `(?:...)` if you don’t need to capture
- **Anchor wisely**: `^` and `$` make regex faster and more accurate
- **Throttle your greed**: Use `{min,max}` quantifiers to avoid overmatching
- **Escape your dots**: `.` = anything — so escape it when you mean a literal
- **Group when needed**: `(?:...)` avoids capturing when you don’t need to
- **Precompile with tools**: Test in [regex101.com](https://regex101.com) or use `grep -P`, `awk`, `jq`, or `python re`
- Combine patterns with **thresholds**: 10+ matches in 5 minutes? Alert it.
- Log everything **before** parsing: Regex works best on raw log truth.
- Tag alerts with **contextual risk** (e.g., geo-IP, ASN, user-agent combo)
To avoid false positives:
- Anchor key terms (`^`, `$`)
- Use non-capturing groups: `(?:...)`
- Combine with **context** (e.g., path + payload, not just payload)
---


