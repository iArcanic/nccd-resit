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
