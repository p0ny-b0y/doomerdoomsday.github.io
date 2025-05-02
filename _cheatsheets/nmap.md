---
layout: cheatsheet
title: "Nmap"
---

## Basic Scans

| Command                          | Description                                  |
|----------------------------------|----------------------------------------------|
| `nmap [target]`                  | Basic scan (host discovery + port scan)      |
| `nmap -Pn [target]`              | Skip host discovery (assume host is up)      |
| `nmap -sn [target]`              | Ping scan only (host discovery, no ports)    |
| `nmap -p- [target]`              | Scan all 65535 ports                         |
| `nmap -F [target]`               | Fast scan (only top 100 ports)               |
| `nmap -iL targets.txt`           | Scan list of targets from file               |

---

## Service & Version Detection

| Command                          | Description                                  |
|----------------------------------|----------------------------------------------|
| `nmap -sV [target]`              | Probe open ports to determine service/version|
| `nmap -sV --version-all`         | Try harder to get accurate versions          |
| `nmap -A [target]`               | Aggressive scan: OS + version + scripts      |
| `nmap -O [target]`               | OS detection (TCP/IP fingerprinting)         |

---

## Port Specification

| Command                         | Description                                      |
|---------------------------------|--------------------------------------------------|
| `nmap -p 80 [target]`           | Scan port 80 only                                |
| `nmap -p 22,80,443 [target]`    | Scan specific ports                              |
| `nmap -p 1-1000 [target]`       | Scan port range                                  |
| `nmap -p U:53,161,T:21-25,80`   | Mixed UDP/TCP port scan                          |

---

## Speed & Stealth

| Command                            | Description                                      |
|------------------------------------|--------------------------------------------------|
| `nmap -T4 [target]`                | Speed up scan (1–5, 5 = insane, 4 = normal fast) |
| `nmap -sS [target]`                | Stealthy SYN scan (default, but explicit)        |
| `nmap -sT [target]`                | Full TCP connect (no SYN/ACK, loud)              |
| `nmap --max-retries 2`            | Reduce retries (stealthier, faster)              |
| `nmap --min-rate 1000`            | Set packets per second (faster)                  |

---

## Output Formats

| Command                                 | Description                          |
|-----------------------------------------|--------------------------------------|
| `nmap -oN output.txt [target]`          | Normal output                        |
| `nmap -oX output.xml [target]`          | XML output                           |
| `nmap -oG output.gnmap [target]`        | Grepable output                      |
| `nmap -oA myscan [target]`              | All formats: `.nmap`, `.xml`, `.gnmap`|

---

## Real-World Use Cases

| Goal                                  | Command                                                |
|---------------------------------------|--------------------------------------------------------|
| Internal scan (10.0.0.0/24)           | `nmap -sS -sV -O -T4 -oA internal 10.0.0.0/24`         |
| External hardened host (stealth)     | `nmap -Pn -sS -T2 -oA ext_host 1.2.3.4`                |
| Find live hosts                       | `nmap -sn 192.168.1.0/24`                             |
| Find open SMB shares                  | `nmap -p 445 --script=smb-enum-shares 10.0.0.5`        |
| Scan a list of IPs                    | `nmap -iL targets.txt -oA masscan`                    |

---
## Script Scanning (NSE)

| Command                                  | Description                                      |
|------------------------------------------|--------------------------------------------------|
| `nmap --script=default [target]`         | Run default script set                           |
| `nmap --script=vuln [target]`            | Run vulnerability check scripts                  |
| `nmap --script http-title [target]`      | Get HTTP titles (good recon)                     |
| `nmap --script-help [script]`            | See description of an NSE script                 |

---

## Script Power-Ups (NSE)

| Script Set                         | Usage Example                                       |
|------------------------------------|-----------------------------------------------------|
| `--script "http-*"`                | Run all HTTP-related scripts                        |
| `--script "ssl-*" -p 443`          | SSL/TLS enumeration on HTTPS                        |
| `--script "smb-enum-*,smb-vuln-*"` | SMB share, vuln checks on 445                       |
| `--script "ftp-*,telnet-*"`        | FTP/Telnet script enumeration                       |
| `--script "default,safe"`          | Default and safe script sets                        |
---

## Web App Scanning

| Command                                      | Description                              |
|----------------------------------------------|------------------------------------------|
| `nmap --script=http-title [target]`          | Get web page title                       |
| `nmap --script=http-enum [target]`           | Find common web dirs/files               |
| `nmap --script=http-headers [target]`        | Reveal server headers                    |
| `nmap --script=http-methods [target]`        | Allowed HTTP methods                     |
| `nmap --script=http-auth [target]`           | Probe for HTTP auth type                 |
| `nmap --script=http-vuln-* [target]`         | Web-specific vuln checks                 |

---
## NSE Script Paths

To list all available NSE scripts:
```bash
ls /usr/share/nmap/scripts/
