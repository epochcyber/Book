# What is a Refelect cross-site scripting (xss)
It arises when an application receives data in an HTTP request and includes that data within the immediate response in an unsafe way

## How to find reflected XSS vulnerabilities
- Test every entry point 
- Submit random alphanumeric values at every entry point
- Determine each location where the random value is reflected 
- Test alternativate payload 
- Test the attack in browser if you succeed finding a payload 