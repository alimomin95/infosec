# A Beginners Guide to Computer Vulnerabilities

The primary purpose of this repo is to help new software developers who haven't been exposed to writing programs with a focus on information security. In school, assignments focus on functionality and thus most programmers overlook many vulnerabilities that can compromise sensitive information handled by their programs.


## What is a Computer Vulnerability?

There are numerous definitions by countless security organizations. I came up with a hybrid of all of them that I think it best defines what a computer vulnerability is:
>A **state of being exposed** to a possible attack, thus **reducing the information assurance** of the system.

## Classification of Computer Vulnerabilities

A vulnerability can arise in many different areas of a system. We will categorize our vulnerabilities using the BS ISO/IEC 27005:2008. This standard categorizes vulnerabilities in general for an information technology organization but it encompasses all computer vulnerabilities.

The following is the categorization of vulnerabilities in an IT organization and the bold categories deal mainly with computer vulnerabilities:
 1. [**Hardware**](#hardware)
 2. [**Software**](#software)
 3. [**Network**](#network)
 4. Personnel
 5. Physical Site
 6. Organizational

We can see from above that these vulnerabilities arise in all three aspects of the PPT (People, Process, Technology) of an organization. Even though we will focus only on the process and technology aspects of these vulnerabilities, it is paramount for an organization to focus on all three to maximize the organization's information assurance.

## Hardware

Hardware consists of physical computer parts such as laptops, desktops, servers, printers, usb drives, external hard drives and etc.

Hardware vulnerabilities described in the BS ISO/IEC 27005:2008 are things such as exposing computer hardware to unsuitable conditions such as operating the device outside the rated temperature ranges or flood damaging the equipment or maybe theft. These prevent these vulnerabilities, a software developer can't do much and it becomes the job of a system administrator to make sure bad things don't happen to hardware.

There are some hardware vulnerabilities however that do require a software developer to be aware of when writing their programs. Just last year, two huge vulnerabilities, Meltdown and Spectre, were discovered in the computer chips manufactured in the last 20 years. This vulnerability was different from the usual software vulnerabilities because this was a vulnerability in the computer hardware. Researchers found that these vulnerabilities can be worked around in software but it degraded the CPU perfomance by up to 25% in some cases. There is no absolute way to remediate these vulnerabilities besides buying new hardware that has been manufactured differently to correct this issue.

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

To better understand how a buffer overflow attack works, we need to look at how a computer program is set up in the memory. 

![alt text](https://he-s3.s3.amazonaws.com/media/uploads/383f472.png)

A big culprit that causes buffer overflows is the use of the function "strcpy()", which copies a null terminated character array into a specified buffer. To prevent buffer overflows, programmers should always check length of the input parameters before using them and also making use of "strlcpy()" over "strcpy()" can prevent most buffer overflow attacks.

Check out this great [video](https://www.youtube.com/watch?v=1S0aBV-Waeo) on a buffer overflow attack.

### Unvalidated Inputs

Always check inputs to your program. Don't assume that the inputs will always be reasonable. This includes all sorts of input fields such as text input, commands passed through a URL used to launch the program, audio, video, or graphics files provided by users or other processes and read by the program, command line input, any data read from an untrusted server over a network and any untrusted data read from a trusted server over a network (user-submitted HTML or photos on a bulletin board, for example).

### Race Conditions

If your program requires a certain order of execution to function properly and it breaks if it is executed out of order, that is a race condition. An attacker can exploit this property of your program to gain access to sensitive or unauthorized data segments of memory.

To prevent race conditions, make use of proper method synchronizations and make your code fault tolerant.

### Access-Control Problems

There are many access control systems/mechanisms that are used when an application runs on a device. The operating system’s memory management system determines which parts of memory a program can access. Files on disk have permissions written to them telling the operating system to check before granting user access. Most of the time, problems in access control occur because the programmer doesn’t properly implement access control in their programs or they grant root permissions to the program. This creates a vulnerability because in case of a breach, the attacker can gain access to unauthorized sections of memory/files.

### Weakness in Authentication, Authorization, or Cryptographic Practices

//Work in Progress

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

[Validating Input and Interprocess Communication](https://developer.apple.com/library/content/documentation/Security/Conceptual/SecureCodingGuide/Articles/ValidatingInput.html)

[Race Conditions and Secure File Operations](https://developer.apple.com/library/content/documentation/Security/Conceptual/SecureCodingGuide/Articles/RaceConditions.html#//apple_ref/doc/uid/TP40002585-SW1)

[Broken Access Control](http://www.upenn.edu/computing/security/swat/SWAT_Top_Ten_A2.php)
