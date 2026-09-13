Context: 
 This system implements a dual-language SIEM pipeline to detect anomalies in server logs. It leverages C++ for high-throughput, low-footprint log parsing and Python for asynchronous rolling-window analysis and UI rendering. 
Goals: 
 -Rolling-window threat detection
 -UI Rendering in Python
 -Sub-millisecond log parsing in C++
 -Others to be added
Non-Goals: 
 This project will not be gathering information from anything but server logs. (Adding addition sources will be a follow-up project, separately.) It will also not use a persistent database, or use any non-text data. 
Architecture Overview: 
 Log file -> C++ Agent -> Unix Socket -> Python Engine -> TUI
 Note that this is only for the first iteration, and as more problems and solutions are found, 
the architecture will change accordingly. 
API Contract (Will also be changed, and versioned):
{ "version": "1.0", "timestamp": 1726211789,  "ip_address": "192.168.1.50", "event_type": "ssh_failed", "raw_log": "Failed password...”} 
            Note: All arguments are strings except for timestamp, which is an int
Security/V2.0 Considerations and Solutions:
 -Regex DoS: Use RE2 instead of standard regex
 -JSON Injection: Use strict escaping
 -Log Forging: Implement input validiation in Python
 -Socket Deadlocking: Implement non-blocking sockets in C++

