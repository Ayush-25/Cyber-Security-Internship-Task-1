# Local Network Port Scan — Cyber Security Internship Task 1
*Network reconnaissance and open port scanning using Nmap in Kali Linux*


## Objective
Scan the local network to discover open ports and understand network service exposure.  
This task helps in learning basic network reconnaissance skills and identifying potential security risks.


## Methodology and Commands with screenshots.
We performed the complete local network port scanning task using Nmap with the following commands:

# Find local IP addresses and network range (CIDR)
ip -4 addr show | grep -oP '(?<=inet\s)\d+\.\d+\.\d+\.\d+/\d+'
<img width="658" height="145" alt="image" src="https://github.com/user-attachments/assets/b36c1c0c-df8d-4e82-8804-1bbe18dab90a" />

# Perform TCP SYN scan on the local network
sudo nmap -sS 192.168.0.0/24 --open -oN scan_results.txt
<img width="757" height="482" alt="image" src="https://github.com/user-attachments/assets/c11b2922-801e-4f0f-b341-f59223afeeaa" />

# Extract IP addresses and open ports into a concise summary
awk '/Nmap scan report for/{ip=$NF} /\/tcp.*open/{print ip " : " $0}' scan_results.txt > findings.txt
<img width="922" height="166" alt="image" src="https://github.com/user-attachments/assets/be433b51-4b9f-4443-b23f-9f3948bf549b" />

# Perform full TCP scan with service and OS detection
sudo nmap -sS -p- -T4 -sV -O 192.168.0.0/24 -oN full_tcp_scan.txt
<img width="1216" height="748" alt="image" src="https://github.com/user-attachments/assets/c3eb8999-a3e5-4e06-94aa-c4fda7ce7855" />

# Save scan results in XML format
sudo nmap -sS 192.168.0.0/24 -oX results.xml

<img width="651" height="551" alt="image" src="https://github.com/user-attachments/assets/ee410285-acae-4356-bc6c-e9008a4e5947" />


# Convert XML results to HTML for easier visualization
xsltproc results.xml -o results.html

<img width="661" height="573" alt="Screenshot 2025-09-22 113143" src="https://github.com/user-attachments/assets/01f703ae-cdb2-4b1a-930e-1c9e4e4e4304" />




## Findings
From the scan, the following hosts and open ports were detected:

IP Address       | Open Ports         | Services
-----------------|-----------------|--------------------------
192.168.0.1      | 22, 53, 80, 1900 | SSH, DNS, HTTP, UPnP
192.168.0.102    | 1234             | Hotline


## Risks & Recommendations
- Open ports can expose devices to unauthorized access or exploitation.
- Close unused ports or secure them via firewall rules.
- Regularly patch services to reduce vulnerabilities.
- UPnP (1900) and unusual ports (e.g., 1234) should be monitored carefully.


## Files Included
- scan_results.txt → main scan output
- findings.txt → IP + open ports summary
- Screenshots of commands as proof of execution


## Conclusion
The network scan demonstrated how to discover open ports and analyze network service exposure.  
Practical skills gained include network reconnaissance, interpreting Nmap results, and identifying potential security risks.

---

## Contact
Ayush Singh  
Email: ayushsinghfeb2502@gmail.com
