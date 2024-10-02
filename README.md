# metasploit-kali
Using Metasploit to access vulnerable machines on my home lab

# Step 1
I used ``nmap -sV [Target PC IP]`` to scan for open/vulnerable ports. I will be exploiting TCP Port 21 using FTP
![image](https://github.com/user-attachments/assets/5b8357bf-5f0c-4b0b-a128-d9edd64eae47)

# Step 2
I then opened metasploit and used `use exploit/unix/ftp/vsftpd_234_backdoor` to open the exploit tool
![image](https://github.com/user-attachments/assets/d14fe601-90fc-4dc3-b807-28da1375f55e)

# Step 3
I use `set RHOST [Target IP]` to access the computer in a shell terminal
&nbsp;
![image](https://github.com/user-attachments/assets/485bad15-6538-4807-820c-f0fc582cd4e2)

# Step 4
I then navigate through their files to find my target file and do whatever I need to. 
&nbsp;
![image](https://github.com/user-attachments/assets/2be18301-3ff5-4427-a063-eb0a062b0fdd)
