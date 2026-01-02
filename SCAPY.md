# Work with Scapy on Kali Terminal

1. Switch to the root user using "sudo su", which is required because Scapy needs elevated privileges to capture packets and interact with network interfaces.

         Sudo su

2. Launch the Scapy interactive shell.

<img width="358" height="296" alt="Navigating Scapy" src="https://github.com/user-attachments/assets/ac0f865f-fd33-4b89-acc4-a46c619e8ac9" />


3. Use sniff() to Start capturing packets on the default network interface until manually stopped
   
<img width="403" height="394" alt="sniffing" src="https://github.com/user-attachments/assets/48a3514f-2914-46f4-bb0e-f7f289941911" />


4. ping google.com : This creates ICMP packets (echo-request and echo-reply), allowing Scapy to capture live traffic.

         In ping terminal → Ctrl + C : Stops the ping.

- temi = _
         : _ in Scapy (and Python REPL) represents the last output.
          This stores the sniffed packets inside variable temi.

5. temi.summary(): Displays a shorthand list of every packet captured (e.g., ARP, ICMP, TCP, DNS).

6. sniff(iface="br-internal") : Starts sniffing specifically on the interface br-internal, which is likely the internal NAT or lab network.

            sniff(iface="br-internal")

7. ping 10.6.6.1/24 : Pinging a gateway or device pushes new packets through the network — ARP requests, ARP replies, ICMP traffic.

         Open browser → type 10.6.6.23
              TCP handshake packets
              HTTP GET request(s)
              DNS lookups (if hostname used)
              Responses from the server

8. sniff(iface="br-internal", filter="icmp", count=5):
   This tells Scapy:
   - Listen only on br-internal
   - Capture only ICMP packets
   - Stop after 5 packets
     
<img width="329" height="194" alt="ping based on interface and filter protocol" src="https://github.com/user-attachments/assets/9be76f8f-832a-48e2-a060-dcba664ba13d" />

9. temi3[3] : Shows the 4th packet captured in full detail.
   - An ICMP request
   - An ICMP reply
   - ARP resolution packet (if ARP occurred before ICMP)
This prints the whole packet structure (IP layer → ICMP layer → payload).
<img width="951" height="69" alt="Network logs" src="https://github.com/user-attachments/assets/d288447c-17a7-48e1-8f8c-9594c95b766c" />

