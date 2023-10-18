# Azure-Sentinel--Mapping-Live-Cyber-Attacks

Table of Contents
Introduction
Prerequisites
Setup
Usage
Architecture
Sample Scenario
Contributing
License

Introduction
<!-- Provide a detailed introduction to your project, its purpose, and what users can expect to achieve with it -->

This lab provides a hands-on experience for tracking live cyber attacks using Azure Sentinel and mapping them for analysis.

As an overview, this lab will involve a honeypot exposed to the internet, collecting attack log data, and a map to display the number of attacks from their respective countries. I have also used Windows PowerShell ISE, a third part API which is ipgeolocation, and Azure for setting up the honeypot VM and capturing log data.

We will use a PowerShell Script that will take the IP addresses from attempted failed logins and insert them onto ipgeolocation. These logs will be used to create a query in Sentinel to map the geographic locations.


Prerequisites
<!-- List any prerequisites or dependencies that users need to have before using your lab -->
Before you begin, ensure you have:

An active Azure subscription.
Azure Sentinel workspace set up.
Permissions to create and manage resources in Azure.
Remote Desktop Protocol (RDP)
An account on IPGeolocation.io for the API Key
Custom Powershell Script (Provided by Josh Madakor)

Step 1: Creating your account on Azure 
Create an Azure free account, insert credit card information and receive $200 free credits. 

Step 2: Create a Honeypot Virtual Machine

On the search bar, search for Virtual Machines, click create virtual machine.

Subscription group: Pay as you go
Resource group: Honeypotlab
Virtual machine name: Honeypot-vm
Region: West US 3
Security Type: Standard
Image: Windows 10 Pro
Size: Standard
Create your username and password for the VM.
Public inbound ports: Allow selected ports
Select inbound ports: RDP (3389)

Leave Disks section as default

On the networking section, find NIC network security group, change to advanced 
Create network security group- Delete original inbound rule, add an inbound rule

Source: Any
Source port ranges=*
Destination: Any
Service: Custom
Destination port ranges: *
Protocol: Any
Action: Allow
Priority: 100
Name: DANGER_ANY_IN

Step 3: Create a Log Analytics Workspace 
Search for Log Analytics Workspace on Azure, create Log Analytics workspace

Subscription: Pay as you go
Resource group: Choose the honeypotlab
Name: LAWhoneypot
Region: West US 2


Step 4: Configure Microsoft Defender for Cloud

Search for Microsoft Defender for the Cloud on Azure
On left side bar, look for management section, and click on environment settings
Click on LAWhoneypot
Turn off SQL Servers on Machines, click save
Click Data collection, choose "All Events", click save





Return to Log Analytics workspace
Find virtual machine section, and click "Connect" to connect the workspace to the honeypotvm


• Setup Microsoft Sentinel- Find and click create
o Click Log Analytics workspace that was created- Add






