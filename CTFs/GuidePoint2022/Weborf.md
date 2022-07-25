# Weborf Challenge  

A web based challenge based around the weborf webserver, designed to rapidly share directories.  

<br />

### 1. Run nmap to see whats what  

`sudo nmap -sV -p54043 10.10.100.200`  

The output wasn't super useful so I decided to investigate it via the web browser.

<br />

### 2. Web Investigating  

The webpage displayed a directory of files which seemed interesting and I immediately thought there maybe a way to do directory traversal.  

Looking through the files I noticed the weborf documents.  

<br />  

### 3. Googling for Weborf  

Googling around for weborf presenting a few things:  
* the repo on github
* some interesting things on exploit-db  

<br />

### 4. Download the project  

There was a weborf.zip file on the webpage so I decided to download rather than the github repo in case there were modifcations made to this version.  

I spun up the weborf server to see how it interacted with the system which was very similar to a simple python server. You could navigate the directory.

I tried a few different things in the url bar but nothing so I decided to look at the exploit-db findings and fire up burp suite.  

<br />

### 5. Burpsuite for the win (and exploit-db)  

I brought up burp suite and opened the internal browser, navigating to the weborf challenge site.  

I sent the request to repeater so I could attempt various different directory traversal methods.  

```
http://host/../../../../../etc/passwd
http://host/../../../../../etc/passwd%00
http://host/..%2f..%2f..%2f..%2f..%2f..%2f..%2fetc%2fpasswd
```

### 6. Bingo  

`/..%2f..%2f..%2f..%2f..%2f..%2f..%2fetc%2fpasswd`  

It was the format being sent. This was the correct way to send to request, get access to the /etc/passwd file, and find the flag.  