# Serial-Communication-with-socat
This repository provides a simple setup for serial communication over TCP using socat. Useful for devices connected via /dev/ttyACM0.

Usage
1. Host Setup
Run the following on the host machine:

bash
Copy code
sudo chmod 666 /dev/ttyACM0
sudo usermod -a -G dialout $USER

socat -d -d -v TCP-LISTEN:1680,fork,reuseaddr /dev/ttyACM0,raw,echo=0
2. Client Connection
Connect from the client machine using:

Option 1: Link to /dev/Gripper
bash
Copy code
socat PTY,link=/dev/Gripper,raw TCP:<HOST_IP>:1680
Option 2: Link to /tmp/Gripper (No sudo needed)
bash
Copy code
socat -d -d -v PTY,link=/tmp/Gripper,raw,ignoreeof,onlcr TCP:<HOST_IP>:1680
Replace <HOST_IP> with the IP of the host machine.
