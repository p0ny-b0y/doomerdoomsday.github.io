---
layout: cheatsheet
title: "Injection"
---

## Command Injection 

Explained:
: Exploits vulnerabilities in programs that allow the execution of external commands on the server.

### Ways of injecting OS Commands (Windows and Unix):
- &
- &&
- pipe (|)
- double pipe (||)

### Ways of injecting OS Commands (Unix):
- ;
- newline (0x0a or \n)
- `
- $(


### Commands to try

| Purpose               | Linux                 | Windows        |
|-----------------------|-----------------------|----------------|
| Name of current user  | whoami                | whoami         |
| Operating System      | uname -a              | ver            |
| Network configuration | ifconfig              | ipconfig /all  |
| Network connections   | netstat -an           | netstat -an    |
| Running processes     | ps -ef                | tasklist       |


### Resources
[OWASP](https://owasp.org/www-community/attacks/Command_Injection)
[HACKTRICKS](https://book.hacktricks.xyz/pentesting-web/command-injection)
[PORTSWIGGER](https://portswigger.net/web-security/os-command-injection)
[OSCP NOTES](https://gabb4r.gitbook.io/oscp-notes/cheatsheet/command-injection-cheatsheet)


## LDAP Injection

Explained:
: Apps may pass authentication queries for data into back-end LDAP systems. Important to note LDAP Filters constructed from key-value pairs. 


| Symbol | Description |
| ---- | ---- |
| * | Wildcard |
| Logical AND | & |
| Logical OR | \| |
| Approximately  | ~= |
| Greater than | >= |

Example:
```
http://website/ldapsearch?user= *)(uid= * ))(|uid= *)
```

## Resources:
[OWASP](https://cheatsheetseries.owasp.org/cheatsheets/LDAP_Injection_Prevention_Cheat_Sheet.html)

## SQLi
Explained:
: Enables attackers to manipulate a website's database by inserting malicious SQL queries throughout input fields, potentially leading to unauthorized access, data leakage, or database manipulation

### How to Test
- When is the app interacting with a DB server
	- Authentication forms
	- Search engines
	- E-Commerce sites and their product descriptions
- Input fields, including the hidden fields of POST requests
- Consider also HTTP headers and Cookies

| Command | Purpose |
| ---- | ---- |
| SHOW tables; | List tables in database |
| DESC table name; | Describe field values in table |
| SELECT column From table; | Select field from table |
| INSERT INTO table name (col1, col2) VALUES (val1, val2); | Insert a new record |
| DELETE database name | Delete a DB |

### Error-based SQLi
- Intentionally triggering an error in the database query to extract information from the error messages returned by the server
- This allows the attacker to gather valuable information about the database structure
### Blind SQLi
- Attacker sends a crafter SQL query to the server but no feedback is received
- Instead, observe the differences in the application's response to determine if the query was successful
- Boolean-based SQLi
	- Ask the database true or false questions, such as (id =1 AND 1=1) or (id=1 AND 1=2)
- Time-based SQLi
	- Can you get the database to pause?
	- http://example.com/test.php?id=1 and sleep(5)-- 
- Can you conduct a linear search?
- Can you conduct a binary search?

### Union Query SQL Injection
- The UNION keyword combines the results of their injected query with the original query
- http://example.com/search?keyword=iphone' UNION SELECT username, password FROM users --

### Resources
[SQL WORKBENCH](www.sql-workbench.net/dbms_comparison.html)
[HACKTRICKS](https://book.hacktricks.xyz/pentesting-web/sql-injection)

## XSS

Explained:
: Attackers can inject client-side scripts or HTML code into web pages to steal information or bypass authentication. This occurs because of a lack of inspection on the server side. 

### What to Look For
- Input fields users can enter text
	- search bars, contact forms, login forms, user profile, chat systems
- URL parameters
- Cookies
- File upload forms
- Is it encoded? URL or base64?
### XSS Types
- Reflected: Injection is reflected back to the user's browser. I.E. a pop up box from a script alert
- Stored: Injection is permanently stored on the server and executes when other users view that page
- DOM-based: Modifies DOM in browser. Unliked the other two, this injection occurs on the client side. Can occur if user-controlled data is used to update the DOM directly.

### Resources
[OWASP FILTER EVASION](https://owasp.org/www-community/xss-filtter-evasion-cheatsheet)
[HACKTRICKS XSS](https://book.hacktricks.xyz/pentesting-web/xss-cross-site-scripting)
[HACKTRICKS DOM XSS](https://book.hacktricks.xyz/pentesting-web/xss-cross-site-scripting/dom-xss)
