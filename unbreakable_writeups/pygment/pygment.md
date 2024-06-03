# Pygment
## Description: I managed to obtain the affected source code and make a small POC. There is no issue with it. Can you check it?
### This challenge begins with an error message outputted on the screen
### ![alt text](photo1.jpg)
Error is: 
Warning: Undefined array key "a" in /var/www/html/index.php on line 77 Warning: Undefined array key "b" in /var/www/html/index.php on line 77 Fatal error: Uncaught RuntimeException: sh: 1: pygmentize: not found in /var/www/html/index.php:63 Stack trace: #0 /var/www/html/index.php(77): Pygmentize::highlight(NULL, NULL) #1 {main} thrown in /var/www/html/index.php on line 63
We can understand the a, b are tried to be used and they aren’t defined. I try to add them in the url as GET parameters

### After adding them to the url, the error changes:
Fatal error: Uncaught RuntimeException: sh: 1: pygmentize: not found in /var/www/html/index.php:63 Stack trace: #0 /var/www/html/index.php(77): Pygmentize::highlight('x', 'x') #1 {main} thrown in /var/www/html/index.php on line 63
We can see that the values we give to a and b are passed into a function.
Given the challenge name and info collected from errors, I started to do some research.
I stumbled upon the Github page of the app that is used in this challenge: 
https://github.com/dedalozzo/pygmentize/
Searching more on the Github page, I understand that this app had an RCE vulnerability in a previous version of it.
In order to figure out the version of the Pygmentize app used in this CTF, I try to access the composer.lock file
http://challenge_IP:PORT/composer.lock
I see version 1.0 is being used.
### ![alt text](photo2.jpg)
### From now, we can definitely exploit the RCE vulnerability and get the flag.




### Looking more through the Github page, I found someone’s POC: https://github.com/dedalozzo/pygmentize/issues/1 
### ![alt text](photo3.jpg)
### Knowing this, I start to build my payload to insert in the variables a and b. After many tries, this payload reveals the flag:
http://34.107.71.117:31907/?a=x&b=;cat%20flag.php|| 
### It was a very interesting challenge which required some research to understand how the app is built in order to exploit this vulnerability.
### ![alt text](photo4.jpg)
