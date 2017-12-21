Introduction
------------
Auto Domain Admin and Network Exploitation (autoDANE) is a tool that allows you to automate the process of exploiting, pivoting and escalating privileges on Windows-based domains. A key feature of autoDane is to assist penetration testers in quickly identifying the low-hanging fruit across a Windows domain; thereby allowing them to focus their attentions on more advanced attacks.

Background
----------
Given the prevalence of Microsoft Active Directory domains as the primary means of managing large corporate networks both globally and in South Africa specifically; one of the common first goals of many internal penetration tests is to get Domain Administrator (DA) level access.

To assist with this, a plethora of tools and techniques exist, from the initial “in” through to elevation of privilege and eventually extracting and cracking all domain credentials. However, the processes followed are still manual and time consuming. This detracts from potentially more dangerous attacks that may be specific to the organisation under assessment. In particular, networks that require pivoting across several internal hosts results in an analyst engaging in sometimes time-consuming “lateral movement”.

Observing both the time consuming nature of these “common tasks” and that they appeared easily automatable, we decided to construct a framework for automating such activities.

Differences to Existing Tools (e.g., DeathStar)
-----------------------------------------------
The heart of the autoDane project is an event-driven task manager, which runs small plugins (refer to Wiki), normalizes their output, and passes that as input to other plugins based on predefined rules. For example, when a host is identified (either manually, or through running standard host enumeration techniques), the host’s net block is port scanned. Open ports are passed to other plugins, which run further fingerprinting or vulnerability scanning tasks.

While tools like DeathStar aims to automate the entire DA process, autoDane takes a slightly different approach. The tool only automates the "common tasks" and provides insights into low-hanging vulnerabilities within a Windows domain. This information can then be manually interpreted and used by analysts to further infiltrate the domain. Thus, it gives power and insight directly to the analysts - instead of, a click and forget solution. This prevents those ackward situations where a client machine is brought down, and the analysts have no idea why.

What Does It Do?
----------------
autoDane has multiple plugins that automate "common tasks" and more are planned. These includes:
* Footprinting for common ports, mssql instances, and websites
* Host enumeration and vulnerability testing (testing for weak sql/tomcat creds, ms08-067...)
* Vulnerability exploitation (exploiting low-hanging vulnerabilities)
* Pivoting between machines (gaining further access into the domain).
* Domain enumeration (obtaining AD forest information and brute-forcing NTLM hashes)

The extend to which the above activities are performed is controllable by a slider within the application. All plugins are editable and can be modified/extended based upon the analysts particular requirements.

Getting Started
---------------
Pre-requisites
--------------
1. A machine running Kali-Linux 2017.3 rolling edition
2. An interface connected to the Internet (for installation purposes only)
2. An interfact (LAN/WiFi) connected to the Windows domain

Installing
----------
1. Ensure Kali is up-to-date (sudo apt-get update && sudo apt-get upgrade)
2. Ensure the PostgreSQL and Metasploit services are started (service postgresql start && service metasploit start)
2. Git clone autoDane to a local folder on the Kali machine (git clone https://github.com/sensepost/autoDANE.git)
3. Run install.sh (cd autoDane && ./install.sh)

Running
-------

1. Ensure the PostgreSQL and Metasploit services are started (service postgresql start && service metasploit start)
2. After that, simply run ./autodane.py

Full documentation on using autoDane and its various plugins can be found in the Wiki.

License
-------

autoDane is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License (http://creativecommons.org/licenses/by-nc-sa/4.0/). Permissions beyond the scope of this license may be available at http://sensepost.com/contact_us/.
