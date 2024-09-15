# What is Stored XSS 
Stored cross-site scripting (also known as second-order or persistent XSS) arises when an application receives data an application receives data from an untrusted sources and includes that data within its later HTTP response in an unsafe way. 

## What is difference between stores xss and reflected
A stored XSS vulnerability enables attacks that are self-contained within the application itself. the attacker does not need to find an external way of inducing otyher user to a particular request containing their exploit . Rather the attacker place their exploit into the application itself and simply wait for user to encounter it. 

## How to find and test for stored xss Vulnerabilites 
we will check all "entry point" where we can enter the data and after we check all 'exist point" where that data might appear in the application's responses.

### Entry point into the application's processing includes
- Parameters or other data within the URL query string and message body.
- The URL file path.
- HTTP request headers that might not be exploitable in relation to reflected XSS.
- Any out-of-band routes via which an attacker can deliver data into the application. The routes that exist depend entirely on the functionality implemented by the application: a webmail application will process data received in emails; an application displaying a Twitter feed might process data contained in third-party tweets; and a news aggregator will include data originating on other web sites.
