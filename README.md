# Snort-IDS-Home-Lab
#
## 1. Introduction
### This guide helps you set up a Snort Intrusion Detection System (IDS) Home Lab.
### Components:
 - ### Kali Linux (Attacker)
 - ### Ubuntu (Snort IDS)
            
## 2. Lab Setup
- ### Install VMware/VirtualBox.
- ### Create an Ubuntu VM for Snort.

## 3. Install Snort on Ubuntu
### 1.Update and upgrade packages:``sudo apt update && sudo apt upgrade -y``
![image](https://github.com/user-attachments/assets/b84dd285-8d06-48d7-92e3-8ec93af83a49)

### 2.Install Snort: ```sudo apt install snort -y```
![image](https://github.com/user-attachments/assets/0f28c4d8-19a6-4039-afaf-af56a76ce9e4)
- ### During installation, it may ask for the Network Interface (e.g., eth0, ens33). Open another terminal and run: ``ip a``  # For Linux  ``ipconfig``  # For Windows
![image](https://github.com/user-attachments/assets/5df75d11-11a7-4241-aba3-68404c142d04)

- ### Find the IP address and select the correct network interface.
![image](https://github.com/user-attachments/assets/d0ebf062-5067-4bb3-923a-b68d52623595)
![image](https://github.com/user-attachments/assets/b2be294b-412f-4432-9d8b-9b2523509a45)
- ### Verify installation:```snort --version```
![image](https://github.com/user-attachments/assets/6d8dc48d-9598-4ea2-b794-993b751fe307)
## 4.Configure Snort
- ### Open the Snort configuration file:```sudo nano /etc/snort/snort.conf```
![image](https://github.com/user-attachments/assets/39fc153f-ff5b-4944-85e0-2dbe1c1ca340)
 ### 1.Edit the Network Variables:
- ### Locate: ipvar HOME_NET any
- ### Replace "any" with your local network IP range (e.g., 192.168.1.0/24).
![image](https://github.com/user-attachments/assets/7b661f8f-873a-4061-9b6e-355e131e88bc)
 ### 2.Define the Rule Path:var RULE_PATH /etc/snort/rules
 - ### Ensure this line exists.
![image](https://github.com/user-attachments/assets/86e661f8-141e-48f0-87cd-e36a186b7090)
 - ### Save and exit:Press CTRL + X, then Y, and hit ENTER.
 ## 5. Create Required Directories
 - ### 1.Create the rules and log directories:```sudo mkdir -p /etc/snort/rules```
  - ### ```sudo mkdir -p /var/log/snort```,  ```sudo touch /etc/snort/rules/local.rules```
![image](https://github.com/user-attachments/assets/54c0538d-4599-4ba9-8fa5-be203be0d6f2)
 - ### 2.Assign correct permissions:```sudo chmod -R 777 /var/log/snort```
![image](https://github.com/user-attachments/assets/90fb4ffc-5883-4ce6-a7b5-9dbab9907126)
 ## 6.Add Snort Rules
 - ### 1.Create a basic test rule:```echo 'alert icmp any any -> any any (msg:"ICMP Packet Detected"; sid:1000001;)' | sudo tee -a /etc/snort/rules/local.rules```
![image](https://github.com/user-attachments/assets/db1e2e45-fcf5-488d-89b0-3285aea10341)
## 7. Run Snort in IDS Mode 
- ### Start Snort to monitor packets:```sudo snort -A console -q -c /etc/snort/snort.conf -i ens33```
![image](https://github.com/user-attachments/assets/abcae4d0-86f0-4cc3-a3a7-7f1167c4df74)
- ### Open another terminal (or Kali Linux machine) and run a ping test to the Ubuntu machine:ping <Ubuntu-IP>
![image](https://github.com/user-attachments/assets/81930bb4-9701-410a-ad2f-38e94b9e20bc)
- ### If Snort is working correctly, it should detect ICMP packets and display alerts.
![image](https://github.com/user-attachments/assets/4b5c5698-6f41-4814-b36d-56d1e64a0d08)
## 8.Stopping Snort Service
- ### To stop the Snort service, use:sudo systemctl stop snort
![image](https://github.com/user-attachments/assets/9202c3fa-e0b0-4a8a-9806-350120495399)
- ### To disable it from starting at boot:sudo systemctl disable snort
![image](https://github.com/user-attachments/assets/247837e7-01dd-47ae-a484-093032c60a8c)

## Conclusion
- ### This guide walks you through setting up Snort IDS in a home lab. With Snort running, you can analyze and detect network intrusions. You can further enhance it by adding more advanced rules and integrating it with SIEM solutions.
- ### Next Steps:Add more Snort rules.
- ### Integrate Snort logs with SIEM (e.g., Splunk, ELK Stack).
- ### Test with different types of attacks.







 



