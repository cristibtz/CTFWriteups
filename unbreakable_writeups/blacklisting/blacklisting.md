# Blacklisting
## Description: I think my blacklist is going to prevent any vulnerability!
### We are given the code of a PHP app. There is a filter which we need to bypass and execute some command to get the flag.
<p align="center"> 
  <img src="photo1.png" alt="Material Bread logo">
</p>

### The strpos function verifies if we have space in our input. Also we need to escape from the find command. We can do that by appending ‘;’. So, until now we can run one word commands, like:
<p align="center">http://34.107.71.117:30302/?start&secrets=;ls;</p>

<p align="center"> 
  <img src="photo3.png" alt="Material Bread logo">
</p>

### Knowing space is not allowed, we should try something else instead of it. After some research, I found this link: 
<p align="center">https://unix.stackexchange.com/questions/351331/how-to-send-a-command-with-arguments-without-spaces</p>

### from which we can find that ${IFS} can be used instead of space. We try this:
<p align="center">http://34.107.71.117:30302/?start&secrets=;cat{$IFS}secrets.php;</p>

### And we got the flag!!!!!
<p align="center"> 
  <img src="photo2.png" alt="Material Bread logo">
</p>
