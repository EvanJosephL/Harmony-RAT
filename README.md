# Harmony-Proof of Concept
A Proof of Concept remote administration tool developed for cybersecurity research and educational purposes.  It demonstrates how modern malware can leverage legitimate cloud services for command and control communications. 


**Features**  
- Full Shell  
- Download files  
- Upload files  
- Screenshot    
- Dump credentials stored in Chrome  
- Persistence  
- And more...

# Disclaimer
All code provided in this repository is for educational purposes only.

# Detection Opportunities
Harmony generates attacker like activity that can be used to develop and validate defensive detections. Depending on the features excersised defenders may observe:
- Discord-based command-and-control activity using a bot token, webhooks, channels, and server-side tasking
- System reconnaissance using commands such as `wmic`, `getmac`, `whoami`, and external IP lookup through `ipinfo.io`
- Remote shell execution through `subprocess.Popen(..., shell=True)`
- File upload and download behavior involving Discord attachments and local filesystem paths
- Screenshot capture through Windows desktop/GDI APIs
- Chrome credential access through the `Login Data` database, `Local State`, DPAPI, and AES-GCM decryption
- Persistence attempts through the current user Run registry key and the Startup folder
- File hiding through the Windows `attrib +H` command

# Defensive Engineering
Harmony was developed as an educational proof of concept for understanding attacker like behaviours and improving defensive visibility. The project can be used to:
- Generate realistic telemetry for blue team and malware analysis labs
- Practice identifying command-and-control behavior over legitimate cloud services
- Build and validate detections for suspicious process execution, registry persistence, screenshot capture, and browser credential access
- Study how host artifacts appear in Windows logs, EDR telemetry, and network monitoring tools
- Map observed behaviors to MITRE ATT&CK techniques
- Understand how defensive controls can detect or limit common post-exploitation actions


# Usage  
**In your server you MUST create a text channel named 'check-in'  
and create a webhook that posts in the 'check-in' channel**

**You have to enter your Discord servers:**  
* Webhook URL
* Bot Token  
* ServerID  
* executable filename

**Into the script around line 32.**
___
Once harmony is executed it will create a new category on your server named with the hardware ID of the computer that executed it.  


3 channels will also be created in that category:  
&emsp;-main: Use this channel to send commands to the victim computer.  
&emsp;-info: On first run the script will dump useful system information in here.  
&emsp;-creds: On first run the script will dump URL, username and password saved in chrome into here.  

# Commands  

**Commands are used in the main channel in the target category**

To send shell commands prefix the command with '>'.  
&emsp;EX:  
```
> tasklist
# Execute command 'tasklist' and return list of running tasks.

> dir c:\Users\bob\Downloads
# Execute command 'dir c:\Users\bob\Downloads' and return list of files in bobs download directory.
```  
---  
**Non shell commands dont need the '>' symbol**  

---  
**kill**  
Kills process specified by pid.  

EX:  
```
kill 2654
```

---
**hide**  
Adds the hidden attribute to the harmony file.  

**unhide**  
Removes the hidden attribute from the harmony file.  

EX:
```
hide
```
```
unhide
```

---
**download**
Uploads file specified by path to server.

EX:
```
download c:\Users\bob\Downloads\nuclearlaunchcodes.txt
```

---
**upload**  
Downloads a file and saves it to c:\Users\Public\Downloads\

type upload and then drag the file you want to upload into discord and send the command.

EX:
![](https://github.com/EvanJosephL/Harmony-RAT/blob/main/pngs/upload_example.gif)  

----
**screenshot**  
Takes a screenshot and uploads it to the server.  

EX:
```
screenshot

# or

ss
```

---
**listWindows**
Lists all open windows.  

EX:
```
listWindows

# or

lw
```

---
**credDump**
Dumps all creds saved in Chrome.

EX:
```
credDump

# or

cred
```

---
**persistence**
Attempts to add persistence

EX:
```
persistence

# or

pt
```
