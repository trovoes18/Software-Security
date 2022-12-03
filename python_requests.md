# Challenge `Python requests` writeup

- Vulnerability: What type of vulnerability is being exploited
  - _Endpoint is vulnerable to brute-force attack_
- Where: Where is the vulnerability present
  - _`/more` and `/finish` endpoint_
- Impact: What results of exploiting this vulnerability
  - _Allows to find a number equal to server's target number by sending unlimited requests to server until getting the target number_

## Steps to reproduce

**1. reconnaissance**

My first step was to access the link to the challenge (http://mustard.stt.rnl.tecnico.ulisboa.pt:22053/) where the rules of this ctf were being listed.

> [![screenshot][1]][1]

  [1]: ./Images/python_requests_rules.jpg


Basically, I should ask for numbers using http://mustard.stt.rnl.tecnico.ulisboa.pt:22053/more until my current number was equal to my target number. Once that happened, I could access http://mustard.stt.rnl.tecnico.ulisboa.pt:22053/finish to retrieved the flag.

I played around with the challenge a bit to better understand the dynamics of the ctf. It was relatively easy to get the flag manually, however getting the flag through a script is more interesting and fun.

> [![screenshot][2]][2]

  [2]: ./Images/python_requests_merge.jpg

**2. Scripting**

To automate this processes I wrote a small python script using `requests` Python module. 
Initially, the script does a get request to http://mustard.stt.rnl.tecnico.ulisboa.pt:22053/ where I obtain the target number after processing the server response. Then, the script does multiple get requests to http://mustard.stt.rnl.tecnico.ulisboa.pt:22053/more where once again I obtain the current number after processing the server response to these requests. When the current number is equal to the target number a get request to http://mustard.stt.rnl.tecnico.ulisboa.pt:22053/finish is performed to obtain the flag.

After that, I run the python script and was able to retrieve the flag.

	`python python_requests.py`

> [![screenshot][3]][3]

  [3]: ./Images/python_requests_flag.jpg


[(POC)](`python_requests.py`)
