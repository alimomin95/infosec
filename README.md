# A Beginners Guide to Computer Vulnerabilities

The primary purpose of this repo is to help new software developers who haven't been exposed to writing programs with a focus on informatio security. In school, we are given assignments that focus on functionality and thus most programmers overlook many vulnerabilities that can compromise sensitive information handled by their program.


## What is a Computer Vulnerability?

There are numerous definitions by countless security organizations. I came up with a hybrid of all of them that I think it best defines what a computer vulnerability is:
>A **state of being exposed** to a possible attack, thus **reducing the information assurance** of the system.

## Classification of Computer Vulnerabilities

A vulnerability can arise in many different areas of a system. We will categorize our vulnerabilities using the BS ISO/IEC 27005:2008. This standard categorizes vulnerabilities in general for an information technology organization but it encompasses all computer vulnerabilities.

The following is the categorization of vulnerabilities in an IT organization and the bold categories deal mainly with computer vulnerabilities:
 1. [**Hardware**](#hardware)
 2. [**Software**](#software)
 3. **Network**
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
 1. Buffer Overflows
 2. Unvalidated Inputs
 3. Race Conditions
 4. Access-Control Problems
 5. Weakness in Authentication, Authorization, or Cryptographic Practices
