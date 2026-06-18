# Guided-Lab-Traffic-Analysis-Workflow
Analyis of a Security Event Along with a writeup preparing for CDSA exam.


"One of our fellow admins noticed a weird connection from Bob's host IP = 172.16.10.90 when analyzing the baseline captures we have been gathering. He asked us to check it out and see what we think is happening.

Attempt to utilize the concepts from the Analysis Process sections to complete an analysis of the guided-analysis.zip provided in the optional resources and live traffic from the academy network. Once done, a guided answer key is included with the PCAP in the zip to check your work."

1. what is the issue?
-a brief summary of the issue.
-My thought process was to first filter for the IP first based on the first bit of info given

<img width="1026" height="740" alt="image" src="https://github.com/user-attachments/assets/f72de66d-cd31-4a62-9f89-8b38a7ff8aa5" />


I then also notice in the image that the destination port is 4444, from my previous learning in the lab I know that this port (4444) is commonly used by attackers for reverse shells and C2 traffic.

Also from the photo I can see that 172.16.10.2 is initiating the communication by first sending the (SYN) PACKET 
<img width="1028" height="731" alt="image" src="https://github.com/user-attachments/assets/e476d14f-3eb2-4c3a-9f82-fafdfbeb97dc" />

Next was to identify the first connection by identyfing the syn, syn-ack, ack handshake.

<img width="1028" height="731" alt="image" src="https://github.com/user-attachments/assets/36c36fe3-b1ed-4604-84b9-165e92f992ba" />

One way we could better establish and acknowledge of the reverse shell/backdoor is due to the "PSH" flag. After the handshake established a connection the attacker actually sent commands.

Next to see what other connections were made via 172.16.10.2 and 172.16.10.2

<img width="1031" height="386" alt="image" src="https://github.com/user-attachments/assets/555d89b8-b273-4f89-8c12-953d06dae92f" />



<img width="1013" height="545" alt="image" src="https://github.com/user-attachments/assets/c3178f22-de87-4956-bbec-c707833d3d22" />

From here we can see the attacker connected to Bob's host 172.16.10.90 via port 4444 and started pushing commands. 


Lets go through the actual document to find everything I missed.


what is the issue?
Suspicious traffic coming from within the network

define our scope and the goal (what are we looking for? which time period?)
target: traffic is originating from 10.129.43.4
when: within the last 48 hours. Capture traffic to determine if it is still happening.
supporting info: file: NTA-guided.pcap

define our target(s) (net / host(s) / protocol)
scope: 10.129.43.4 and anyone with a connection to it. Unknown protocol over port 4444.
capture network traffic
plug into a link with access to the 10.129.43.0/24 network to capture live traffic attempting to see if anything is happening.
We have been given a PCAP with historical data that contains some of the suspect traffic. We will examine this to analyze the issue.
identification of required network traffic components (filtering)

First, we will filter out anything that does not have a connection to 10.129.43.4, since this is our primary suspicious target for the moment.




