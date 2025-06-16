# Active Directory Lab

## Objective

The goal of this project is to create a virtual lab environment that has a Ubuntu server hosting splunk, a Windows Server 2022 machine that has Active Directory and is a Domain Controller, as well as a Windows 10 machine acting as the target machine and Kali Linux acting as the attacking machine. From there, my objective was to see what I could do to generate telemetry that can then be viewed on Splunk.

## Network Diagram
![Network Diagram](https://github.com/user-attachments/assets/05890264-289a-4bee-aedc-ae67b85a7612)

### Key Skills Learned

- IT Administration by creating users, groups and OU's in Active Directory.
- Basic Penetration Testing by performing brute force attacks on Kali Linux.
- Utilizing SIEMs (Splunk) for analyzing logs.
- Became familiar with the MITRE ATT&CK framework by utilizing Atomic Red Team.
- Gained more experienced with Linux Terminal and Windows Powershell.

### Tools Used

- Splunk for log ingestion and analyzing the telemetry generated.
- Active Directory for creating users, groups, and OU's.
- Hydra for performing brute force attacks on Target Machine.
- Atomic Red Team for using the MITRE ATT&CK framwework to generate additional Telemetry that could be analyzed on Splunk.

## Steps

The first step was to create the virtual machines I would be using in this lab. I already had Virtual Box on my host machine so I downloaded the iso files I needed. 

For this lab, I created a Windows Server 2022 Machine, an Ubunbtu server, a Windows 10 Machine (which the target machine), and Kali Linux (which is the attacker machine).

Once I had all my virtual machines up and running, I created a NAT network called AD Project in Virtual Box and put all my machines on it so they can all communicate and talk to each other. 

Once all my machines were on the same network, I gave each machine its own static IP address.

To verify the changes that have been made, I ran the ip a command and the ifconfig command on Windows and Kali respectively.

I also ping google and my other machines to test connectivity

My next objective was to download the tools I needed on each of my machines.

To download Splunk on my Ubuntu server, I first downloaded Splunk on my host machine.

I then installed virtual box additional guest add ons on the Ubuntu server.

I then created a shared folder on Virtulbox which contains the Ubuntu download file.

I then added the user to the vboxsf group.

I then created a directory called share.

I then mounted the shared folder to my newly created share directory.

I then changed into the user called splunk and then changed into a directory called bin so I can install Splunk on to my VM.

I then enabled the user to Splunk as the user Splunk every time the machine boots

I then moved over to the my Windows









## Issues that I faced


## Notes
[notes.docx](https://github.com/user-attachments/files/20738369/notes.docx)

