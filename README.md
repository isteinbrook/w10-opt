# Windows 10 Optimizations

## TOC
1. [Optimizations](https://github.com/isteinbrook/w10-opt/blob/master/README.md#1-optimizations)

	A. [Mouse accel tweaks](https://github.com/isteinbrook/w10-opt/blob/master/README.md#a-mouse-accel-tweaks)
	
	B. [Undoing Nagle's Algorithm / Improving Latency](https://github.com/isteinbrook/w10-opt#b-undoing-nagles-algorithm--improving-latency)
	
	C. [Network throttling index](https://github.com/isteinbrook/w10-opt#c-network-throttling-index)
	
	D. [System Gaming Responsiveness](https://github.com/isteinbrook/w10-opt#d-system-gaming-responsiveness)
	
	E. [Disable bandwidth sharing](https://github.com/isteinbrook/w10-opt#e-disable-bandwidth-sharing-for-updates)
	
2. [Bloatware Removal](https://github.com/isteinbrook/w10-opt#2-bloatware-removal)

	a. [Cortana Removal](https://github.com/isteinbrook/w10-opt#a-remove-cortana)
	
	b. [Bloatware removal](https://github.com/isteinbrook/w10-opt#b-bloatware-removal)


## 1. Optimizations
### A. Mouse accel tweaks
Disable the “help” (hint: it doesn’t help) Windows tries to give you. This disables mouse acceleration and stops Windows from modifying your mouse input.
2. Press the windows key
3. Type in “mouse”
4. Click “Mouse settings”
5. Click “Additional mouse options”
6. Select the “Pointer Options” tab and make sure that “Enhance pointer precision” is turned off, and your pointer speed is set exactly in the middle (the 6th notch from the left or right). 

https://i.imgur.com/qOUpWLC.png

Mouse accel tweaks 
http://donewmouseaccel.blogspot.com/2010/03/markc-windows-7-mouse-acceleration-fix.html



### B. Undoing Nagle's Algorithm / Improving Latency
Read more about Nagle's Algorithm here: https://en.wikipedia.org/wiki/Nagle%27s_algorithm

Nagle's algorithm TL;DR: I have a packet I want to send to a server, but it's kinda small so I'll wait to send it until I have more and lump them together.


#### Requirements
1. Windows XP or higher (does not work on mac/linux as this is changing window's settings)
2. Decent CPU - A decent CPU means typically a quad core (or a computer made in this decade). This does increase your CPU by a very small margin. If you aren't running minecraft at 100% CPU you have nothing to worry about.
3. Internet that isn't dial up - 5 Mbps Down and 1Mbps Up should be sufficient, but lower limits might still work. 
4. Common sense - If you can't follow instructions then I highly recommend you don't do this.


#### Instructions
1. Open up run (Windows Key + R) and type "regedit" (without quotes, and note that everything afterwards that is surrounded by quotes should be removed too) and then hit enter

2. Go to the path "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\Tcpip\Parameters\Interfaces"

3. For each folder under Interfaces, you need to **repeat steps 4 and 5**. Please note three things: If the DWORD registry key is already there, just make sure it is set to the correct value. Capitalization MaTtErS, if you do not type the values with the EXACT correct capitalization, it WILL NOT WORK. Do NOT, I REPEAT DO NOT, EDIT/DELETE ANYTHING I DO NOT TELL YOU TO TOUCH.

4. Create two "DWORD" registry keys called "TcpAckFrequency" and "TCPNoDelay"
How to create new DWORD registry keys - https://i.imgur.com//Zdi6d98.png

5. Double-click on each new registry key and change the value from "0" to "1"(base hexadecimal)
Examples of editing them (double click on the name or right click on the name and hit modify… - MAKE SURE YOU ARE USING HEXADECIMAL) - https://i.imgur.com//LIlPMOm.png https://i.imgur.com//OoMJKMS.png

6. Confirm that you have done these keys ( https://i.imgur.com//3hRs3V2.png ) for all subfolders of the Interfaces folder (I have 4, you could have anywhere from 1 to 100. Also note that some of these might have nothing in them) - https://i.imgur.com//LscZ34O.png

7. Restart your computer (this is VERY important - these won't activate until you do so as most registry updates don't actually activate until windows reloads. If you've ever wondered why you are asked to restart after installing a program - this is why)


### C. Network Throttling Index
Windows implements a network throttling mechanism, the idea behind such throttling is that processing of network packets can be a resource-intensive task. It is beneficial to turn off such throttling for achieving maximum throughput.

1. To implement this tweak, run regedit and modify the registry HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile. 

2. Under SystemProfile, create a DWORD value and name it to “NetworkThrottlingIndex” then set its Hexadecimal value to ffffffff for gaming and max throughput, this completely disables throttling.

### D. System Gaming Responsiveness
Multimedia streaming and some games that uses “Multimedia Class Scheduler” service (MMCSS) can only utilize up to 80% of the CPU. The “Multimedia Class Scheduler” service (MMCSS) ensures prioritized access to CPU resources, without denying CPU resources to lower-priority background applications.

1. Run regedit and modify the registry key HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile. 

2. create a new DWORD and name it to “SystemResponsiveness” set its hexadecimal value to 00000000 for pure gaming/streaming.

In the same Registry hive as the above tweak, you can also change the priority of Games. To implement this tweak, 
1. go to HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games and change the following registry values:

“GPU Priority” change its values to 8 for gaming.

“Priority” set to 6 for gaming.

### E. Disable Bandwidth Sharing for Updates
In another strange act of opt-out data sharing between users, Windows now uses a sort-of peer-to-peer network for downloading updates. Similar to a torrent program, this means that when you download a Windows update file, you're also uploading parts of it to other users.

1. Start by heading to the Settings menu, but this time open the "Update & Security" section.

2. From the "Windows Update" tab on the next screen, click the "Advanced options" button to find the setting we're looking for.

3. Next, scroll down to the bottom of this page, then select the option labeled "Choose how updates are delivered."

4. Finally, turn off the toggle switch directly beneath the excerpt about "Updates from more than one place." They really buried this one deep, didn't they?

## 2. Bloatware removal

### a. Remove cortana
1. Open regedit the registry editor, from the search box on the taskbar.
2. Go to HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Windows Search
But wait! Windows Search might not be there. It wasn't for us, so we had to create it.
2a. Right-click the Windows folder and choose New>Key. Call it "Windows Search."
3.  Right click "Windows Search" and choose New > DWORD (32-bit Value).
4. Name the DWORD "AllowCortana." Click it and make sure the value is "0."
5. Restart the computer (or log out and log back in). Cortana will be replaced with a regular search bar.


### b. Bloatware removal
Script removes

Create a new file called (e.g.) delete_bloatware.bat and copy the code from https://pastebin.com/31yrSCCe into it, then right click and execute as administrator

