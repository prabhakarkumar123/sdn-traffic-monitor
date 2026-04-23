🟦 Project Title

Traffic Monitoring and Statistics Collector using SDN (Ryu + Mininet)

📌 Problem Statement

The objective of this project is to design and implement a Software Defined Networking (SDN) controller that collects, monitors, and displays network traffic statistics. The system should demonstrate controller-based traffic management, dynamic flow rule installation, and real-time monitoring of packet and byte counts.

🎯 Objectives
Demonstrate controller–switch interaction
Implement flow rules using match–action logic
Handle packet_in events in the controller
Monitor traffic statistics periodically
Analyze network behavior using tools
Demonstrate access control (allowed vs blocked traffic)
Validate performance using ping, iperf, and Wireshark
🧠 Technologies Used
Mininet – Network emulation
Ryu Controller – SDN controller
OpenFlow Protocol – Communication between switch and controller
Wireshark – Packet analysis
iperf – Throughput measurement
🧩 Network Topology
1 Switch (s1)
3 Hosts (h1, h2, h3)
Remote Ryu controller

👉 Simple topology chosen to clearly demonstrate:

Learning switch behavior
Traffic monitoring
Access control
⚙️ Installation & Setup
Step 1: Activate Ryu Environment
source ryu-env/bin/activate
Step 2: Run Controller
python3 -m ryu.cmd.manager traffic_monitor.py

👉 This starts the SDN controller which:

Handles packet_in events
Installs flow rules
Collects statistics
Step 3: Start Mininet
sudo mn -c
sudo mn --topo single,3 --controller remote

👉 Creates:

3 hosts
1 switch
Connected to controller
▶️ Execution Commands
🔹 Connectivity Test (Latency)
pingall

✔ Expected:

0% dropped (6/6 received)
🔹 Flow Table Inspection
dpctl dump-flows

✔ Shows:

Match fields
Actions
Flow rules
🔹 Throughput Test (iperf)
h1 iperf -s &
h2 iperf -c h1

✔ Expected:

Bandwidth ≈ 60 Mbps
🔹 Monitoring Output (Controller)

Controller continuously prints:

Packets: XXXX  Bytes: XXXX

✔ Shows real-time traffic statistics

🧪 Test Scenarios
✅ Scenario 1: Normal Operation
All hosts communicate
pingall → 0% dropped
❌ Scenario 2: Failure (Controller OFF)

Stop controller:

CTRL + C

Then:

pingall

✔ Output:

100% dropped
🚫 Scenario 3: Allowed vs Blocked
Traffic between h1 and h3 is blocked
Others communicate normally

✔ Output:

33% dropped
📊 Performance Analysis
Metric	Tool	Observation
Latency	ping	Low delay
Throughput	iperf	~60 Mbps
Flow rules	dpctl	Dynamic updates
Statistics	Controller	Increasing packet count
🔍 Wireshark Analysis
ARP packets → Address resolution
ICMP packets → Ping communication

✔ Confirms network behavior

🔄 Flow Rule Design
Match Fields:
Input port (in_port)
Destination MAC (dl_dst)
Actions:
Forward to output port
Drop (for blocked traffic)
Table-Miss Rule:
Sends unknown packets to controller
📈 Results
Successful learning switch implementation
Dynamic flow rule installation
Real-time traffic monitoring
Controlled traffic filtering
Performance validated using iperf
✅ Validation
Connectivity tested using ping
Performance tested using iperf
Packet analysis using Wireshark
Flow rules verified using dpctl
📚 References
Ryu Documentation
Mininet Documentation
OpenFlow Specification
