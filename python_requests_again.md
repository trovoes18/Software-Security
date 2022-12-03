# Challenge `Python requests Again` writeup

- Vulnerability: What type of vulnerability is being exploited
  - _Session Hijacking, Enumeration Attack_
- Where: Where is the vulnerability present
  - _In the client cookies_
- Impact: What results of exploiting this vulnerability
  - _Allows to impersonate an user inside an application by brute forcing the cookies or by simply changing some cookie values_

## Steps to reproduce

**1. reconnaissance** 

My first step was to access the link to the challenge (http://mustard.stt.rnl.tecnico.ulisboa.pt:22054/) where the rules of this ctf were being listed. 

> [![screenshot][1]][1]

  [1]: ./Images/python_requests_again_rules.jpg

According to the rules, I could only ask for numbers once using http://mustard.stt.rnl.tecnico.ulisboa.pt:22054/more. After that I had no more tries and the current number should be equal to the target number. The only thing left to do was accessing http://mustard.stt.rnl.tecnico.ulisboa.pt:22054/finish to obtain the flag. 

After knowing the rules, I tried to test this challenge with a few numbers. Despite of having only one try it seemed that the current number was always very distant from the target number as if they had their own limited range of values. 

> [![screenshot][2]][2]

  [2]: ./Images/python_requests_again_merge.jpg


I also notice that after closing the tab and opening another one in the same session the information about the challenge was persisting. Therefore, I tried to inspect the page looking for strange information and I found two interesting cookies. The first one was the `remaining_tries` cookie which inicially had the value `1` and it was most likely being used by the server to control the attempts of each user. The second was the `user` cookie which was a random number that identified the user in a each session.

> [![screenshot][3]][3]

  [3]: ./Images/python_requests_again_cookies.jpg

With this knowledge about the information used by the server I could send a request in which I set the cookies to an arbitrarily large number of attempts. So it would be a matter of time until the current number was equal to the target number.


**2. Scripting**

To automate this processes I wrote a small python script using `requests` Python module. 
Initially, the script does a get request to http://mustard.stt.rnl.tecnico.ulisboa.pt:22054/ where I obtain the target number after processing the server response. After that, I changed the `remaining_tries` cookie value to `1000`, which was enough by sending a get request to the server. Then, the script does multiple get requests to http://mustard.stt.rnl.tecnico.ulisboa.pt:22053/more where once again I obtain the current number after processing the server response to these requests. When the current number is equal to the target number a get request to http://mustard.stt.rnl.tecnico.ulisboa.pt:22054/finish is performed to obtain the flag.

After that, I run the python script and was able to retrieve the flag.

	`python python_requests_again.py`
	
> [![screenshot][4]][4]

  [4]: ./Images/python_requests_again_flag.jpg
