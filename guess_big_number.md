# Challenge `Guess a BIG number` writeup

- Vulnerability: What type of vulnerability is being exploited
  - _Eg, SQL Injection, XSS, Endpoint is vulnerable to brute-force attack, etc_
- Where: Where is the vulnerability present
  - _Eg, `/guess/number` endpoint_
- Impact: What results of exploiting this vulnerability
  - _Eg, allows to find the server's guess by enumeration_
- NOTE: Any other observation

## Steps to reproduce

**1. reconnaissance **

My first step was to understand how should I try to guess a number with 100000 possibilities in order to get the flag. Therefore, I visited the provided link (http://mustard.stt.rnl.tecnico.ulisboa.pt:22052/).

	(SHOW IMAGE of http://mustard.stt.rnl.tecnico.ulisboa.pt:22052/)

Knowing that I should submit the number as `/number/<guess>` I did some tests with a few numbers.

	(SHOW IMAGE with tests higher and lower)

The result was an html page giving information about the target number. If the submitted number was smaller than the number we were trying to guess we would get a hint saying that the target number was "Higher". Otherwise, we would get an html page saying to go "Lower" than the number we submitted.



**2. Scripting**

Knowing the behavior of this challenge I did a small script that used the concept of a binary search. The idea was to reduce our interval as much as possible until we reach our target number.
For a better understanding, I started my search with an interval between 0 and 100000 and the respective midpoint which is 50000.
Then we would make a get request to `/number/<midpoint>` using the midpoint. If the html response was saying to go "Higher" then I knew that target number was between 50000 and 100000. If the html response was saying to go "Lower" then the interval was between 0 and 50000. After repeating this process a couple times, always dividing the interval in half I was able to retrieve the flag. 

[(POC)](`guess_big_number.py`)
