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

I then moved over to the my Windows Machine.

The first tool I installed was Splunk Universal Forwarder.

I then installed Sysmon.

After Sysmon was downloaded, I configured a file called inputs.conf to allow Splunk Universal Forwarder to forward Windows logs to my Ubuntu server.

I then stopped and restarted Splunk in the Service Manager.

I repeated these step in my Windows Server machine as well.

I then logged into Splunk and created an index called endpoint (which matched what is written in the inputs.conf file I configured earlier)

I then configured Splunk to read the data recieved my from Windows Machines.

In Splunk, when I click on hosts, I can see my two Windows Machines.

I then moved over to Windows Server machine where I installed Active Directory.

I then promoted my server to a Domain Controller called tommy.local.

I then explored Active Directory and learned how to create users, groups and OU's (organizational units).

I created thee OUs and named them after different departments in a company to simulate a real world scenario: IT, Sales, and Marketing.

I created a user and a group for each OU

I then added each user to their own respective groups.

I then moved on to the Windows 10 Machine to log in as one of the users I created.

I then logged into the user Billy Bob, with the username and password I created for this user.

Now that I had Active Directory set up, I can move over to my Kali Linux machine to perform a brute force attack.

I did plan on using a tool Crowbar, but I was not able to configure it correctly, so instead I used tool called Hydra.

Before I performed the attack, I unzipped a file called rockyou.txt that containes a list of passwords that can be used for a brute force attack.

However, it was long file and i didn't wanna use all of it, so I used the head command to condensed it to 20 lines.

I then edited the file, and added the passwords of the users I created, so the brute force attack could be performed correctly.

I then copied the password file to a directory I called AD Project. 

I then peformed my brute force attack. 

And it was successful.

I then moved over to Splunk to see what telemetry was generarated.

When I was in Splunk, I saw there was 20 failed password attempts.

As well as one successful login attempt, which is congruent with my passwords file.

I then installed Atomic Red team to see what other kinds of telemetry I could generate.

But before that, I set an exclusion for the entire C drive on my Windows 10 machine so Windows Defender doesn't remove any of the files from Atomic Read team.

I then installed Atomic Red Team on my target machine.

I then learned that each of atomics in Atomic Team match the MITRE ATT&CK framework.

I then tested a few of the atomics and see what and then checked Splunk to see what came up.

## Conclusion

## Issues that I faced


## Notes
[notes.docx](https://github.com/user-attachments/files/20738369/notes.docx)

