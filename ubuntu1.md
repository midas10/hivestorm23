# Hivestorm 2023 Ubuntu#1 Image

A quick disclaimer before I complete this "writeup". My team did finish in the top 25%, but I left a good portion of security vulnerabilities on my image. Therefore, if you're looking for a complete writeup from someone that got close to 100% of the vulnerabilities, this is not for you. To be honest this is more for me than any outside audience but I figured I'd make it public anyway in case anyone wanted it.

## *Basic Security Checks*
- Set up a firewall using the following commands: 
```sh
sudo apt install ufw
sudo enable ufw
```
- Then to knock out a few more easy points, compare the users list to the readme and delete any unauthrorized users:
```sh
awk -F':' '{print $1}' /etc/passwd
sudo userdel -r $user
```
- Similarly, check all sudo users and delete any that are not listed as authorized admins:
```sh
getent group sudo
sudo deluser $user sudo
```
- Continue through the linux checklist found below and follow the instructions. The steps above were how I got the majority of my points. Unfortunately a lot of the other steps listed on the checklist got no points, including changing passwords. However, again, I missed a lot of vulnerabilities on my machine so I may have configured something wrong or missed a step.
[Forty-Bot's Linux Checklist](https://github.com/Forty-Bot/linux-checklist)

## *Forensic Question #1*
The first forensic question asks you to find a Ruby backdoor hidden somewhere on the machine. However, the process title changes each time the backdoor's activated so you must use a standard tool to figure this one out.

To solve this question, first I used ps to list all processes and found the PID of "ruby".
```sh
sudo ps -a
```
Then, once I had the Process ID, I had to use ps again but now to find the process title using -p and -o.
```sh
ps -p $pid -o command
```
This returned the name of the process title and therefore the answer to the question.

## *Conclusion*
I doubt anyone finds this writeup but if you do sorry it's kind of mid. I mostly wanted to get this down on my Github before I forgot what I even did. Honestly probably already forgot half of what I did. Thanks to everyone that competed, it was fun, and looking forward to the next Hivestorm.
