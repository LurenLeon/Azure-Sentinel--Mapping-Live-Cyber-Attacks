# Azure-Sentinel--Mapping-Live-Cyber-Attacks

## Table of Contents
1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Setup](#setup)
4. [Usage](#usage)
5. [Architecture](#architecture)
6. [Sample Scenario](#sample-scenario)
7. [Contributing](#contributing)
8. [License](#license)


## Introduction
<!-- Provide a detailed introduction to your project, its purpose, and what users can expect to achieve with it -->

This lab provides a hands-on experience for tracking live cyber attacks using Azure Sentinel and mapping them for analysis.

As an overview, this lab will involve a honeypot exposed to the internet, collecting attack log data, and a map to display the number of attacks from their respective countries. I have also used Windows PowerShell ISE, a third part API which is ipgeolocation, and Azure for setting up the honeypot VM and capturing log data.

We will use a PowerShell Script that will take the IP addresses from attempted failed logins and insert them onto ipgeolocation. These logs will be used to create a query in Sentinel to map the geographic locations.

<!-- List any prerequisites or dependencies that users need to have before using your lab -->
Before you begin, ensure you have:

### Prerequisites

Before you begin, ensure you have the following:

- An active Azure subscription.
- Azure Sentinel workspace set up.
- Permissions to create and manage resources in Azure.
- Remote Desktop Protocol (RDP) access.
- An account on [IPGeolocation.io](https://ipgeolocation.io/) for the API Key.
- Custom PowerShell Script (Provided by Josh Madakor).


<h2>Step 1: Creating your account on Azure </h2>
Create an Azure free account, insert credit card information and receive $200 free credits. 

## Step 2: Create a Honeypot Virtual Machine

On the search bar, search for Virtual Machines, click create virtual machine.

### Azure Sentinel Honeypot Lab Configuration

| Configuration           | Value               |
|--------------------------|---------------------|
| Subscription group       | Pay as you go       |
| Resource group           | Honeypotlab         |
| Virtual machine name     | Honeypot-vm         |
| Region                   | West US 3           |
| Security Type            | Standard            |
| Image                    | Windows 10 Pro      |
| Size                     | Standard            |
| Username and Password    | Create your own     |
| Public Inbound Ports     | Allow selected ports|
| Selected Inbound Ports   | RDP (3389)          |


Leave Disks section as default

On the networking section, find NIC network security group, change to advanced 
Create network security group- Delete original inbound rule, add an inbound rule

### Firewall Rule Configuration - DANGER_ANY_IN

| Configuration             | Value           |
|---------------------------|-----------------|
| Source                    | Any             |
| Source Port Ranges        | *               |
| Destination               | Any             |
| Service                   | Custom          |
| Destination Port Ranges   | *               |
| Protocol                  | Any             |
| Action                    | Allow           |
| Priority                  | 100             |
| Name                      | DANGER_ANY_IN   |


## Step 3: Create a Log Analytics Workspace 

Search for Log Analytics Workspace on Azure, create Log Analytics Workspace

Copy the following when creating:
- **Subscription:** Pay as you go
- **Resource group:** Choose the `honeypotlab`
- **Name:** law-honeypot1 
- **Region:** West US 2

| Configuration      | Value               |
| ------------------- | ------------------- |
| Subscription        | Azure Subscription 1|
| Resource Group      | Honeypotlab         |
| Name                | law-honeypot1       |
| Region              | West US 2           |



## Step 4: Configure Microsoft Defender for Cloud

Follow these steps to configure Microsoft Defender for Cloud on Azure:

- Search for Microsoft Defender for the Cloud on Azure.
- On the left side bar, navigate to the management section and click on "Environment Settings."
- Click on the environment named "law-honeypot1."

# On Defender Plans: 
- Turn off SQL Servers on Machines, and then click save.
- Turn on Servers, click save.
- On the right hand bar, click on Data collection, choose "All Events," and click save.


## Step 5: Return to Log Analytics Workspace
- Search for "Log Analytics Workspaces"
- Select log-honeypot
- On the right hand bar, under Workspace Data Sources, click "Virtual Machines"
- Select the workspace name honeypot-vm
- Click "Connect" to connect to the workspace to the honeypotvm



-Setup Microsoft Sentinel- Find and click create
-Click Log Analytics workspace that was created- Add






