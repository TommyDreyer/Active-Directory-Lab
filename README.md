# Active Directory Lab

## Objective

The objective of this project was to create a virtual lab environment simulating a real-world enterprise network. The lab consists of:

 - A Ubuntu server hosting Splunk for log analysis
 - A Windows Server 2022 machine configured with Active Directory as a Domain Controller
 - A Windows 10 machine serving as the target endpoint
 - A Kali Linux machine acting as the attacker system

The main goal was to generate and observe telemetry data from various attack techniques, which could then be collected and analyzed in Splunk.

## Network Diagram
![Network Diagram](https://github.com/user-attachments/assets/05890264-289a-4bee-aedc-ae67b85a7612)

### Key Skills Learned

- Practiced IT administration by creating users, groups, and organizational units (OUs) in Active Directory.
- Performed basic penetration testing using brute-force techniques on Kali Linux.
- Analyzed security logs and telemetry using Splunk as a SIEM platform.
- Applied the MITRE ATT&CK framework in a hands-on environment using Atomic Red Team.
- Gained experience with both the Linux terminal and Windows PowerShell for administrative and offensive tasks..

### Tools Used

- Splunk – For ingesting and analyzing telemetry data from various sources.
- Active Directory – For user, group, and OU management in a centralized domain environment.
- Hydra – To perform brute-force attacks against login services on the target machine.
- Atomic Red Team – To simulate adversary behavior aligned with the MITRE ATT&CK framework and generate relevant telemetry for analysis.

## Steps

The first step was to create the virtual machines I would be using in this lab. I already had Virtual Box on my host machine so I downloaded the iso files I needed.

![2](https://github.com/user-attachments/assets/f3b62e59-67d6-4f1e-8c4a-a0b60bc87b91)

For this lab, I created a Windows Server 2022 Machine, an Ubunbtu server, a Windows 10 Machine (which the target machine), and Kali Linux (which is the attacker machine).

![1](https://github.com/user-attachments/assets/f475eae6-0c96-41d0-9237-6c8dacb50c4b)

Once I had all my virtual machines up and running, I created a NAT network called AD Project in Virtual Box and put all my machines on it so they can all communicate and talk to each other. 

![3](https://github.com/user-attachments/assets/f8c1c4df-ff47-4b69-baa2-ae47fdec59bb)

Once all my machines were on the same network, I gave each machine its own static IP address.

Windows 10:

![4](https://github.com/user-attachments/assets/8c5e22aa-0d32-41fe-999b-485bbda6b544)

Windows Server: 

![6](https://github.com/user-attachments/assets/f3d5cfdd-cb92-4deb-9c27-2c0a15cc3627)

Kali Linux:

![7](https://github.com/user-attachments/assets/e9755dc3-7639-444b-a266-9146e07d4971)

Ubuntu Server:

![9](https://github.com/user-attachments/assets/51c6285d-c365-4e36-9b9d-27635da8b9fa)

To verify the changes that have been made, I ran the ip a command and the ifconfig command on Windows and Kali respectively.

![5](https://github.com/user-attachments/assets/978a1784-fa70-467c-9714-ab05561862bc)

![8](https://github.com/user-attachments/assets/6f493fde-1250-476b-9b85-8db64eb6fc69)

I also pinged google and my other machines to test connectivity.

![ss16](https://github.com/user-attachments/assets/107efb94-ac21-4ca2-b915-3cac76c7d950)

![ss17](https://github.com/user-attachments/assets/c9c71df5-d1fb-40e4-bdba-b81e7981de8c)

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

I then enabled Splunk to be the user every time the machine boots.

![ss10](https://github.com/user-attachments/assets/3557819e-db77-494b-ba25-58263bddba46)

I then moved over to the my Windows Machine.

The first tool I installed was Splunk Universal Forwarder.

![ss11](https://github.com/user-attachments/assets/16d428e4-065a-4503-b307-c3e8546cf9bf)

I then installed Sysmon.

![ss12](https://github.com/user-attachments/assets/f4bd2743-9135-4093-8e62-50294882c221)

After Sysmon was downloaded, I configured a file called inputs.conf to allow Splunk Universal Forwarder to forward Windows logs to my Ubuntu server.

![ss13](https://github.com/user-attachments/assets/0f35474b-ecb8-4a88-91a6-451dac808912)

I then stopped and restarted Splunk in the Service Manager.

![ss14](https://github.com/user-attachments/assets/0a7e162d-bde2-4c78-bdbf-d23197c488ae)

I repeated these step in my Windows Server machine as well.

I then logged into Splunk and created an index called endpoint (which matched what is written in the inputs.conf file I configured earlier).

![ss15](https://github.com/user-attachments/assets/c6065ca5-efe3-4678-9737-cd51e20cff1f)

I then configured Splunk to read the data recieved my from Windows Machines.

In Splunk, when I click on hosts, I can see my two Windows Machines.

![10](https://github.com/user-attachments/assets/d30fac76-40e0-47c8-960f-894adf15190e)

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

I also enable rdp (remote desktop protocol) on my Windows Machine, so the brute force attack could work.

![ss20](https://github.com/user-attachments/assets/58c6ec0a-03c2-4917-8c3f-bb5bd382d290)

Now that I had Active Directory set up, I can move over to my Kali Linux machine to perform a brute force attack.

My first step whas to update and upgrade repositories.

![ss1](https://github.com/user-attachments/assets/471b2ec6-a34b-419c-901a-6866f73a9f8a)

I then created a directory where I can work.

![ss2](https://github.com/user-attachments/assets/23c9c7d9-62c6-473f-9a83-2d1b5ffb67ee)

I did plan on using a tool Crowbar, but I was not able to configure it correctly, so instead I used a tool called Hydra.

To perform a brute force attack, I need a list of passwords that Hydra can use to try and break into the system.

I first unzipped a wordlist that was in the usr/share/wordlists directory.

![ss3](https://github.com/user-attachments/assets/dd523bfd-aa0c-4f20-808d-85b4b3799b59)

However, it was long file and i didn't wanna use all of it, so I used the head command to condensed it to 20 lines.

![ss5](https://github.com/user-attachments/assets/f3b50eff-31c1-49b0-8748-df8be60393b6)

I then edited the file, and added the passwords of the users I created, so the brute force attack could be performed correctly.

![ss6](https://github.com/user-attachments/assets/35b7cc1b-a1e0-49f9-9f74-b160f8db7925)

I then copied the password file to a directory I called AD Project. 

![ss4](https://github.com/user-attachments/assets/5f62a17b-9fc6-4b0f-9894-510161920b7f)

Now I just need the target user name (which in this case is billybob), the protocol (which is rdp) and the target IP address.

I then peformed my brute force attack. 

And it was successful.

![ss7](https://github.com/user-attachments/assets/f9c8426b-b105-42e7-850e-2d718fb826eb)

I then moved over to Splunk to see what telemetry was generarated.

When I was in Splunk, I saw traffic with an event code of 4625, which is an unsuccessful login attempt.

![ss8](https://github.com/user-attachments/assets/5392f028-ff0b-4ac4-a93d-2dbd8961bcf8)

You can also see that it came from Kali Machine, since it says the IP address of that machine.

![ss9](https://github.com/user-attachments/assets/1cdc5b76-fb29-4ec2-9953-f579c1abf52b)

There was also traffic with an event code of 4624 which is a successful login attempt, further proving that the brute force attack was successful.

![ss10](https://github.com/user-attachments/assets/666eed61-d454-4146-836a-68f2dc483838)

My next objective was to install Atomic Red team to see what other kinds of telemetry I could generate.

But before that, I set an exclusion for the entire C drive on my Windows 10 machine so Windows Defender doesn't remove any of the files from Atomic Read team.

![ss12](https://github.com/user-attachments/assets/095541a4-2efa-4f9e-968f-9a2e6183d8fe)

I then installed Atomic Red Team on my target machine.

![ss13](https://github.com/user-attachments/assets/ecab9348-1fd8-436e-99fe-8bf64003f45c)

I then learned that each of atomics in Atomic Red Team match the MITRE ATT&CK framework.

![ss15](https://github.com/user-attachments/assets/3a306ac8-7d76-4bbc-91b8-d538e5560dc9)

I then tested a few of the atomics in Powershell and then I checked Splunk to see what came up.

I used T1136.001 too create a new user.

![ss16](https://github.com/user-attachments/assets/87dddfa5-2422-401e-af62-271f3636a3d2)

After looking through Splunk, I found that a new user called NewLocalUser was created.

![ss17](https://github.com/user-attachments/assets/2aad6042-5327-4a4d-a598-41c997276e08)

## Issues that I faced

As mentioned earlier, I initally wanted to use Crowbar to perform my brute force attack. However, when I tried to run the attack, the tool said it couldn't find xfreerdp. 

![ss18](https://github.com/user-attachments/assets/c87b3992-ee47-41a2-a188-faf733cb9bd5)

After hours after researching and troubleshooting, I found that Kali had removed xfreerdp from it's repositories a few months ago, so I moved to plan B, and used Hydra.

Another issue I face was a lag in Splunk. It took some time between performing the brute force attack and seeing the results in Splunk. I then realized I didn't give the Ubuntu server enough memory to contain all searching and reporting data, so once I gave it more memory, Splunk worked perfectly.

![ss19](https://github.com/user-attachments/assets/aeb8326b-8a02-4df0-9484-d32df9bac79e)

## Conclusion

Overall, I had a lot fun with this lab. I felt that I gained experience in many different areas such IT adminstration, basic penetration testing, SOC environment, etc. I also felt that I became better in researching and troubleshooting when an issues had arised. Especially with the xfreerdp issue, I felt that I put many hours into finding the solution. Even though I determined the best solution was to just use another tool, I was proud of myself of not giving up right away. Like I said before, this lab was really fun and I learned many skills that I can take with me as I progress further with my cybersecurity journey.

## Notes
[notes.docx](https://github.com/user-attachments/files/20738369/notes.docx)

