# EDR-Home-Lab-Attack-and-Defense

# <b>Project</b>

This lab is dedicated to simulating a real Cyber Attack and endpoint detection and response. Utilizing Eric <a href="https://blog.ecapuano.com/p/so-you-want-to-be-a-soc-analyst-intro?utm_campaign=post&utm_medium=web">Capuano's guide online</a>, I will be using virtual machines to simulate the threat & victim machines. The attack machine will utilize 'Sliver' as a C2 framework to attack a Windows endpoint machine, which will be running 'LimaCharlie' as an EDR solution.

# Azure Components Utilized

- Azure Virtual Network (VNet)
- Virtual Machine
- Log Analytics Workspace with Kusto Query Language (KQL) Queries
- Azure Storage Account
- Microsoft Sentinel
- Microsoft Defender for Cloud

# Architecture Before Hardening

In the "BEFORE" stage of the project, all resources were initially deployed with the hope that attraction would be gained from the public internet. The Virtual Machine had its Network Security Groups (NSGs) and built-in firewalls wide open, allowing unrestricted access from any source. This machines was then left to the public for 24 hours to generate the following attack maps mentioned earler.

<b> Using KQL Quesries i extracted logs from MS Sentinel to present the result of attacks on our Machine and location it came from</b>

<img src="https://i.imgur.com/ctQqArh.png">

<b> Next i Plotted this information to create an attack map that showcases RDP failures against the Windows machine.</b>

<img src="https://i.imgur.com/K6Xj5NO.png">

# After Hardening Measures and Security Controls

In the "AFTER" stage, based off the incidents created from the "Before" 24 hour capture, I implemented hardening measures and security controls to improve the environment's security from attackers.
These improvements included:

- Built-in Firewalls: In my virtual machines I configured the built-in firewalls so that it would deny access from unauthorized users.

<i>All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.</i>

# Metrics Before Hardening / Security Controls

The following table shows the metrics I measured in the secure environment for 24 hours:

SecurityEvent count on our Windows machine was	2087. After implementing security features to harden our environment, the count went down to 975. No failed login attempts were recorded.

# Utilizing NIST 800.61r2 Computer Incident Handling Guide

For each simulated attack I practiced incident responses following NIST SP 800-61 r2.

<img src="https://i.imgur.com/VUxp3ZA.png">

Each organization will have policies related to an incident response that should be followed. This event is just a walkthrough for possible actions to take in the detection of malware on a workstation.

# Preparation

The Azure lab was set up to ingest all of the logs into Log Analytics Workspace, Sentinel and Defender were configured, and alert rules were put in place.

# Detection & Analysis

- Malware has been detected on a workstation with the potential to compromise the confidentiality, integrity, or availability of the system and data.
- Assigned alert to an owner, set the severity to "High", and the status to "Active"
- Identified the primary user account of the system and all systems affected.
- A full scan of the system was conducted using up-to-date antivirus software to identify the malware.
- Verified the authenticity of the alert as a "True Positive".
- Sent notifications to appropriate personnel as required by the organization's communication policies.

# Containment, Eradication & Recovery

- The infected system and any additional systems infected by the malware were quarantined.
- If the malware was unable to be removed or the system sustained damage, the system would have been shut down and disconnected from the network.
-Depending on organizational policies the affected systems could be restored known clean state, such as a system image or a clean installation of the operating system and applications. Or an up-to-date anti-virus solution could be used to clean the systems.

# Post-Incident Activity

- In this simulated case, an employee had downloaded a game that contained malware.
- All information was gathered and analyzed to determine the root cause, extent of damage, and effectiveness of the response.
- Report disseminated to all stakeholders.
- Corrective actions are implemented to remediate the root cause.
- And a lessons-learned review of the incident was conducted.

# Conclusion

In this project, a Honeypot was deployed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. The significant reduction in security events and incidents following the implementation of security controls highlights their effectiveness in safeguarding the environment.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
