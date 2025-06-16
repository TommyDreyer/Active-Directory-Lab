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

![2](https://github.com/user-attachments/assets/f3b62e59-67d6-4f1e-8c4a-a0b60bc87b91)

For this lab, I created a Windows Server 2022 Machine, an Ubunbtu server, a Windows 10 Machine (which the target machine), and Kali Linux (which is the attacker machine).

![1](https://github.com/user-attachments/assets/f475eae6-0c96-41d0-9237-6c8dacb50c4b)

Once I had all my virtual machines up and running, I created a NAT network called AD Project in Virtual Box and put all my machines on it so they can all communicate and talk to each other. 

![3](https://github.com/user-attachments/assets/f8c1c4df-ff47-4b69-baa2-ae47fdec59bb)

Once all my machines were on the same network, I gave each machine its own static IP address.

To verify the changes that have been made, I ran the ip a command and the ifconfig command on Windows and Kali respectively.

I also pinged google and my other machines to test connectivity.

My next objective was to download the tools I needed on each of my machines.

To download Splunk on my Ubuntu server, I first downloaded Splunk on my host machine.

![ss4](https://github.com/user-attachments/assets/ef1b60c8-5a4e-4b5f-82ba-825ae38ecfa7)

I then installed virtual box additional guest add ons on the Ubuntu server.

![ss5](https://github.com/user-attachments/assets/67510b07-9615-4ca7-abbd-8248dd284a3f)

I then created a shared folder on Virtulbox which contains the Ubuntu download file.

![ss3](https://github.com/user-attachments/assets/3fbcfab1-e984-4276-a378-4a65c0da44ea)

I then added the user to the vboxsf group.

![ss6](https://github.com/user-attachments/assets/82e7dbcb-0c71-4958-944c-2cb85fc90e84)

I then created a directory called share.

![ss7](https://github.com/user-attachments/assets/563a9ce5-675d-4ca6-8bd8-0b0c322fbfad)

I then mounted the shared folder to my newly created share directory.

![ss8](https://github.com/user-attachments/assets/c71e8701-83af-403b-8f56-b82973e95ea9)

I then changed into the user called splunk and then changed into a directory called bin so I can install Splunk on to my VM.

![ss9](https://github.com/user-attachments/assets/8cbd11b7-c9e9-410f-83a8-4e57cefe1571)

I then enabled the user to Splunk as the user Splunk every time the machine boots

![ss10](https://github.com/user-attachments/assets/3557819e-db77-494b-ba25-58263bddba46)

I then moved over to the my Windows Machine.

The first tool I installed was Splunk Universal Forwarder.

I then installed Sysmon.

After Sysmon was downloaded, I configured a file called inputs.conf to allow Splunk Universal Forwarder to forward Windows logs to my Ubuntu server.

I then stopped and restarted Splunk in the Service Manager.

I repeated these step in my Windows Server machine as well.

I then logged into Splunk and created an index called endpoint (which matched what is written in the inputs.conf file I configured earlier).

I then configured Splunk to read the data recieved my from Windows Machines.

In Splunk, when I click on hosts, I can see my two Windows Machines.

I then moved over to Windows Server machine where I installed Active Directory.

![ss2](https://github.com/user-attachments/assets/cc8bcde0-f9f2-4f32-b540-84229e0cae61)

I then promoted my server to a Domain Controller called tommy.local.

I then explored Active Directory and learned how to create users, groups and OU's (organizational units).

I created thee OUs and named them after different departments in a company to simulate a real world scenario: IT, Sales, and Marketing.

![ss3](https://github.com/user-attachments/assets/170d80b0-ebec-434e-b86d-45a5f403178b)

I created a user and a group for each OU.

I then added each user to their own respective groups.

![ss4](https://github.com/user-attachments/assets/2506731e-38c9-48b0-97e0-7a5cc382f52e)

![ss5](https://github.com/user-attachments/assets/9f8d2e1b-61c4-4d9b-add1-24af1f86f088)

I then moved on to the Windows 10 Machine to log in as one of the users I created.

I then logged into the user Billy Bob, with the username and password I created for this user.

![ss6](https://github.com/user-attachments/assets/1b9937eb-d744-4c9a-b4b3-8bb394418ea7)

Now that I had Active Directory set up, I can move over to my Kali Linux machine to perform a brute force attack.

I did plan on using a tool Crowbar, but I was not able to configure it correctly, so instead I used tool called Hydra.

Before I performed the attack, I unzipped a file called rockyou.txt that containes a list of passwords that can be used for a brute force attack.

However, it was long file and i didn't wanna use all of it, so I used the head command to condensed it to 20 lines.

I then edited the file, and added the passwords of the users I created, so the brute force attack could be performed correctly.

I then copied the password file to a directory I called AD Project. 

I then peformed my brute force attack. 

And it was successful.

![ss7](https://github.com/user-attachments/assets/f9c8426b-b105-42e7-850e-2d718fb826eb)

I then moved over to Splunk to see what telemetry was generarated.

When I was in Splunk, I saw there was 20 failed password attempts.

![ss8](https://github.com/user-attachments/assets/5392f028-ff0b-4ac4-a93d-2dbd8961bcf8)

![ss9](https://github.com/user-attachments/assets/1cdc5b76-fb29-4ec2-9953-f579c1abf52b)

As well as one successful login attempt, which is congruent with my passwords file.

![ss10](https://github.com/user-attachments/assets/666eed61-d454-4146-836a-68f2dc483838)

I then installed Atomic Red team to see what other kinds of telemetry I could generate.

![ss11](https://github.com/user-attachments/assets/928c9f81-333a-433f-a008-78edf381c1b2)

But before that, I set an exclusion for the entire C drive on my Windows 10 machine so Windows Defender doesn't remove any of the files from Atomic Read team.

![ss12](https://github.com/user-attachments/assets/095541a4-2efa-4f9e-968f-9a2e6183d8fe)

I then installed Atomic Red Team on my target machine.

![ss13](https://github.com/user-attachments/assets/ecab9348-1fd8-436e-99fe-8bf64003f45c)


I then learned that each of atomics in Atomic Red Team match the MITRE ATT&CK framework.

![ss15](https://github.com/user-attachments/assets/3a306ac8-7d76-4bbc-91b8-d538e5560dc9)

I then tested a few of the atomics in Powershell and then I checked Splunk to see what came up.

![ss16](https://github.com/user-attachments/assets/87dddfa5-2422-401e-af62-271f3636a3d2)


![ss17](https://github.com/user-attachments/assets/2aad6042-5327-4a4d-a598-41c997276e08)


## Conclusion

## Issues that I faced


## Notes
[notes.docx](https://github.com/user-attachments/files/20738369/notes.docx)

