# Port Scanning

1. Check nmap version

       nmap -v
   
<img width="376" height="290" alt="Screenshot 2025-12-12 114610" src="https://github.com/user-attachments/assets/f54d286c-145c-4a68-a7de-c38ac529ef93" />


2. Performs a ping scan (no port scanning) across the subnet 10.6.6.0/24 to identify which hosts are up and reachable.

        nmap -sn 10.6.6.0/24

3. Attempt to identify the operating system running on the target host (10.6.6.23).
   - This helps understand the environment and potential OS-specific vulnerabilities.

        sudo nmap -O 10.6.6.23
<img width="380" height="196" alt="open port_OS running on host" src="https://github.com/user-attachments/assets/a872d068-0a8f-44e5-bf60-528a4be9ece3" />

4. Scan port 21 specifically with:

       nmap -p21 -sV -A -T4 10.6.6.23
   
   - sV → Detects service versions
   - A → Enables OS detection, traceroute, and NSE scripts
   - T4 → Faster scan timing
<img width="391" height="243" alt="aggressive scan" src="https://github.com/user-attachments/assets/f61c82e9-263e-4095-a9e8-1430841a8631" />

5. Scan Windows SMB ports (139 and 445) with aggressive detection.

       nmap -p139,445 -A 10.6.6.23
   
   - Useful to identify:SMB version
   - Security posture
   - Potential SMB vulnerabilities

6. Runs the SMB share enumeration script against port 445. 

       nmap --script smb-enum-shares.nse -p445 10.6.6.23

   - Reveals: Shared folders, Permissions & Anonymous access possibilities
<img width="350" height="290" alt="weakness on SMB" src="https://github.com/user-attachments/assets/6653eddf-bda9-4e58-8086-0132790a5133" />

7. Attempts to access the SMB share print$ without authentication (-N).
   - If access succeeds, you can browse files within the share.
  
         smbclient //10.6.6.23/print$ -N

8. Display network interface configuration using "ifconfig"
   IP address, MAC address & Network status

       ifconfig
<img width="316" height="389" alt="ifconfig" src="https://github.com/user-attachments/assets/c0918552-87f9-4bac-be58-2e28375f03df" />

9. ip route: Shows the system’s routing table, including:
   - Default gateway, Routing paths & Interface assignment
   - Useful for understanding how traffic leaves the machine

10. Display DNS server configuration using:

        cat /etc/resolv.conf
    - Helps verify: Domain names & DNS servers being used

11. Capture all network traffic on interface eth0, saving it to a file named flames.pcap.

        sudo tcpdump -i eth0 -s 0 -w flames.pcap: 
    Parameters:
    - i eth0 → specify interface
    - s 0 → capture full packets (no truncation)
    - w flames.pcap → write to file
<img width="491" height="123" alt="ncap" src="https://github.com/user-attachments/assets/c0cadbfb-a1dc-4f56-8dab-dcd2eed71ed6" />


12. Verify that the capture file exists in the current directory using:

        ls flames.pcap

13. Open the Wireshark GUI to import and analyze the captured .pcap file
    <img width="540" height="425" alt="wireshark" src="https://github.com/user-attachments/assets/a7957543-0d18-4425-a0c2-1a51b23e657a" />

