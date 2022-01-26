# Notes
- - [Notes](#notes)
  * [Email Security - Proofpoint](#email-security---proofpoint)
    + [Protection Server Foundations Level 1](#protection-server-foundations-level-1)
      - [Message Flow](#message-flow)
      - [SMTP and Filtering](#smtp-and-filtering)
    + [Protection Server Administration Level 1](#protection-server-administration-level-1)
      - [Cluster and Modules](#cluster-and-modules)
      - [Navigation](#navigation)
      - [User Management](#user-management)
      - [End User Services](#end-user-services)
      - [TAP](#tap)
    + [Protection Server Configuration](#protection-server-configuration)
      - [Policy Routes](#policy-routes)
      - [Rules](#rules)
      - [Dispositions](#dispositions)
      - [Quarantine Function](#quarantine-function)
  * [Email Security - Microsoft Defender 365](#email-security---microsoft-defender-365)
    + [Zero-hour auto purge ZAP basics](#zero-hour-auto-purge--zap--basics)
    + [How ZAP works](#how-zap-works)

## Email Security - Proofpoint
### Protection Server Foundations Level 1
#### Message Flow
- Protection server filters messages that arrive and only accepts messages that meet criteria set by admin
- Diagram structure:

![image](https://user-images.githubusercontent.com/95253821/144477472-2fd51fe1-d2e9-449a-b67d-3d7268e60269.png)
- From internal mail server to Mail Transfer Agent (MTA) to Mail Exchange record (MX). 
- This record specifies server on the internet responsible for accepting email messages on behalf of receiver server. 
- With info gathered from DNS sending MTA can reach receiving MTA Proofpoint protection serer acts as MTA then sends to mail server then to receiver. 
- The Protection Server is an email security gateway, which does what the name suggests; it provides a gateway for processing and filtering email to protect your users and your network from threats and attacks sent via email.
- Without email security gateway users exposed to spam, fraud/spoofs, harmful attachments/links, viruses, email loads

#### SMTP and Filtering
 ![image](https://user-images.githubusercontent.com/95253821/144477606-4d5a8bd8-b63c-4397-97ab-8c5a0780bd44.png)
 - Connection: Sender reaches out to receiver, checks if they are supposed to reject messages, verify the IP belongs to it, check reputation within the Protection server 
- Envelope: Shows where message is from and who it is for, protection server checks all of those
- Body: MTA lets protection server know they are going to send message; Protection server gives rules for sender to follow. Protection servers checks message and looks for any malicious things
- What they contain
  - Header: Within the body of message, bad guys can spoof header to pretend its from somewhere safe.
  - Connection: Sender HELO domain, sender IP address, sender host name
  - Envelope: Sender email address, recipient host name
  - Body: Message Size, attachment attributes, message text content
  - Header: Subject, from, date, to 
 
### Protection Server Administration Level 1
#### Cluster and Modules
- Cluster = Master + Agents (# of agents depends)
- The agents filter and relay the messages, and the master provides centralized configuration and administration through the web-based management interface.
- Module is an app that performs specific filtering task
- Making changes to policy or anything do so on master
- Cluster can be on-prem or virtual. Can Configure and manage cluster from Master server
- On Prem:
  - Filtering agents first contacts for inbound messages MX records point to clusters
  - Master Never handles mail directly, once scanned by Filtering agents then sent to internal mail server then to user
  - These ports need to be open for Master server and Agents to communicate (usually of different networks separated by firewall)
  - Ports: 
    - Configuration 10000
  	- Database 3306
  	- Logs 10010
    - Master needs to talk to Proofpoint Update server (needs outbound access SSL 443) for updates
- Proofpoint On Demand: Proofpoint hosted option
 - Cluster in Proofpoint Data center, MX record points to Proofpoint IP
 - Modules: software plugins essentially, add new features to protection server
 - 6 Modules
    - Email firewall Module: Filters in-bound messages by connection and envelope attributes
    - Virus Protection module: uses virus definitions and heuristics to detect messages containing infection
    - Spam Detection Module: Uses Proofpoint’s proprietary MLX tech to classify inbound messages as spam
    - Regulatory Compliance Module: Ensure that outbound messages comply with privacy-related regulations
    - TAP Module: Targeted Attack Protection inspects attachments and URLs for threats
    - Digital Assets Module: Scans outbound messages for confidential or proprietary info
      
#### Navigation
- All menus grouped into 3 major tabs across the top
- System Tab: Manage administrative and global settings
    - Appliance Settings
  	- User management
    - Logs and reports
    - Quarantine
    - Policy Routes
- Email Protection tab: Manage in-bound traffic
    - Email firewall
    - Email authentication
    - Spam detection
    - Virus protection
    - TAP
- Information Protection tab: Manage out-bound traffic
    - Encryption
    - Digital assets
    - Secure share
    - Regulatory compliance
    
#### User Management
- User repository: data base on the protection server that contains the info about users in the org. Use it to organize users and give them group and individual settings
- Recipient Verification Overview: filtering & processing a message and uses resources. Checks the intended recipient against the user repository
- Email Filtering: can apply firewall rules to groups by grouping individuals in the user repository 

#### End User Services
- End User Digest overview: provides user with list of messages that have been sent to quarantine, helps filter and false positives by seeing digest
- End User web app overview: allows a user to edit their safe and block lists, views their quarantine and release messages, manage encryption keys for messages

#### TAP
- URL defense: when msg contains embedded link protection server will analyze link
- If the URL's status is unknown, the user will be allowed to the site while the URL is further evaluated, and a reputation can be assigned
- Re-written URL: when URL is revealed, protection server rewrites URL so user cannot simply type the malicious URL into a browser and access site
- Attachment defense: when attachment arrives, protection server analyzes before forwarding the message
- 
### Protection Server Configuration
#### Policy Routes
- Policy Routes: provide a way to group connect and envelope attributes into conditions
- Protection server evaluates each message, give sit a tag then routes it to the appropriate firewall rule
- Creating Policy Routes
  1. Route ID
  2. Description
  3. Condition
    - Country Code
    - Envelope Recipient
    - Envelope Sender
    - Local IP
    - Protocol
    - Sender HELO domain
    - Sender hostname
    - Sender IP address
    - Sender reverse IP 
  4. Save Changes
- System tab --> System menu --> Policy Routes --> add
- Ex: 
- Route ID(name) Orange
- Descrip.       Sender is from X Company
- Add Condition
- Condition:            
-                       Sender Hostname
- Condition Attribute:  
-                       Attribute: Sender Hostname
-                       Operator: Contains
-                       Value: X Company
- Save changes
- Policy listed bottom of table now
#### Rules
- Make them If/Then statements
- All conditions met then disposition is enforced
- “If msg arrives from Y Company, then delete”
- Rule Settings
- Conditions (If) --> Dispositions (Then)
- Email Protection --> Rules --> Rule
- Rule ID cannot be changed so think of a good rule name
- For each filtering module, administrators create rules that determine how to process messages
#### Dispositions
- Made up of Delivery methods and Delivery options
- Quarantine options is on its on
- EX:
- If a msg is from company W (CONDITION)
	- AND
- It contains “X” in the subjection or body (CONDITION)
- ----------------------------------------------------------- 
- Dispositions
- Then continue processing (DELIVERY METHOD)  
	- AND
- Change subject to “Y” (DELIVERY OPTION)
	- AND
- Place a copy in the Job Offer Quarantine folder (DELIVERY OPTION)
- Delivery Methods:
	- Deliver Now: available for all modules, delivers the msg, nothing else
	- Continue: available for all, passes msg to each module for filtering. Once	passes all filtering sent to email infrastructure
	- Reject: all available, permanently reject msg, sender receives reject msg
	- Retry: all available, is reject but sender can retry
	- Discard: all available, accepts msg from host and quietly discard msg	without sender knowing
  - Re-route: available all, route filtered message through different SMTP server. 
#### Quarantine Function
- Quarantine: creates a copy and quarantines the copy instead
- Look at it as a type of repository

## Email Security - Microsoft Defender 365
### Zero-hour auto purge (ZAP) basics
- In Microsoft 365 organizations with mailboxes in Exchange Online, zero-hour auto purge (ZAP) is an email protection feature that retroactively detects and neutralizes malicious phishing, spam, or malware messages that have already been delivered to Exchange Online mailboxes.
- doesn't work in Exchange Online Protection (EOP) environments that protect on-premises Exchange mailboxes
### How ZAP works
- 
