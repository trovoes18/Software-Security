# Challenge `Secure by Design` writeup

- Vulnerability: What type of vulnerability is being exploited
  - _Session Hijacking, Enumeration Attack_
- Where: Where is the vulnerability present
  - _In the client cookies_
- Impact: What results of exploiting this vulnerability
  - _Allows to impersonate an user inside an application by brute forcing the cookies or by simply changing some cookie values_

## Steps to reproduce

**1. reconnaissance**

My first step was to access the link to the challenge (http://mustard.stt.rnl.tecnico.ulisboa.pt:22056/).  
In this html page I was prompted to enter my nickname. 
At this point, I tried some common usernames like `adminstrator` or `admin` but nothing really worked. For non-admin users the web page showed a message saying it was under construction.
An interesting fact is that the website could detect that the `admin` user was fake because the response web page showed the message 
`Welcome back fake-admin.
Unfortunately our page is still under construction for non-admin users.`  
Another interesting detail I found was that when the user was `admin` the server did not return the original base64 encoding which is `YWRtaW4K`, but another value.

I also notice that after closing the tab and opening another one in the same session the information about the challenge was persisting.
Then I inspected the page and found the `user` cookies that the server was using. The value of this cookie was encoded in base64.

Basically, every time someone entered their username a POST request was performed and the server was responsible for encoding the username in base64 and returning the cookie to the client. Then, a GET request to the server was performed using the cookies that the server have sent previously.  

Knowing this I could exploit this vulnerability to find an admin user.

**2. Scripting**

To explore this vulnerability I wrote a small python script using `requests` Python module. This script iterates through a list of common username that are encoded using base64. It then sets a cookie dictionary value to the encoded username and finally makes the request to the server using these cookies. 

After that, I run the python script and was able to retrieve the flag and the respective admin user in a few seconds.

	`python secure_by_design.py`


[(POC)](./Code/secure_by_design.py)
