# FiDo Charity Networks Assignment Coursework 3 Resit
## 1 Overall context
FiDo (FiDo) is a charity. FiDo is planning to move to offices in Coventry. As part of the move, they are planning to implement a better security architecture and network design. This is in comparison to their current arrangement which has evolved haphazardly over the last three decades.

FiDo currently has a workforce of approximately 1300 individuals. A significant proportion of these workers are unsalaried volunteers. Most work predominantly online with a few days each month in the office.

There are several departments including HR, Finance, Corporate Comms and System Administration.

FiDo works closely with a New Zealand collaborator organisation on a range of projects.

FiDo has all its online assets within the domain ```fido22.cyber.test```.

FiDo needs the proposed security architecture and network design to accommodate significant expansion over the next three years.

The FiDo foundation charter requires them to utilise open-source solutions where these exist. Currently and for the foreseeable future, they adopt a Debian by default operating system on all endpoints and infrastructure.

## 2 Our role
We have been engaged as a Security Architect and Network Design consultant by FiDo. We have been supplied with a starter pack. This starter pack comprises:
1. a preliminary infrastructure layout that summarises what FiDo believe to be the main components of their infrastructural needs. This utilises the historic IP address block ```80.64.0.0/16``` that they inherited from the original creator of the organisation in 1988.
2. a preliminary emulation of this infrastructure. This deliberately incorporates negligible security architecture and summarises many bulk features (user endpoints for example) into a small number of representative examples.

## 3 Our task
### 3.1 Zones of trust
1. Re-design the infrastructure to group assets into zones of trust. As well as re-organising existing assets, you should identify and position any infrastructure assets that you believe should be present but are missing. Similarly, you should remove any assets that are present but not appropriate.
2. Implement the reconfigured zones of trust as LANs or VLANs within the Netkit realisation. Insofar as is reasonable, you should utilise what is provided in the starter pack with the minimum essential change.
### 3.2 IP addressing
3. Re-organise the IP address utilisation of the organisation so as to reduce to a realistic minimum, the number of public IP addresses that FiDo should retain from within the ```80.64.0.0/16``` address block. Utilise NAT and / or port-forwarding as appropriate.
4. Implement the re-organised IP address allocation and associated routing within the Netkit realisation.
### 3.3 Traffic filters
5. Determine the filters that should apply between zones of trust (network firewalls) and where significant on endpoints (host firewalls).
6. Implement the filters within the emulated infrastructure.
### 3.4 Verify
7. Verify that connectivity is achieved between appropriate clients and the services they should be able to utilise.
8. Verify that connectivity is prevented between inappropriate clients and the services they should not be able to access.
### 3.5 Augment
9. Design, implement / configure and test additional features that will usefully enhance the organisation's security posture. You should select features that you consider to be particularly important to FiDo and that will also showcase your comprehensive mastery of security architecture and network defence, above and beyond what you have already demonstrated in tasks 3.1 to 3.4 above.

## 6 Marking scheme
### 6.1 Phase 1:
To achieve a mark up to 55% you must:
1. use the specified file names,
2. define and implement credible zones of trust. As a minimum, you should have four: untrusted public internet; internet-facing servers; staff workstations; internal-facing servers,
3. define and implement re-organised IP addressing, using the specified private addresses internally.
4. implement NAT so that client devices on private IP addresses can interact with services provided on the public internet,
5. define and implement filters between zones of trust,
6. partially verify that connectivity is achieved / prevented as appropriate between clients and services,
7. have hashes at the demonstration that match the hashes in the submission nccd-hashes.sha1 file (ie provide evidence that nothing significant has changed between the submission and the demonstration).
### 6.2 Phase 2:
To achieve a mark up to 75%, you must satisfy the following:
1. satisfy all the requirements of phase 1,
2. implement NAT / port-forwarding so the internet facing servers can have private IP addresses,
3. robustly verify connectivity is achieved / prevented as appropriate between clients and services.

# Network Topology
![NCCD CW3 Network Topology Diagram](https://github.com/iArcanic/nccd-resit/assets/18505350/25b618be-2268-425f-bd3e-95091dacee20)

## Subnets + machines
### [Internet](https://github.com/iArcanic/nccd-resit/blob/main/Internet.startup) (`80.64.157.254/26`)
A representation of the public internet within the Netkit virtual environment. Derives from the public IP block which the company's founder inherited, which is `80.64.0.0/16`.

### [Central-router](https://github.com/iArcanic/nccd-resit/blob/main/Central-router.startup) (`192.168.0.2/24`)
Internet-facing router, which facilitates connections between all 6 subnets and helps them communicate with each other. Also acts as a gateway for those subnets to communicate with the public Internet. Has firewall rules for all subnets and machines for easy management.

### DMZ (`10.0.1.0/24`)
Contains machines that act as proxy to filter packets from the external public internet to internal resources. Akin to a security layer, with dummy machines:
- [DMZ-switch](https://github.com/iArcanic/nccd-resit/blob/main/DMZ-switch.startup) (`10.0.1.2/24`): A switch to facilitate outgoing connections to the Central-router and incoming connections to the DMZ subnet.
- [Squid](https://github.com/iArcanic/nccd-resit/blob/main/Squid.startup) (`10.0.1.3/24`): A proxy machine that runs the Squid proxy software. Widely-used for HTTP filtering and caching. Used for content filtering, access control and enhanced privacy.

### External (`10.0.2.0/24`)
Contains external machines, previously hosted on the public internet, but decided to host internally, since they are owned by the company:
- [External-switch](https://github.com/iArcanic/nccd-resit/blob/main/External-switch.startup) (`10.0.2.2/24`): A switch to facilitate outgoing connections to the Central-router and incoming connections to the External subnet.
- [Ext-Office](https://github.com/iArcanic/nccd-resit/blob/main/Ext-Office.startup) (`10.0.2.3/24`): This machine represents external office machines. These are the company's machines that are accessible from the Internet but have been internally hosted for security reasons. They may include typical office devices used by employees.
- [Ext-DNS](https://github.com/iArcanic/nccd-resit/blob/main/Ext-DNS.startup) (`10.0.2.4/24`): This machine represents an external DNS server. It's responsible for handling DNS requests from both internal and external clients. DNS servers resolve domain names to IP addresses, allowing devices to locate each other on the network.
- [Ext-WWW](https://github.com/iArcanic/nccd-resit/blob/main/Ext-WWW.startup) (`10.0.2.5/24`): This machine represents an external web server. It hosts web services that are accessible from the internet. It may contain company websites, applications, or services meant to be accessed by external users.

### Staff (`10.0.3.0/24`)
Contains staff machines, which may be in the form of PC workstations that the company employees use on a day-to-day basis:
- [Staff-switch](https://github.com/iArcanic/nccd-resit/blob/main/Staff-switch.startup) (`10.0.3.2/24`): A switch to facilitate outgoing connections to the Central-router and incoming connections to the Staff subnet.
- [Staff-1](https://github.com/iArcanic/nccd-resit/blob/main/Staff-1.startup) (`10.0.3.3/24`), [Staff-2](https://github.com/iArcanic/nccd-resit/blob/main/Staff-2.startup) (`10.0.3.4/24`), [Staff-3](https://github.com/iArcanic/nccd-resit/blob/main/Staff-3.startup) (`10.0.3.5/24`): These machines represent staff members' workstations. It's used by employees for their daily tasks, including accessing company resources, emails, and other applications.

### Services (`10.0.4.0/24`)
Contains internal services which the Staff subnet requires and interecats with frequently which are required for the organisation to function:
- [Services-switch](https://github.com/iArcanic/nccd-resit/blob/main/Services-switch.startup) (`10.0.4.2/24`): A switch to facilitate outgoing connections to the Central-router and incoming connections to the Services subnet.
- [Int-WWW](https://github.com/iArcanic/nccd-resit/blob/main/Int-WWW.startup) (`10.0.4.3/24`): This machine serves as an internal web server, providing web-based applications or services that are meant to be accessed only within the organization's internal network.
- [Int-DNS](https://github.com/iArcanic/nccd-resit/blob/main/Int-DNS.startup) (`10.0.4.4/24`): This machine is configured as an internal DNS (Domain Name System) server for the organization's network. Its primary purpose is to resolve domain names to IP addresses within the internal network.

### Server (`10.0.5.0/24`)
Contains specialised server-related resources and services crucial to the organisation's daily activities:
- [Server-switch](https://github.com/iArcanic/nccd-resit/blob/main/Server-switch.startup) (`10.0.5.2/24`): A switch to facilitate outgoing connections to the Central-router and incoming connections to the Server subnet.
- [LDAP](https://github.com/iArcanic/nccd-resit/blob/main/LDAP.startup) (`10.0.5.3/24`): This machine hosts an LDAP server, which is used for centralized user authentication and directory services.
- [OpenVPN](https://github.com/iArcanic/nccd-resit/blob/main/OpenVPN.startup) (`10.0.5.4/24`): This machine hosts an OpenVPN server, which provides secure remote access to the internal network over the public internet.

### Management (`10.0.6.0/24`)
Contains admin machines dedicated to managing and monitoring network devices and services within the topology.
- [Management-switch](https://github.com/iArcanic/nccd-resit/blob/main/Management-switch.startup) (`10.0.6.2/24`): A switch to facilitate outgoing connections to the Central-router and incoming connections to the Management subnet.
- [Admin](https://github.com/iArcanic/nccd-resit/blob/main/Admin.startup) (`10.0.6.3/24`): This machine is used only by the nwtwork administrators to manage and control various aspects of the network.

## Firewall rules
Specificed in [Central-router.startup](https://github.com/iArcanic/nccd-resit/blob/main/Central-router.startup).
### Management
Since this is a subnet that cannot be compromised as it contains user privileges as well as access to prohibited commands for common users of the network, it is best to limit the attack vector:
- Allow outgoing packets from the Management subnet to all other subnets.
- Drop incoming packets to the Management subnet from all other subnets.

### DMZ
In the case that the filter does catch malicious packets, we would want to obviously not allow them to pass to the other subnets, so limiting potential attack vectors or expose the internal network:
- Drop outgoing packets from the DMZ subnet to all other subnets.
- Drop incoming packets to the DMZ subnet from all other subnets.

### LDAP + External
Since LDAP contains sensitive information about user directories authentication details, blocking connections to the External subnet, which also has access to the public Internet, limits the attack vector on a highly compromisable machine:
- Drop incoming packets from External subnet to LDAP
- Drop incoming packets from LDAP to External

## NAT rules
Specificed in [Central-router.startup](https://github.com/iArcanic/nccd-resit/blob/main/Central-router.startup).
### SNAT
Allows machines, which have a private IP, to be able to interact with services on the public Internet:
- Reject SNAT for Management subnet: Again, like the firewall rule, blocking connection to the public Internet means that the Management subnet cannot be easily accessed.
- Reject SNAT for Services subnet: Since these are internal machines, they do not require access to the network directly.
- Allow SNAT for all other subnets: General rule to allow other subnets to access the public Internet.

### DNAT
DNAT concerns itself with incoming packets into the network, and the specific machines it should be routed to (based on the protocol):
- Ext-Office, Ext-DNS, Ext-WWW, Int-WWW, Int-DNS, OpenVPN
