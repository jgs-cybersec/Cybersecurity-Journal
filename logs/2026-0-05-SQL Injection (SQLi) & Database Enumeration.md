## The Scenario

At 11:15 AM, the Web Application Firewall (WAF) triggers a high-severity alert on your primary public-facing portal:

`ALERT: Potential SQL Injection (SQLi) and Database Schema Probing detected from external source.`

## Goal

Analyze the raw Nginx /var/log/nginx/access.log entries below, identify the attacker's progression, evaluate the server's responses, and determine if database data was successfully compromised.

## The Raw /var/log/nginx/access.log Snippet

Note: In web server logs, each line represents a single HTTP request, containing: 

`Source_IP - - [Timestamp] "Method Path Protocol" Status_Code Bytes_Sent "User_Agent"`.

`203.0.113.110 - - [05/Jul/2026:11:10:02 +0000] "GET /items.php?id=105 HTTP/1.1" 200 1420 "Mozilla/5.0"
203.0.113.110 - - [05/Jul/2026:11:10:15 +0000] "GET /items.php?id=105' HTTP/1.1" 500 234 "Mozilla/5.0"
203.0.113.110 - - [05/Jul/2026:11:11:04 +0000] "GET /items.php?id=105%20AND%201=1 HTTP/1.1" 200 1420 "Mozilla/5.0"
203.0.113.110 - - [05/Jul/2026:11:11:22 +0000] "GET /items.php?id=105%20AND%201=2 HTTP/1.1" 200 452 "Mozilla/5.0"
203.0.113.110 - - [05/Jul/2026:11:12:45 +0000] "GET /items.php?id=105%20UNION%20SELECT%20null,username,password%20FROM%20users HTTP/1.1" 200 3512 "Mozilla/5.0"
203.0.113.110 - - [05/Jul/2026:11:14:10 +0000] "GET /items.php?id=105%20UNION%20SELECT%20null,null,null%20FROM%20admin_credentials HTTP/1.1" 404 180 "Mozilla/5.0"`

## Analyst Answer

**1. The Targeted Parameter**: The parameter is **id inside /items.php**.

**2. The Vulnerability Indicator**: At 11:10:15, injecting the `'` symbol resulted in an** HTTP 500 (Internal Server Error)**. This indicates that the database interpreter tried to compile the unescaped quotation mark, broke, and returned a database syntax error rather than handling the input cleanly.

**3. The Exploitation Technique**: **A UNION-Based SQL Injection**. The attacker attempted to append a secondary command using `UNION SELECT` to merge the application's legitimate results with administrative tables.

**4. Success vs. Failure**:

The database dump attempt for the users table returned an **HTTP 200 (OK)** status code with a significantly **larger response size (3512 bytes vs. the standard 1420 bytes)**, confirming that **user credentials were successfully dumped and displayed on the web page**.

The admin_credentials attempt returned an **HTTP 404 (Not Found)** because that table name likely does not exist in the database schema.

**5. Troubleshooting Command**:

To quickly isolate attacking IPs targeting that specific script on a live Linux server, you can parse the raw Nginx access log using standard piping commands:

`cat /var/log/nginx/access.log | grep "items.php" | awk '{print $1}' | sort -u`

**Explanation of the command:**

The Pipe symbol `|` Passes the output of the command on its left directly to the command on its right.

`grep "items.php"` takes that raw log stream and filters it, keeping only the lines that contain the word items.php (our targeted script).

`awk '{print $1}'`

`awk` is a powerful text processing tool. By default, it splits lines of text into columns based on spaces. {print $1} tells it to extract and display only Column 1.(in this log format `Source_IP - - [Timestamp] "Method Path Protocol" Status_Code Bytes_Sent "User_Agent`"

`sort -u`
`* sort` organizes the IP addresses in order.`-u` stands for unique. If an IP address appears 50 times in the logs, it filters out all the duplicates and prints it only once.

## The Exact Output

`203.0.113.110`

Because every single attempt to exploit the web server came from this single, malicious external address, sort -u consolidated all those requests into one single IP.

If there were other hackers or legitimate users visiting that page, you might see an output like this:

`192.168.1.12      <-- A local IT admin testing the site
203.0.113.110     <-- The attacker
220.14.32.99      <-- Another external user`




