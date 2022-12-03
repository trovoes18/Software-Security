# Challenge `PwnTools Sockets` writeup

- Vulnerability: What type of vulnerability is being exploited
  - _Server is vulnerable to brute-force attack_
- Where: Where is the vulnerability present
  - _In the service running on the server_
- Impact: What results of exploiting this vulnerability
  - _Allows to find a number equal to server's target number by sending unlimited requests to server until getting the target number_

## Steps to reproduce

**1. reconnaissance**

In this challenge it was provided the code that the server was running and an `netcat` command to connect to the server.

From analysing the code, the goal was to obtain a `current` number equal to the `target` number. To ask for new numbers it was needed to provide the string `MORE`. Once the `current` number was equal to the `target` number it was necessary to provide the string `FINISH` to obtain the flag.

So, to start I connected to the server using the `netcat` command (`nc mustard.stt.rnl.tecnico.ulisboa.pt 22055`) to interact with it and have a better understanding of the execution flow. However, after being connected to the server I notice that there was a timeout with the command which means that I couldn't use `netcat` to find the flag because I didn't have the appropriate time to do it.
As the statement suggests one of the solutions was to use pwntools.


**2. Scripting**

To automate this processes I wrote a small python script using `pwn` Python module. 
Initially, the script connects to the server over a raw socket. Then, the target number is obtained by reading the bytes that are in the socket. After that, the string `MORE` is sent through the socket until the `current` number equals the `target` number. Once that happens, the string `FINISH` is sent over the socket and the flag is retrieved. 

After that, I run the python script and was able to obtain the flag.

	`python pwntools_sockets.py`



[(POC)](./Code/pwntools_sockets.py)
