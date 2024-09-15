# What is cross-site scripting (XSS)
Cross-Site Scripting (XSS) is a type of security vulnerability typically found in web applications. It allows attackers to inject malicious scripts into webpages viewed by other users. These scripts can then be executed in the context of the victim’s browser, leading to various potential security issues, such as data theft, session hijacking, or defacement of the website

## XSS proof of concept 
To confirm a cross-site scripting (XSS) vulnerability, we can use the print() function before we used the alert() function. However, starting from July 20, 2021, Chrome began preventing the alert() function from being called in certain contexts.

## Type of XSS attack
1. [Reflected xss](./Reflected/intro.md)
2. [stored XSS](./Store/intro.md)
3. [DOM-based XSS](./DOM/intro.md)

