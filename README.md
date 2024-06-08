# EDR Home Lab Attack and Defense

# <b>Project</b>

This lab is dedicated to simulating a real Cyber Attack and endpoint detection and response. Utilizing Eric <a href="https://blog.ecapuano.com/p/so-you-want-to-be-a-soc-analyst-intro?utm_campaign=post&utm_medium=web">Capuano's guide online</a>, I will be using virtual machines to simulate the threat & victim machines. The attack machine will utilize 'Sliver' as a C2 framework to attack a Windows endpoint machine, which will be running 'LimaCharlie' as an EDR solution.

# Setup

The first step to the lab is setting up both machines. The attack machine will run on Ubuntu Server, and the endpoint will be running Windows 11. In order for this lab to work smoothly Microsoft Defender should be turned off (along with other settings). I am also going to be installing Sliver on the Ubuntu machine as my primary attack tool, and setting up LimaCharlie on the Windows machine as an EDR solution. LimaCharlie will have a sensor linked to the windows machine, and will be importing sysmon logs.

<img src="https://i.imgur.com/C16urUV.png">
<img src="https://i.imgur.com/jtFipvD.png">
<img src="https://i.imgur.com/PRz4Fmi.png">
<img src="https://i.imgur.com/JjncUXW.png">



# The Attacks, and the Defense

The first step is to generate our payload on Sliver, and implant the malware into the Windows host machine. Then we can create a command and control session after the malware is executed on the endpoint.

<img src="https://i.imgur.com/qqFPVFL.png">
<img src="https://i.imgur.com/0oAYil6.png">
<img src="https://i.imgur.com/rGSAtK6.png">
<hr>
Now that we have a live session between the two machines, the attack machine can begin peeking around, checking priveleges, getting host information, and checking what type of security the host has.

<img src="https://i.imgur.com/Jh0RacS.png">
<img src="https://i.imgur.com/20BbPrG.png">
<hr>
On the host machine we can look inside our LimaCharlie SIEM and see telemetry from the attacker. We can identify the payload thats running and see the IP its connected to.

<img src="https://i.imgur.com/3Jpyw7i.png">
<img src="https://i.imgur.com/JNb0W8w.png">
<img src="https://i.imgur.com/z9c4pkS.png">
<hr>
We can also use LimaCharlie to scan the hash of the payload through VirusTotal; however, it will be clean since we just created the payload ourselves.
<img src="https://i.imgur.com/tQVLaP1.png">
<img src="https://i.imgur.com/sZyhrAb.png">
<hr>
Now on the attack machine we can simulate an attack to steal credentials by dumping the LSASS memory. In LimaCharlie we can check the sensors, observe the telemetry, and write rules to detect the sensitive process.

<img src="https://i.imgur.com/mIYGpbK.png">
<img src="https://i.imgur.com/fM2sXhe.png">
<hr>

Now instead of simply detection, we can practice using LimaCharlie to write a rule that will detect and block the attacks coming from the Sliver server. On the Ubuntu machine we can simulate parts of a ransomware attack, by attempting to delete the volume shadow copies. In LimaCharlie we can view the telemetry and then write a rule that will block the attack entirely. After we create the rule in our SIEM, the Ubuntu machine will have no luck trying the same attack again.


<img src="https://i.imgur.com/0PHRQmE.png">
<img src="https://i.imgur.com/rpOYuEW.png">
<img src="https://i.imgur.com/ljJsuhR.png">
<img src="https://i.imgur.com/49RYl58.png">



# Conclusion

This home lab project effectively demonstrates a simulated cyber attack and defense scenario using virtual machines and specific tools: Sliver as the C2 framework on an Ubuntu server, and LimaCharlie as the EDR solution on a Windows 11 endpoint. Following Eric Capuano's guide, we set up the environment, disabled default security measures, and conducted various attack simulations to test the effectiveness of LimaCharlie.

<br>This exercise provided practical experience in both offensive and defensive cybersecurity measures, showcasing the importance of EDR solutions in detecting and responding to cyber threats. By simulating real-world attacks and defenses, we gained valuable insights into the dynamics of endpoint security and incident response.
