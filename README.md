# Windows 10 Optimizations


## TOC
1. Undoing Nagle's Algorithm / Improveing Latency


## Undoing Nagle's Algorithm / Improveing Latency
Read more about Nagle's Algorithm here: https://en.wikipedia.org/wiki/Nagle%27s_algorithm

Nagle's algorithm TL;DR: I have a packet I want to send to a server, but its kinda small so I'll wait to send it untill I have more and lump them together.


### Requirements
1. Windows XP or higher (does not work on mac/linux as this is changing window's settings)
2. Decent CPU - A decent CPU means typically a quad core (or a computer made in this decade). This does increase your CPU by a very small margin. If you aren't running minecraft at 100% CPU you have nothing to worry about.
3. Internet that isn't dial up - 5 Mbps Down and 1 Mbps Up should be sufficient, but lower limits might still work. 
4. Common sense - If you can't follow instructions then I highly recommend you don't do this.


### Instructions
1. Open up run (Windows Key + R) and type "regedit" (without quotes, and note that everything afterwards that is surrounded by quotes should be removed too) and then hit enter

2. Go to the path "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\Tcpip\Parameters\Interfaces"

3. For each folder under Interfaces, you need to **repeat steps 4 and 5**. Please note three things: If the DWORD registry key is already there, just make sure it is set to the correct value. Capitalization MaTtErS, if you do not type the values with the EXACT correct capitalization, it WILL NOT WORK. Do NOT, I REPEAT DO NOT, EDIT/DELETE ANYTHING I DO NOT TELL YOU TO TOUCH.

4. Create two "DWORD" registry keys called "TcpAckFrequency" and "TCPNoDelay"
How to create new DWORD registry keys - https://i.imgur.com//Zdi6d98.png

5. Double-click on each new registry key and change the value from "0" to "1"(base hexadecimal)
Examples of editing them (double click on the name or right click on the name and hit modify… - MAKE SURE YOU ARE USING HEXADECIMAL) - https://i.imgur.com//LIlPMOm.png https://i.imgur.com//OoMJKMS.png

6. Confirm that you have done these keys ( https://i.imgur.com//3hRs3V2.png ) for all subfolders of the Interfaces folder (I have 4, you could have anywhere from 1 to 100. Also note that some of these might have nothing in them) - https://i.imgur.com//LscZ34O.png

7. Restart your computer (this is VERY important - these won't activate until you do so as most registry updates don't actually activate until windows reloads. If you've ever wondered why you are asked to restart after installing a program - this is why)
