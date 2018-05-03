# A Beginners Guide to Computer Vulnerabilities

The primary purpose of this repo is to motivate new software developers to think about vulnerabilities that might be present in their programs and how to remediate these vulnerabilities. In school, assignments focus on functionality and thus most programmers overlook many vulnerabilities that can compromise sensitive information handled by their programs.


## What is a Computer Vulnerability?

There are numerous definitions by countless security organizations. I came up with a hybrid of all of them that I think it best defines what a computer vulnerability is:
>A **state of being exposed** to a possible attack, thus **reducing the information assurance** of the system.

## Classification of Computer Vulnerabilities

A vulnerability can arise in many different areas of a system. We will categorize our vulnerabilities using the BS ISO/IEC 27005:2008[<sup>[3]</sup>](https://github.com/alimomin95/infosec/blob/master/sources/BS%20ISO:IEC%2027005:2008%20-%20p42.pdf) standard. This standard categorizes vulnerabilities in general for an information technology organization and it encompasses all computer vulnerabilities.

The following is the categorization of vulnerabilities in an IT organization and the bold categories deal mainly with computer vulnerabilities:
 1. [**Hardware**](#hardware)
 2. [**Software**](#software)
 3. [**Network**](#network)
 4. Personnel
 5. Physical Site
 6. Organizational

We can see from above that these vulnerabilities arise in all three aspects of the PPT (People, Process, Technology) of an organization. Even though we will focus only on the technology aspect of these vulnerabilities, it is paramount for an organization to focus on all three to maximize the organization's information assurance.

## Hardware

Hardware consists of physical computer parts such as laptops, desktops, servers, printers, usb drives, external hard drives and etc.

Hardware vulnerabilities described in the BS ISO/IEC 27005:2008[<sup>[3]</sup>](https://github.com/alimomin95/infosec/blob/master/sources/BS%20ISO:IEC%2027005:2008%20-%20p42.pdf) standard are things such as exposing computer hardware to unsuitable conditions such as operating the device outside the rated temperature ranges or flood damaging the equipment or maybe theft. To prevent these vulnerabilities, a software developer can't do much and it becomes the job of a system administrator to make sure bad things don't happen to hardware.

There are some hardware vulnerabilities however that do require a software developer to be aware of when writing their programs. Just last year, two huge vulnerabilities, Meltdown and Spectre, were discovered in the computer chips manufactured in the last 20 years. These vulnerabilities were different from the usual software vulnerabilities because these were vulnerabilities in the computer hardware.

When you write your computer program and run it on an operating system, your program is not the only process running. Modern computers are heavy multitaskers and CPU manufacturers know that. This is why they develop microprocessors that can execute code that they think might be executed next. This is called speculative execution and it is done because processors nowadays are so fast that they are usually left waiting for data to move in and out of memory. If the processor guesses correct, it is a performance gain, and if not, the calculation done preemptively is thrown out. All the results of the speculative execution are stored on the cache for the CPU and can be accessed by any running application on the system. This breaks the isolation of execution between processes and a malicious process can peek into cache and see sensitive data (encryption keys, passwords, etc) of another process.

Researchers found that these vulnerabilities can be remediated in software but it degrades the CPU perfomance by up to 25% in some cases. There is no absolute way to remediate these vulnerabilities besides buying new hardware that has been manufactured differently to correct this issue.

## Software

Software consists of all programs contributing to the execution of an operation. This includes operating systems, service software, maintainance software, administration software, package software or standard software and business software.

There are an enormous amount of software vulnerabilities that are currently known. Apple's Secure Coding Guide does an excellent job categorizing and describing these vulnerabilities. They categorize software vulnerabilities as the following:
 1. [Buffer Overflows](#buffer_overflows)
 2. [Unvalidated Inputs](#unvalidated_inputs)
 3. [Race Conditions](#race_conditions)
 4. [Access-Control Problems](#access-control_problems)
 5. [Weakness in Authentication, Authorization, or Cryptographic Practices](#weakness_in_authentication,_authorization,_or_cryptographic_problems)

### Buffer Overflows

A buffer overflow occurs when a computer program, while writing to a buffer or memory space, overruns and writes data outside a buffer's boundary and changes data held in adjacent memory locations. Buffer overflow attacks usually occur because of malformed inputs or functions not checking input lengths.

To better understand how a buffer overflow attack works, we need to look at how a computer program is set up in the memory. See the figure below that shows the layout of a typical C program in memory. The stack region of the program's memory is used heavily to store local variables and return addresses of functions. A stack can only be accessed from the top using push and pop operations. Since variables for functions are stored on the stack along with return address, if the program copies content into the available buffer space allocated for a local variable and does not check the length of the data it is copying, it might overrun the available buffer space and write over the return address. This vulnerability can be used by an attacker by simply feeding the program a malicious string that overwrites the return address of the function to a program written by the attacker that can give him/her access to the system. This can become even worse if the vulnerable program runs with root or admin privileges because the attacker can spawn a shell with root or admin privileges. 

![alt text](https://he-s3.s3.amazonaws.com/media/uploads/383f472.png)

A big culprit that causes buffer overflows is the use of the function "strcpy()", which copies a null terminated character array into a specified buffer. To prevent buffer overflows, programmers should always check length of the input parameters before using them and also making use of "strlcpy()" over "strcpy()" can prevent most buffer overflow attacks.

Modern compilers have also gotten smarter. When compiling the program, they add canary words that are checked before a return and if that memory location is changed, the program can detect if memory was overwritten.

Check out this great [video](https://www.youtube.com/watch?v=1S0aBV-Waeo) on a buffer overflow attack.

### Unvalidated Inputs

Always check inputs to your program. Don't assume that the inputs will always be reasonable. This includes all sorts of input fields such as text input, commands passed through a URL used to launch the program, audio, video, or graphics files provided by users or other processes and read by the program, command line input, any data read from an untrusted server over a network and any untrusted data read from a trusted server over a network (user-submitted HTML or photos on a bulletin board, for example).

### Race Conditions

If your program requires a certain order of execution to function properly and it breaks if it is executed out of order, that is a race condition. An attacker can exploit this property of your program to gain access to sensitive or unauthorized data segments of memory.

To prevent race conditions, make use of proper method synchronizations and make your code fault tolerant.

### Access-Control Problems

There are many access control systems/mechanisms that are used when an application runs on a device. The operating system’s memory management system determines which parts of memory a program can access. Files on disk have permissions written to them telling the operating system to check before granting user access. Most of the time, problems in access control occur because the programmer doesn’t properly implement access control in their programs or they grant root permissions to the program. This creates a vulnerability because in case of a breach, the attacker can gain access to unauthorized sections of memory/files.

### Weakness in Authentication, Authorization, or Cryptographic Practices

Do you remeber the Firefox plugin called Firesheep?
Firesheep was a proof of concept plugin created by Eric Butler who showed a major weakness in online websites such Facebook, Flickr, Evernote, Amazon, Twitter and more. Most websites before 2010s used to only encrypt the users login session to authenticate the user and then once authenticated, the rest of the communication between the user and the servers was unencrypted and relied on IP address tied with cookies to keep the user logged in. This was not a big issue before WiFi was a commonplace and most computers were online through a hard wired connection but the rise of internet hotspots in Starbucks and McDonald's put most users at risk. Firesheep was essentially a packet sniffer that searched for unencrypted packets on a WiFi network and would allow the attacker to assume another person's identity who was on the network. Later all websites adopted the HTTPS protocol to fully encrypt all traffic from the user to ensure no information can be seen by simple packet sniffing. This was an important lesson for the tech community about the importance of Authentication, Authorization and using strong Cryptographic practices.

Let's start with Authentication. Authentication is the process where you determine that the user on the other end is actually who they say they are. This is usually done through a username and password login. For added security, 2FA (Two Factor Authentication) is used where a user logging into a new device is required to enter a security code that is sent to them via a text message or a phone call. A key thing to remember when you are developing a web application that allows user accounts is to use HTTPS. This is essential because without any encryption in place, the user's username and password are sent over the network in plain text allowing attackers with packet sniffers to have their way with this kind of information.

Have you been asked to enter your password again before making a purchase on Amazon or on the App Store? This is the Authorization step. Authorization is the process where you ask the user's permission to perform a certain task. When it comes to making/handling purchases, proper authorization to be in place is crucial. Apple used to have a big issue with having to refund users who claimed that their children purchased some apps on the App Store without their permission. Apple since then has gotten smarter and prompts users to enter their Apple password or authenticate with their fingerprint/face to authorize the purchase. When developing an application that can remember users logged in and keep them logged in, it becomes important to ask for authorization when performing certain tasks.

Finally, lets talk about Cryptography. This subject might seem difficult and a bunch of math theorems but I assure you, all you need to know is this, imagine two machines, one machine takes in an object and spits out something unrecognizable (garbage), the other machine can take in this "garbage" and transforms it back into that original object. Cryptography allows use to encrypt messages and send them over an open network without anyone seeing what the message says. There are many ways of encrypting data but as computers become more and more powerful, older methods of encryption become less secure and breakable. This is why it is crucial for developers to stay up to date with new developments in this area and be aware of what technologies have become obsolete. Check out a very good entry on Cryptography on OWASP[<sup>[17]</sup>](https://www.owasp.org/index.php/Guide_to_Cryptography).

![alt text](https://raw.githubusercontent.com/alimomin95/infosec/master/sources/man-in-the-middle-mitm.jpg)

Now that I have introduced encryption and cryptography, we can talk about Man-in-the-middle Attacks (MITM). I can try to explain MITM in a paragraph but I would suggest you'd rather go [here](https://www.youtube.com/watch?v=-enHfpHMBo4) for an excellent visual explaination of MITM Attacks. I assume you now know what MITM is and let's discuss how MITM can be mitigated. One way that was discussed in the video was using a Certificate Authority to validate public keys of the server you want to communicate with. This is done if your website forces users to HTTPS. This uses SSL to encrypt all traffic to your website using the certificate you registered with a Certificate Authority. Another way to keep your traffic encrpyted is to use a VPN. This will keep all your traffic encrpyted even if an attacker manages to get on your local network. 

## Network

Making sure an organization’s network is secure is just as important as securing an application that runs on the organization’s servers. The end goal is always to secure information. An attacker that can get into a network can cause just as much harm as an attacker exploiting an application’s vulnerability.

To ensure that your network is as strong and hard to penetrate, here are a few basic rules that must be followed:

#### RULE #1: Choose a Strong Password

To authenticate a user on a network, use a very strong password. Educate all users on the network to choose passwords that are virtually impregnable. Weak passwords that are about 7 or 8 characters in length can be [brute-force cracked](https://www.youtube.com/watch?v=7U-RbOKanYs) within a day with the current processing power at hand.

Checkout this [video](https://www.youtube.com/watch?v=3NjQ9b3pgIg) on how to choose a password.

#### RULE #2: Properly Configure Firewall Rules

“If it ain’t broke, why fix it” is not the right way to go about it when it comes to setting and configuring a network firewall. Networks are like a creature that morphs as time goes by. Some parts of the network get abandoned and forgotten but they still maintain high level access in the DMZ which attackers can use as an easy entry into an organizations information database.

Regular review of firewall rules and network analysis is crucial to maintain a secure network.

#### RULE #3: Update Devices/Endpoints

>A network is only as secure as it's weakest node

A network is made up of multiple devices/endpoints. It just takes one to be vulnerable to an attack to compromise the network.

It is important to apply patches and updates to all devices on the network to ensure network safety.

## Summary and Next Steps

This document should get you motivated to think about security when you write your computer programs. This guide is intended as a beginners guide to understanding and categorizing computer vulnerabilities. I suggest checking out further readings and sources I used below to write this guide to learn more in depth about computer vulnerabilities.

___
### References

[NIST - Risk Management Guide for Information Technology Systems](https://github.com/alimomin95/infosec/blob/master/sources/NIST%20-%20Information%20Security%20Guide%20for%20IT%20Systems.pdf)

[A Structured Approach to Classifying Security Vulnerabilities - Robert C. Seacord and Allen Householder](https://github.com/alimomin95/infosec/blob/master/sources/A%20Structured%20Approach%20to%20Identifying%20Vulnerabilities.pdf)

[BS ISO/IEC 27005:2008 - Information technology - Security techniques - Information security risk management](https://github.com/alimomin95/infosec/blob/master/sources/BS%20ISO:IEC%2027005:2008%20-%20p42.pdf)

[National Vulnerability Database](https://nvd.nist.gov/vuln/categories)

[OWASP Top 10 2013](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project#OWASP_Top_10_for_2013)

[Web Application Security Stats](http://projects.webappsec.org/w/page/13246989/Web-Application-Security-Statistics#APPENDIX2ADDITIONALVULNERABILITYCLASSIFICATION)

[Dumb Ideas in InfoSec](http://www.ranum.com/security/computer_security/editorials/dumb/)

[Apple Security Practices](https://developer.apple.com/library/content/documentation/Security/Conceptual/SecureCodingGuide/Articles/TypesSecVuln.html)

[The Top 5 Network Security Vulnerabilities](https://www.acunetix.com/blog/articles/the-top-5-network-security-vulnerabilities/)

[Vulnerabilities in Network Systems](http://searchsecurity.techtarget.com/tip/Vulnerabilities-in-network-systems)

[Meltdown and Spectre](https://www.theatlantic.com/technology/archive/2018/01/spectre-meltdown-cybersecurity/551147/)

[Buffer Overflow Attacks](http://www.cse.scu.edu/~tschwarz/coen152_05/Lectures/BufferOverflow.html)

[Buffer Overflow Attacks - Computerphile](https://www.youtube.com/watch?v=1S0aBV-Waeo)

[Validating Input and Interprocess Communication](https://developer.apple.com/library/content/documentation/Security/Conceptual/SecureCodingGuide/Articles/ValidatingInput.html)

[Race Conditions and Secure File Operations](https://developer.apple.com/library/content/documentation/Security/Conceptual/SecureCodingGuide/Articles/RaceConditions.html#//apple_ref/doc/uid/TP40002585-SW1)

[Broken Access Control](http://www.upenn.edu/computing/security/swat/SWAT_Top_Ten_A2.php)

[Firesheep](https://github.com/codebutler/firesheep)

[Guide to Crptography](https://www.owasp.org/index.php/Guide_to_Cryptography)

[Public-Private Key Cryptography - Computerphile](https://www.youtube.com/watch?v=GSIDS_lvRv4)

[Man-in-the-middle Attacks - Veracode](https://www.veracode.com/security/man-middle-attack)

[Man-in-the-middle Attacks - Hackerspace](https://hackerspace.kinja.com/how-to-defend-yourself-against-mitm-or-man-in-the-middl-1461796382)

[Man-in-the-middle Attacks - Computerphile](https://www.youtube.com/watch?v=-enHfpHMBo4)

[How to choose a password](https://www.youtube.com/watch?v=3NjQ9b3pgIg)
